# Utilizando o NPM

O NPM, como mencionado no capítulo anterior, é um gerenciador de pacotes. Seu objetivo é facilitar o uso de algumas bibliotecas e frameworks ligados ao NodeJS.  


Para instalar o NPM, tudo o que precisa fazer \(em linha de comando\) é rodar o seguinte comando:

```text
sudo apt-get install npm

```

Com isso, a instalação irá acontecer devidamente.  


Para inicializar o uso do NPM em uma pasta, terá que fazer:

```text
npm init
```

Logo em seguida, irá pedir que insira algumas informações, mas se deixá-las em branco \(só ir apertando a tecla Enter ou inserir -y no comando acima\), o sistema irá deixar a pasta no padrão.  


Dessa forma, o npm irá preparar sua pasta para documentar\(no package.json\) e receber as libraries do ecossistema npm.  


Para instalar algum pacote do ecossistema do NPM, a maioria dos pacotes podem ser instalados via o comando:  


```text
npm install <nome_do_pacote>
```

Caso queira instalar alguma biblioteca globalmente, então:

```text
npm install -g <nome_do_pacote>
```

Caso a biblioteca não siga esse padrão, é só procurar no site npm.org, que o comando de instalação da biblioteca estará disponível.  


As bibliotecas instaladas vão ser colocadas numa pasta chamada node\_modules, nela o npm reconhece quais as funções que podem ser utilizadas pelo node.  


Como o package.json é atualizado a cada library instalada para reconhecer as libraries que estão sendo utilizadas pelo projeto. Caso a pasta node\_modules não esteja dentro da pasta escolhida para o projeto, só precisa usar:

```text
npm install
```

Que todas as libraries marcadas no package.json serão instaladas e a pasta node\_modules será criada.

Para desinstalar algum pacote do repositório npm:

```text
npm uninstall <nome_do_pacote>
```

Com os comandos mostrados, deseja-se ter total controle dos repositórios em que se utiliza as libraries do ecossistema NPM. 

