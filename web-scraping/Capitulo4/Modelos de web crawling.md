---
description: Modelos de web crawling
---

# Resumo
Neste capitulo, o objetivo é construir um crawler que seja organizado e escalável. Para isso, primeiramente devemos nos atentar as entradas e aos dados que queremos obter.
Para isso, utilizaremos web crawlers que coletam um número limitado de dados por página, pois não lidaremos com banco de dados.

## Planejando e definindo objetos
Sempre que pensamos em obter determinado dado, buscamos sites específicos e nos baseamos neles, resultando em novos dados a cada página visitada e um conjunto difícil de interpretar. Para construir um crawler eficiente, é preciso considerar os aspectos mais gerais de cada 'objeto' e buscar obter apenas o que será necessário para sua aplicação.

## Lidando com diferentes layouts
Sabendo que é preciso lidar com diversos sites com estruturas diferentes, o jeito mais óbvio de obter esses dados é produzir um crawler ou um parser de página específico para cada um. No entanto, essa abordagem deixa de ser eficiente no momento em que você precisa escalar seu código. 

Caso opte por esse caminho, será possível observar um certo padrão na função de cada parser, pois todos possuem o objetivo de obter o mesmo dado. Por exemplo, se busca-se capturar o título, data de publicação e o primeiro parágrafo de sites de notícias, pode-se perceber que as únicas mudanças necessárias para obter esses dados é a sua localização na determinada página. Para isso, consegue-se criar uma função genérica o suficiente para que receba essa posição e retorne o dado.

Neste capítulo, será introduzido a função 'select' de um objeto BeautifulSoup. Tal função, realiza a busca de determinada tag que contenha o seletor CSS especificado.

```html
<a> Aprendendo web scraping.</a>
<a class='Paragrafo'>Testando seletores.</a>
```

Em CSS, para selecionar determinada classe, utiliza-se '.nomeClasse'. A função select exigirá o mesmo padrão de argumento. 
Se o objetivo é selecionar apenas a tag 'a' com a classe 'Paragrafo', utilizamos:

```python
bs.select('a.Paragrafo')
```

Essa função retornará uma lista com todas as correspondências encontradas.

# Estruturando os crawlers
Esta seção tem o objetivo de exemplificar uma estrutura capaz de coletar dados e links de maneira automatizada. O crawler que será apresentado é um bom começo para os que você irá construir a partir de agora, contemplando a maioria dos problemas que você encontrará, salvo algumas mudanças.

## Rastreando os sites por meio de pesquisas
O modo mais prático de encontrar sites é pesquisando. Embora seja necessário uma palavra-chave ou termo específico para haver uma pesquisa eficiente, a maioria dos sites possuem uma página de busca com um link base concatenado com algumas outras informações, como por exemplo, "https://example.com?search=meuTopico". 

Dentro da página, o link pode ser relativo ("/articles/page.html") ou absoluto ("https://example.com/articles/page.html"). Essa propriedade será armazenada na estrutura criada para o website.

Após a pesquisa, grande parte dos sites mantém os resultados em uma estrutura de fácil indentificação, em geral com um tag conveniente ao redor, como `<span class='Result'>`, cujo formato também será armazenado.

Primeiramente, o código possuirá uma classe denominada Content, que será a base de identificação para todos os sites/artigos.

```python
class Content:
    """Classe-base comum para todos os artigos/páginas"""
    def __init__(self, topic, url, title, body):
        self.topic = topic
        self.title = title
        self.body = body
        self.url = url
    def print(self):
        """
        Uma função flexível de exibição controla a saída
        """
        print(Novo artigo encontrado do topico:", self.topic)
        print("TITLE: {}".format(self.title))
        print("BODY:\n{}".format(self.body))
        print("URL: {}".format(self.url), '\n')
```

Cada objeto dessa classe armazenará o URL, o corpo da página HTML (body), seu título e o tópico que gerou sua pesquisa.

Já, a classe Website, será criada para que seja possível armazenar todos os dados referentes a estrutura do site e ao modo como a pesquisa deve ocorrer. Os atributos são:
- name: Nome da página 
- url: Link para acessar a site
- searchUrl: Link base da página de pesquisa do site
- resultListing: Define o "local" em que estão armazenados os resultados da pesquisa na página de busca
- resultUrl: Define o "local" exato em que está o URL do item pesquisado em resultListing 
- absoluteUrl: Indica se o resultUrl é absoluto ou não
- titleTag: Título da página web
- bodyTag: Body da página web

Vale lembrar que o "local" será buscado por uma função select.

```python
class Website:
    def __init__(self, name, url, searchUrl, resultListing,
        resultUrl, absoluteUrl, titleTag, bodyTag):
        self.name = name
        self.url = url
        self.searchUrl = searchUrl
        self.resultListing = resultListing
        self.resultUrl = resultUrl
        self.absoluteUrl=absoluteUrl
        self.titleTag = titleTag
        self.bodyTag = bodyTag
```

Agora será apresentado a classe Crawler, ela será capaz de realizar as buscas automatizadas a partir dos sites inserido pelo usuário. A classe possui uma função que faz o acesso a página e retorna um objeto BeautifulSoup (getPage). Um outro método que faz retorna o texto de determinada tag a partir de um seletor (safeGet). O método de pesquisa, que irá realizar a busca de determinado tema na página e, após fazer o acesso, buscará todos os itens que forem apresentados, recuperando seus determinados URLs. Por fim, irá recuperar o título e o body da página resultante.

```python
import requests
from bs4 import BeautifulSoup

class Crawler:
    def getPage(self, url):
        try:
            req = requests.get(url)
        except requests.exceptions.RequestException:
            return None
        return BeautifulSoup(req.text, 'html.parser')

    def safeGet(self, pageObj, selector):
        childObj = pageObj.select(selector)
        if childObj is not None and len(childObj) > 0:
            return childObj[0].get_text()
        return ""
    
    def search(self, topic, site):
        """
        Pesquisa um dado site em busca de um dado tópico e registra
        todas as páginas encontradas
        """
        
        bs = self.getPage(site.searchUrl + topic)
        searchResults = bs.select(site.resultListing)

        for result in searchResults:
            url = result.select(site.resultUrl)[0].attrs["href"]
            
            # Verifica se é um URL relativo (./) ou absoluto (https)
            if(site.absoluteUrl):
                bs = self.getPage(url)
            else:
                bs = self.getPage(site.url + url)

            if bs is None:
                print("Something was wrong with that page or URL. Skipping!")
                return

            title = self.safeGet(bs, site.titleTag)
            body = self.safeGet(bs, site.bodyTag)
            
            if title != '' and body != '':
                content = Content(topic, url, title, body)
                content.print()

#--------------------------Execução

crawler = Crawler()
siteData = [
    ['Livrarias Curitiba', 'https://www.livrariascuritiba.com.br/',
    'https://www.livrariascuritiba.com.br/','li.livros',
    'a.productImage', True, 'h1 div.productName', 'div.productDescription']
]

sites = []
for row in siteData:
    sites.append(Website(row[0], row[1], row[2], row[3], row[4], row[5], row[6], row[7]))

topics = ['python', 'data science']
for topic in topics:
    print("RECEBENDO DADOS SOBRE: " + topic)
    for targetSite in sites:  
        crawler.search(topic, targetSite)
```

Durante a execução, esse script percorre os itens da lista *topics* e, pra cada topico, fará a busca em cada site presente em *siteData*. Em seguida, rastreia cada informação apresentada anteriormente e, caso ocorra tudo corretamente, os dados base de cada página serão exibidos no console. Um exemplo, executado durante a produção deste gitbook se apresentou no seguinte formato:

```
GETTING INFO ABOUT: python
New article found for topic: python
TITLE: Python Para Analise De Dados - Novatec
BODY:
Obtenha instruções completas para manipular, processar, limpar e extrair informações de conjuntos de dados em Python. Atualizada para Python 3.6, este guia prático está repleto de casos de estudo práticos que mostram como resolver um amplo conjunto de problemas de análise de dados de forma eficiente. Você conhecerá as versões mais recentes do pandas, da NumPy, do IPython e do Jupyter no processo. Escrito por Wes McKinney, criador do projeto Python pandas, este livro contém uma introdução prática e moderna às ferramentas de ciência de dados em Python. É ideal para analistas, para quem Python é uma novidade, e para programadores Python iniciantes nas áreas de ciência de dados e processamento científico. Os arquivos de dados e os materiais relacionados ao livro estão disponíveis no GitHub.
URL: https://www.livrariascuritiba.com.br/python-para-analise-de-dados-novatec-lv426594/p 

New article found for topic: python
TITLE: Python Para Desenvolvedores - Novatec
...
```

### Explicando o teste
Para o exemplo, foi utilizado o site da empresa Livrarias Curitiba. Para isso, foram informados, respectivamente, seu URL (https://www.livrariascuritiba.com.br/), URL de busca que terá o tópico concatenado (https://www.livrariascuritiba.com.br/), tag+seletor de onde se encontram os resultados da busca (li.livros), tag+seletor de onde se encontra o URL - na página de busca - para cada item resultante (a.productImage), booleano referente ao modelo do URL encontrado (True), tag+seletor onde está o título da página (h1 div.productName) e tag+seletor de onde se localiza a descrição do produto (div.productDescription).

Essa estruturação dos laços de repetição, buscando a mesma página para cada tópico em momentos diferentes, foi utilizada para evitar uma sobrecarga no servidor. Pois, caso houvessem centenas de tópicos a serem buscados, e os laços estivessem invertidos, também seriam realizados centenas de acessos. Se atentar a esse ponto durante a produção de seus web crawlers é de fundamental importância.