# Introdução ao Node

## Introdução

O Node JS é um interpretador de Javascript totalmente independente do navegador, isto é, suas funções podem ser feitas totalmente sem a ajuda de um browser.

Ele foi desenvolvido em 2009 a partir do Chrome v8, uma engine escrita em C++ feita pela Google para interpretar e rodar códigos escritos em Javascript. O Node é comumente usado em aplicações relacionadas a Web.

O Node trabalha de forma assíncrona, isto é, os comandos e requisições vão ser tratados por um processo único, chamado event-loop. Nele, quaisquer requisições feitas pela aplicação são colocadas em uma pilha, onde que são tratadas uma a uma pelo event loop. Assim, como as requisições são tratadas por um só processo, não há problema que a execução deste processo bloqueie outras execuções, até mesmo a do navegador.

## Gerenciadores de Pacotes

Gerenciadores de pacotes, como npm ou yarn, são mecanismos utilizados para instalar, atualizar ou remover pacotes. Esses pacotes são disponibilizados publicamente em repositórios online, com gerenciamento de dependência ou versão a ser utilizada pela aplicação, e funcionam como auxiliadores no desenvolvimento de aplicativos usando NodeJS. Caso se interesse pelo Node Package Manager \(NPM\), que é o maior repositórios de software do mundo, há uma lista de pacotes que podem ser encontrada em [https://npmjs.org/](https://npmjs.org/). Lá o ecossistema é público, o que te permite publicar os seus próprios pacotes. Além disso, eles podem ser acessados via uma ferramenta de Command Line Inteface \(CLI\) do NPM.

## Instalando

Há algumas formas de instalar o Node, dependendo do seu sistema operacional. Caso seu sistema seja Linux, o seguinte pode ser feito usando o terminal:

```bash
sudo apt-get install nodejs
```

Para Windows ou Mac, acesse o site do NodeJS, onde podem ser encontrados os arquivos de instalação do Node: [https://nodejs.org/en/](https://nodejs.org/en/)

_Obs: No site do Node, podem ser encontrado arquivos de instalação para Linux, caso você não queira instalar pelo terminal._

## Utilizando o Node

Pelo Windows ou Mac, há um arquivo disponível após a instalação. Neste arquivo, que lembra um terminal, você pode utilizar o Javascript para realizar comandos quaisquer, como se estivesse em um arquivo da linguagem \(.js\).

Para as distribuições Linux, o seguinte deve ser feito no terminal:

```bash
node
```

Caso queira executar um arquivo javascript:

```bash
node <nome_do_arquivo>.js
```

