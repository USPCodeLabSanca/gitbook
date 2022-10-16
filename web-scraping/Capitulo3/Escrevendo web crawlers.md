---
description: Escrevendo web crawlers
---

# Introdução
Nos capítulos anteriores, o Web Scraping foi mostrado de forma mais "artificial", em sites mais simples e compostos por páginas únicas. 
Neste capítulo, veremos scrapers sendo utilizados em problemas do mundo real.

# Percorrendo um único domínio
Tendo como exemplo o Six Degrees of Wikipedia - jogo que consiste na associação de artigos da Wikipedia ligados entre si -, o livro propõe
um simples script Python que obtém uma lista de links presentes em uma página da Wikipedia.

```python
from urrlib.request import urlopen
from bs4 import BeautifulSoup

html = urlopen('http://en.wikipedia.org/wiki/Kevin_Bacon')
bs = BeautifulSoup(html, 'html.parser')
for link in bs.find_all('a'):
  if 'href' in link.attrs:
  print(link.attrs['href'])

```
Analisando a lista gerada, vemos que alguns itens indesejados apareceram, como links para caixas de texto e até para rodapés:

```html
//wikimediafoundation.org/wiki/Privacy_policy
//en.wikipedia.org/wiki/Wikipedia:Contact_us
```

Os links que estávamos procurando - os que apontam para outras páginas de artigo - têm as seguintes características em comum:

- Estão na div com id bodyContent
- Os  URLs não contém dois-pontos
- Os URLs começam com /wiki/

Com esse padrão em mente, podemos revisar o código usando a expressão regular ^(/wiki/)((?!:).)*$"):

```python
from urllib.request import urlopen
from bs4 import BeautifulSoup
import re

html = urlopen('http://en.wikipedia.org/wiki/Kevin_Bacon')
bs = BeautifulSoup(html, 'html.parser')
for link in bs.find('div', {'id':'bodyContent'}).find_all(
  'a', href=re.compile('^(/wiki/)((?!:).)*$')):
  if 'href' in link.attrs:
    print(link.attrs['href'])
```
Executando esse código, obtemos uma lista de todos os URLs de artigo para os quais o artigo inicial da Wikipedia aponta. Embora interessante, essa ideia pode ser inútil na prática. Portanto, podemos fazer uma atualização:


- Função getLinks que recebe um URL de um artigo no formato /wiki/<nome> e devolve uma lista com os URLS de outros artigos associados
- Função principal que chame getLinks, escolha um link aleatório na página e chame getLinks novamente, até que o programa seja interrompido ou nada seja encontrado

```python
from urllib.request import urlopen
from bs4 import BeautifulSoup
import datetime
import random
import re
  
random.seed(datetime.datetime.now())
def getLinks(articleUrl):
  html = urlopen('http://en.wikipedia.org{}'.format(articleUrl))
  bs = BeautifulSoup(html, 'html.parser')
  return bs.find('div', {'id':'bodyContent'}).find_all('a',
    href=re.compile('^(/wiki/)((?!:).)*$'))

links = getLinks('/wiki/Kevin_Bacon')
while len(links) > 0:
  newArticle = links[random.randint(0, len(links)-1)].attrs['href']
  print(newArticle)
  links = getLinks(newArticle)
```
O corpo principal do programa define uma lista de tags de links. Depois, o laço encontra uma tag de link aleatória para outro artigo na página, extraindo o href dela, exibindo a página e obtendo uma nova lista de links.

# Rastreando um site completo
Rastrear um site completo pode ser conveniente para várias tarefas, como para gerar um mapa do site em questão ou para coleta de dados.
A abordagem inicial consiste em procurar uma página inicial e ir "descendo" para os links mais internos. Porém, se cada página tiver 10 links internos, por exemplo, e o site tiver uma profundidade de 5 páginas, o número total de páginas que deverão ser rastreadas é de 100.000.
Isso deve-se ao fato de que muitos links internos são duplicados, ou seja, precisamos evitar que uma mesma página seja rastreada mais de uma vez. Usaremos conjuntos.
  
```python
from urllib.request import urlopen
from bs4 import BeautifulSoup
import re
  
pages = set()
def getLinks(pageUrl):
  global pages
  html = urlopen('http://en.wikipedia.org{}'.format(pageUrl))
  bs = BeautifulSoup(html, 'html.parser')
  for link in bs.find_all('a', href=re.compile('^(/wiki/)')):
    if 'href' in link.attrs:
      if link.attrs['href'] not in pages:
        #Encontramos uma página nova
        newPage = link.attrs['href']
        print(newPage)
        pages.add(newPage)
        getLinks(newPage)
getLinks('')

```
Aqui, o scraper procura todos os links que comecem com /wiki/, independente de qualquer outro fator.
  
# Coletando dados de um site completo
Se quiséssemos construir um scraper que colete título, primeiro parágrafo do conteúdo e um link para editar a página (caso exista), precisaríamos observar algumas páginas para estabelecer um padrão:
- Todas os títulos estão em tags h1 -> span
- Todo o texto do corpo encontra-se na div#bodyContent
- Links para edição só estão presentes em páginas de artigo, sob a tag li#ca-edit, em li#ca-edit -> span -> a

Modificando o código anterior:
```python
from urllib.request import urlopen
from bs4 import BeautifulSoup
import re
  
pages = set()
def getLinks(pageUrl):
  global pages
  html = urlopen('http://en.wikipedia.org{}'.format(pageUrl))
  bs = BeautifulSoup(html, 'html.parser')
  try:
    print(bs.h1.get_text())
    print(bs.find(id ='mw-content-text').find_all('p')[0])
    print(bs.find(id='ca-edit').find('span')
      .find('a').attrs['href'])
  except AttributeError:
    print('This page is missing something! Continuing.')
  for link in bs.find_all('a', href=re.compile('^(/wiki/)')):
    if 'href' in link.attrs:
      if link.attrs['href'] not in pages:
      #Encontramos uma página nova
      newPage = link.attrs['href']
      print('-'*20)
      print(newPage)
      pages.add(newPage)
      getLinks(newPage)
getLinks('')
```
# Rastreando pela internet
Antes de escrever um crawler, é importante definir
- Quais dados você quer obter
- Quando o crawler alcançar um site em particular, ele segue para o próximo link ou permanece no mesmo site para explorar outros níveis?
- Há alguma condição para não coletar um site em particular?
- E a parte legal/judicial da coisa? (MUITO IMPORTANTE!)

Também é importante definir funções Python que, quando combinadas, podem executar vários tipos de web scraping:
```python
from urllib.request import urlopen
from urllib.parse import urlparse
from bs4 import BeautifulSoup
import re
import datetime
import random
  
pages = set()
random.seed(datetime.datetime.now())
  
#Obtém uma lista de todos os links internos encontrados em uma página
def getInternalLinks(bs, includeUrl):
  includeUrl = '{}://{}'.format(urlparse(includeUrl).scheme,
    urlparse(includeUrl).netloc)
internalLinks = []
#Encontra todos os links que começam com "/"
for link in bs.find_all('a',
    href=re.compile('^(/|.*'+includeUrl+')')):
    if link.attrs['href'] is not None:
       if link.attrs['href'] not in internalLinks:
          if(link.attrs['href'].startswith('/')):
             internalLinks.append(
                includeUrl+link.attrs['href'])
          else:
            internalLinks.append(link.attrs['href'])
return internalLinks 
  
#Obtém uma lista de todos os links externos encontrados em uma página
def getExternalLinks(bs, excludeUrl):
  externalLinks = []
  #Encontra todos os links que começam com "http" e que
  #não contenham o URL atual
  for link in bs.find_all('a',
    href=re.compile('^(http|www)((?!'+excludeUrl+').)*$')):
    if link.attrs['href'] is not None:
      if link.attrs['href'] not in externalLinks:
         externalLinks.append(link.attrs['href'])
return externalLinks
  
def getRandomExternalLink(startingPage):
  html = urlopen(startingPage)
  bs = BeautifulSoup(html, 'html.parser')
  externalLinks = getExternalLinks(bs,
  urlparse(startingPage).netloc)
if len(externalLinks) == 0:
  print('No external links, looking around the site for one')
  domain = '{}://{}'.format(urlparse(startingPage).scheme,
    urlparse(startingPage).netloc)
  internalLinks = getInternalLinks(bs, domain)
  return getRandomExternalLink(internalLinks[random.randint(0,
                        len(internalLinks)-1)])
else:
  return externalLinks[random.randint(0, len(externalLinks)-1)]
def followExternalOnly(startingSite):
  externalLink = getRandomExternalLink(startingSite)
  print('Random external link is: {}'.format(externalLink))
  followExternalOnly(externalLink)

followExternalOnly('http://oreilly.com')
```
Esse programa começa em http://oreilly.com e pula aleatoriamente de um link externo para outro, tendo como saída, por exemplo:
http://igniteshow.com/
http://feeds.feedburner.com/oreilly/news
http://hire.jobvite.com/CompanyJobs/Careers.aspx?c=q319
http://makerfaire.com/

Nem sempre podemos garantir que links externos serão encontrados na primeira página de um site. Nesse caso, um método utilizado é o de explorar recursivamente os níveis de um site até encontrar um link externo.
A vantagem de separar tarefas em funções simples é que o código pode ser facilmente atualizado no futuro se quisermos executar uma tarefa de rastreamento diferente da original.
  
