---
description: Escrevendo web crawlers
---

# Introdução
Nos capítulos anteriores, o Web Scraping foi mostrado de forma mais "artificial", em sites mais simples e portanto distantes do cotidiano, compostos por páginas únicas. 
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
