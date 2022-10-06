---
description: Executando o BeatifulSoup e conectando-se de forma confiável e tratando exceções
---

# Executando o BeatifulSoup

Vamos apresentar um exemplo da execução da biblioteca BeutifulSoup:
``` python
from urllib.request import urlopen
from bs4 import BeautifulSoup
html = urlopen('http://www.pythonscraping.com/pages/page1.html')
bs = BeautifulSoup(html.read(), 'html.parser')
print(bs.h1)
``` 
Eis a saída:
``` python
<h1>An Interesting Title</h1>
``` 
Note que somente a primeira instância da tag h1 encontrada na página é devolvida. A função urlopen está sendo importada e a função html.read() é chamada para obter o conteúdo HTML da página. 

## Objeto BeautifulSoup

Além da string de texto, o BeautifulSoup também pode
usar diretamente o objeto de arquivo devolvido por urlopen, sem precisar chamar .read() antes:
``` python
bs = BeautifulSoup(html, 'html.parser')
```
O conteúdo HTML é então transformado em um objeto BeautifulSoup com a seguinte estrutura:
``` python
• html → <html><head>...</head><body>...</body></html>
    • head → <head><title>A Useful Page<title></head>
        • title → <title>A Useful Page</title>
    • body → <body><h1>An Int...</h1><div>Lorem ip...</div></body>
        • h1 → <h1>An Interesting Title</h1>
        • div → <div>Lorem Ipsum dolor...</div>
``` 
Observe que a tag h1 que você extraiu da página está aninhada a dois níveis de profundidade na estrutura do objeto BeautifulSoup (html → body → h1). No entanto, ao buscá-la no objeto, é possível acessar a tag h1 diretamente:
``` python
bs.h1
``` 
Com efeito, qualquer uma das chamadas de função a seguir produziria o mesmo resultado:
``` python
bs.html.body.h1
bs.body.h1
bs.html.h1
``` 
Ao criar um objeto BeautifulSoup, dois argumentos são passados:
``` python
bs = BeautifulSoup(html.read(), 'html.parser')
``` 
O primeiro é o texto HTML no qual o objeto se baseia, e o segundo especifica o parser que queremos que o BeautifulSoup use para criar esse objeto. Na maioria dos casos, o parser escolhido não fará diferença. Mas, para citar como exemplos, além do html.parser, outros 2 parsers famosos são o lxml e o html5lib.

# Conectando-se de forma confiável e tratando exceções

A web é confusa. Os dados são mal formatados, os sites ficam inativos e tags de fechamento podem estar ausentes. Assim, devemos sempre prever possíveis exceções.

Vamos analisar a primeira linha de nosso scraper, depois das instruções de importação, e descobrir como lidar com qualquer exceção que seja lançada:
``` python
html = urlopen('http://www.pythonscraping.com/pages/page1.html')
```
Dois erros podem ocorrer nessa linha:
• A página não é encontrada no servidor (ou houve um erro ao obtê-la).
• O servidor não foi encontrado.

## A página não é encontrada no servidor

Nesse caso, um erro de HTTP será devolvido. Esse erro pode ser
“404 Page Not Found” (página não encontrada), “500 Internal Server Error” (erro interno do servidor), e assim por diante. Em todos esses casos, a função urlopen lançará a exceção genérica HTTPError. Essa exceção pode ser tratada da seguinte maneira:
``` python
from urllib.request import urlopen
from urllib.error import HTTPError
try:
html = urlopen('http://www.pythonscraping.com/pages/page1.html')
except HTTPError as e:
print(e) -> devolve null, executa um break ou algum outro "Plano B"
else: -> o programa continua. Nota: se você retornar ou executar um break no catch da exceção, não será necessário usar a instrução "else"
```
Se um código de erro HTTP for devolvido, o programa agora exibirá o erro e não executará o resto do programa que está na instrução else.

## Se o servidor não for encontrado

Nesse caso, urlopen lançará um URLError. Isso quer dizer que não foi possível acessar nenhum servidor e, como o servidor remoto é responsável por devolver códigos de status HTTP, um HTTPError não pôde ser lançado, e o erro URLError, mais grave, deve ser capturado. Podemos acrescentar uma verificação para saber se é isso que está acontecendo:
``` python
from urllib.request import urlopen
from urllib.error import HTTPError
from urllib.error import URLError
try:
html = urlopen('https://pythonscrapingthisurldoesnotexist.com')
except HTTPError as e:
print(e)
except URLError as e:
print('The server could not be found!')
else:
print('It Worked!')
```

### O conteúdo da página não ser exatamente o que você esperava

Sempre que acessar uma tag em um objeto BeautifulSoup,
acrescentar uma verificação para garantir que ela realmente exista é uma atitude inteligente. Se você tentar acessar uma tag que não existe, o BeautifulSoup devolverá um objeto None. O problema é que tentar acessar uma tag em um objeto None resultará no lançamento de um AttributeError.

A linha a seguir (em que nonExistentTag é uma tag inventada, e não o nome de uma verdadeira função do BeautifulSoup):
``` python
print(bs.nonExistentTag)
``` 
Devolve um objeto None. É perfeitamente razoável conferir e tratar esse objeto. O problema ocorrerá se você não o conferir, mas prosseguir tentando chamar outra função no objeto None, conforme mostra o código a seguir:
``` python
print(bs.nonExistentTag.someTag)
``` 
Uma exceção será devolvida:
``` python
AttributeError: 'NoneType' object has no attribute 'someTag'
``` 
Então, como é possível se proteger nessas duas situações? O modo mais fácil é verificar as duas situações explicitamente:
``` python
try:
badContent = bs.nonExistingTag.anotherTag
except AttributeError as e:
print('Tag was not found')
else:
if badContent == None:
print ('Tag was not found')
else:
print(badContent)
``` 

## Reorganizando o código

Nesse exemplo, criamos uma função getTitle que devolve o título da página, ou um objeto None caso tenha havido algum problema para obtê-lo. Em getTitle, verificamos se houve um HTTPError, como no exemplo anterior, e encapsulamos duas das linhas do BeautifulSoup em uma instrução try. Um AttributeError pode ser lançado por qualquer uma dessas linhas (se o servidor não existir, html seria um objeto None e html.read() lançaria um AttributeError). Na verdade, você poderia incluir quantas linhas quiser em uma instrução try, ou chamar outra função totalmente diferente, que poderia lançar um AttributeError em qualquer ponto.

``` python
from urllib.request import urlopen
from urllib.error import HTTPError
from bs4 import BeautifulSoup
def getTitle(url):
try:
html = urlopen(url)
except HTTPError as e:
return None
try:
bs = BeautifulSoup(html.read(), 'html.parser')
title = bs.body.h1
except AttributeError as e:
return None
return title
title = getTitle('http://www.pythonscraping.com/pages/page1.html')
if title == None:
print('Title could not be found')
else:
print(title)
```
