# Promises vs Callbacks

A função `readFile` do modulo fs \(filesytem\) lê um arquivo e retorna o conteúdo

O primeiro argumento é o caminho para o arquivo e o segundo é um **callback**

Ela so esta disponível com o node, se você não conhece o node, não se preocupe, aqui estou usando ela apenas de exemplo

```javascript
const fs = require('fs')

// Ler o conteudo do arquivo `chave-privada.txt`
fs.readFile('./chave-privada.txt', (err, data) => {
  // Quando a leitura terminar, rodar essa função aqui
  console.log(data); // a chave privada
});
```

Essa função possui uma equivalente que retorna uma promise invés de receber uma callback

```javascript
const fsPromises= require('fsPromises')

// Ler o conteudo do arquivo `chave-privada.txt`
const promessaDaLeitura = fsPromises.readFile('./chave-privada.txt');

promessaDaLeitura.then((data) => {
  // Quando a leitura terminar, rodar essa função aqui
  console.log(data); // a chave privada
});

// Tanto faz chamar o then direto da função ou depois (guardando o retorno da função em uma variavel)
// fsPromises.readFile('./chave-privada.txt').then((data) => {
//  console.log(data);
// })
```

Note que as duas formas são parecidas, nos dois casos temos uma função que roda assim que a função original terminar de executar

