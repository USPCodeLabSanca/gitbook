---
description: Parsing de HTML avançado
---

## Introdução

Várias técnicas podem ser usadas para remover o conteúdo que não se pareça com o que estamos procurando, até chegarmos nas
informações desejadas. Neste capítulo, veremos como fazer parse de páginas HTML complicadas a fim de extrair somente as informações desejadas.

## Alternativas ao parsing

Suponha que você esteja visando a certo conteúdo. Talvez seja um nome, uma estatística ou um bloco de texto. A informação pode estar escondida a 20 tags de profundidade em um HTML confuso, sem tags ou atributos HTML convenientes à vista. Suponha que você decida deixar totalmente de lado a cautela e escreva um código como a linha a seguir, na tentativa de extrair os dados:
``` python
bs.find_all('table')[4].find_all('tr')[2].find('td').find_all('div')[1].find('a')
```
Esse código não parece muito bom. Além do aspecto estético da linha, até mesmo a menor das modificações feita por um administrador no site poderá causar falhas em seu web scraper. A linha anterior é frágil e depende de a estrutura do site jamais mudar.
Então quais são as suas opções?
• Procure um link para “imprimir a página” ou, quem sabe, uma versão móvel do site com um HTML mais bem formatado.
• Procure as informações ocultas em um arquivo JavaScript. 
• É mais comum para títulos de página, mas a informação pode estar disponível no próprio URL da página.
• Se, por algum motivo, a informação procurada for exclusiva do site em questão, você estará sem sorte. Se não for, procure pensar em outras fontes a partir das quais seria possível obter essas informações.
Se tiver certeza de que não há alternativas, no resto do capítulo, descreveremos soluções padrões e criativas para selecionar tags de acordo com suas posições, o contexto, os atributos e o conteúdo. As técnicas apresentadas, quando usadas corretamente, serão muito convenientes para escrever web crawlers mais estáveis e confiáveis.

## Outras utilidades do BeautifulSoup

Praticamente todo site que você encontrar conterá folhas de estilo. Embora você ache que uma camada de estilização em sites, projetada especificamente para ser interpretada por navegadores e por seres humanos seja inconveniente, o surgimento do CSS foi extremamente vantajoso para os web scrapers. O CSS se baseia na diferenciação de elementos HTML –
que, de outro modo, poderiam ter exatamente a mesma marcação – para estilizá-los de modo distinto. Algumas tags podem ter o seguinte aspecto:
``` python
<span class="green"></span>
``` 
Outras podem ser assim:
``` python
<span class="red"></span>
``` 
Os web scrapers podem separar facilmente essas tags de acordo com a classe; por exemplo, o BeautifulSoup pode ser usado para obter todos os textos em vermelho (red), mas não os textos em verde (green). Como o CSS depende desses atributos de identificação para estilizar adequadamente os sites, é quase certo que esses atributos de classe e ID sejam abundantes na maioria dos sites modernos.
``` python
from urllib.request import urlopen
from bs4 import BeautifulSoup
html = urlopen('http://www.pythonscraping.com/pages/page1.html')
bs = BeautifulSoup(html.read(), 'html.parser')
nameList = bs.findAll('span', {'class':'green'})
for name in nameList:
    print(name.get_text())
```
Quando executado, esse código deve listar todos os nomes próprios do texto, na ordem em que aparecem em War and Peace. Isso ocorre pois agora chamamos 
``` python
bs.find_all(tagName, tagAttributes) 
```
para obter uma lista de todas as tags da página, em vez de obter somente a primeira. Depois de obter uma lista de nomes, o programa itera por todos os nomes da lista e exibe 
´´´ pyhton
name.get_text() 
´´´
para separar o conteúdo das tags.

# find() e find_all() com o BeuatifulSoup

Com elas, é possível filtrar facilmente as páginas HTML 
e encontrar as listas de tags desejadas – ou uma só tag – de acordo com seus vários atributos.

```python
find_all(tag, attributes, recursive, text, limit, keywords)
find(tag, attributes, recursive, text, keywords)
```
O argumento attributes aceita um dicionário Python de atributos e faz a correspondência com tags que contenham qualquer um desses atributos. O argumento recursive é um booleano. Por padrão, find_all funciona de modo recursivo (recursive é definido com True), assim, a função find_all analisará os filhos, e os filhos dos filhos, em busca de tags que correspondam aos parâmetros. O argumento text é peculiar por fazer a correspondência com base no conteúdo textual das tags, em vez de usar suas propriedades. O argumento limit obviamente é usado somente no método find_all; find é equivalente à chamada de find_all com um limite igual a 1. O argumento keyword permite selecionar tags que contenham um atributo ou um conjunto de atributos específicos. 

