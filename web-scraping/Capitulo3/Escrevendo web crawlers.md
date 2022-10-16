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
  
  
 

