---
description: Seu primeiro web scraper
---

# Introdução

Este capítulo começa com o básico sobre como enviar uma requisição GET (uma requisição para buscar, ou “obter” (get) o conteúdo de uma página web) a um servidor web a fim de obter uma página específica, ler a saída HTML dessa página e fazer uma extração simples de dados para isolar o conteúdo que você estiver procurando.

# Conectando

Quando uma máquina quer conversar com outra, há uma troca de informações entre as máquinas que querem se comunicar. Nessa troca, o navegador web não atua em lugar nenhum. O navegador web é uma aplicação útil para criar pacotes de informações, dizendo ao seu sistema operacional que os envie e interpretando os dados recebidos na forma de imagens bonitas, áudios, vídeos e texto. 

Entretanto, um navegador web é somente um código, e um código pode ser dividido, separado em seus componentes básicos, reescrito, reutilizado, e você pode fazer com que ele aja como você quiser. Um navegador web pode dizer ao processador que envie dados para a aplicação que trata a sua interface sem fio (ou com fio), mas você pode fazer o mesmo em Python usando apenas três linhas de código:

```python
from urllib.request import urlopen
html = urlopen('http://pythonscraping.com/pages/page1.html')
print(html.read())
```

É importante começar a pensar nesses endereços como “arquivos”
em vez de “páginas” pois a maioria das páginas web modernas tem muitos arquivos de recursos associados a elas. Podem ser arquivos de imagens, arquivos JavaScript, arquivos CSS ou qualquer outro conteúdo associado à página sendo requisitada. Quando um navegador web encontra uma tag como:
``` html
<img src="cuteKitten.jpg">
```
 Ele sabe que deve fazer outra requisição ao servidor a fim de obter os dados do arquivo cuteKitten.jpg e renderizar totalmente a página para o usuário. É claro que seu script Python não tem a lógica para voltar e requisitar vários arquivos (ainda); ele é capaz de ler apenas o único arquivo HTML que você requisitou diretamente.

# Introdução ao BeautifulSoup

A biblioteca BeautifulSoup ajuda a formatar e a organizar a
web confusa, fazendo correções em um código HTML mal formatado e apresentando objetos Python que podem ser facilmente percorridos, os quais representam estruturas XML.

## Instalando o BeautifulSoup

Usaremos a biblioteca BeautifulSoup 4 (também conhecida como BS4) neste gitbook. As instruções completas para instalar o BeautifulSoup 4 podem ser encontradas em Crummy.com
(https://www.crummy.com/software/BeautifulSoup/bs4/doc/); no entanto, o método básico para Linux é exibido a seguir:
``` bash
$ sudo apt-get install python-bs4
``` 
Para Macs, execute:
``` bash
$ sudo easy_install pip
```
Esse comando instala o gerenciador de pacotes Python pip. Então execute o comando a seguir para instalar a biblioteca:
``` bash
$ pip install beautifulsoup4
```
Instalar pacotes no Windows é um processo quase idêntico àquele usado em Mac e Linux. Faça download da versão mais recente do BeautifulSoup 4 a partir da página de download
(http://www.crummy.com/software/BeautifulSoup/#Download), vá para o diretório no qual você o descompactou e execute:
``` bash
> python setup.py install
```
É isso! O BeautifulSoup agora será reconhecido como uma biblioteca Python em seu computador. 




