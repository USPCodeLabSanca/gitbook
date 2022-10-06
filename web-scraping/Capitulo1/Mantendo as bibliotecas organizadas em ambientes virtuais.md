---
description: Mantendo as bibliotecas organizadas em ambientes virtuais
---

# Mantendo as bibliotecas organizadas em ambientes virtuais

Se você pretende trabalhar com vários projetos Python, ou precisa de uma maneira fácil de empacotar projetos com todas as bibliotecas associadas, ou está preocupado com possíveis
conflitos entre bibliotecas instaladas, é possível instalar um ambiente virtual Python a fim de manter tudo separado e simples de administrar.

Ao instalar uma biblioteca Python sem um ambiente virtual, ela será instalada globalmente. Em geral, isso exige que você seja um administrador ou execute como root, e que a biblioteca Python esteja disponível para todos os usuários de todos os projetos no computador. Felizmente, criar um ambiente virtual é fácil:
``` bash
$ virtualenv scrapingEnv
``` 
Esse comando cria um novo ambiente chamado scrapingEnv.

## Ativando o ambiente

O ambiente virtual deve ser ativado para ser usado:
``` bash
$ cd scrapingEnv/
$ source bin/activate
``` 
Depois de ativado, o nome do ambiente será exibido no prompt de comandos para que você lembre que está trabalhando nele no momento. Qualquer biblioteca que você instalar ou qualquer script que executar estarão somente nesse ambiente virtual.
Trabalhando no ambiente scrapingEnv recém-criado, você poderá instalar e usar o BeautifulSoup; por exemplo:
``` bash
(scrapingEnv)ryan$ pip install beautifulsoup4
(scrapingEnv)ryan$ python
> from bs4 import BeautifulSoup
``` 

## Desativando o ambiente

O comando deactivate pode ser usado para sair do ambiente; depois disso, não será mais possível acessar nenhuma biblioteca que tenha sido instalada no ambiente virtual:
``` bash
(scrapingEnv)ryan$ deactivate
ryan$ python
> from bs4 import BeautifulSoup
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
ImportError: No module named 'bs4'
``` 
Manter todas as bibliotecas separadas por projeto também facilita compactar a pasta completa do ambiente e enviá-la para outra pessoa. Desde que essas pessoas tenham a mesma versão de Python instalada em seus computadores, o código funcionará no ambiente virtual, sem exigir a instalação de nenhuma biblioteca.

