# Introdução ao Node

### Introdução

O Node JS é um ambiente de javascript assíncrono que é totalmente server-side, isto é, suas funções podem ser feitas totalmente sem a ajuda de um browser.

Ele foi desenvolvido em 2009 no Chrome v8, uma engine escrita em C++ feita pela Google. Usada em aplicações relacionadas a Web, além de implementar o ECMAScript e o WebAssembly.

Como mencionado, o node trabalha de forma assíncrona, isto é, é feito por uma thread única \(ou single-thread\). Dessa forma, os comandos e requisições vão ser tratados só por uma thread, ou como já explicado, o event-loop.

### Gerenciadores de Pacotes 

Gerenciadores de pacotes, como npm ou yarn, são mecanismos utilizados para instalar, atualizar ou remover componentes. Esses componentes são disponibilizados publicamente em repositórios online, com gerenciamento de dependência ou versão do pacote a ser utilizado. Caso se interesse pelo NPM, há uma lista de componentes que podem ser encontrada em [https://npmjs.org/](https://npmjs.org/). Lá, o ecossistema é público, podendo publicar os seus próprios pacotes.  Além disso, esses podem ser acessados via uma ferramenta CLI do NPM.

### Instalando

Há algumas formas de instalar o Node, dependendo do seu sistema operacional. Caso seu sistema seja Linux, o seguinte pode ser feito usando o terminal:

```bash
sudo apt-get install nodejs
```

No Windows ou Mac, pode ser acessado o site do nodejs, onde pode ser encontrado os arquivos de instalação do node.

Obs: No site do Node, pode ser encontrado arquivos de instalação para Linux, caso não queira instalar pelo terminal.

### Utilizando o Node

Pelo Windows ou Mac, há um arquivo disponível após a instalação. Neste arquivo, que lembra um terminal, tem a possibilidade de utilizar o javascript para realizar comandos quaisquer, como se estivesse em um arquivo qualquer.

Para as distribuições Linux, o seguinte deve ser feito no terminal:

```bash
node
```

Caso queira executar um arquivo javascript:

```bash
node <nome_do_arquivo>.js
```

