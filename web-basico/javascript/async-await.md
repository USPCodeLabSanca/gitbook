---
description: O que fazer para evitar o callback hell e o chaining de promises?
---

# Async/Await

No capítulo de promises, foi mostrado como uma promise funciona:

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

No exemplo acima, só há uma promise \(marcado pelo ".then"\), mas e se precisássemos utilizar a variável data em uma outra próxima promise?

Isso criaria um encadeamento de promises uma dentro da outra, e, no final, teríamos infinitas promises uma dentro da outra.

Algo como:

```javascript
f1.then((data1) => {
    f2(data1).then((data2) => {
        f3.then((data3) => {
            console.log(data3)
            //podendo continuar indefinidamente
        })
    })
})
```

Para o código acima, dá-se o nome de **callback hell**.

E como podemos evitar isso? Usando **async/await**!

O que acontece com uma função marcada com async/await é que ela espera a promise ser terminada antes de continuar o código, exatamente como o .then, mas sem entrar nos problemas de chaining.

A única coisa que precisamos fazer é o seguinte:

```javascript
const functionOne = async () => {
    const resultado = await functionTwo();
    const resultado2 = await functionThree(resultado) 
    
    console.log(resultado2)
}
```

Nesse exemplo, a função _functionOne_ foi marcada para ser uma função "async" \(assíncrona\), e, dessa forma, qualquer função chamada com o "await" dentro dela irá fazer com que a _functionOne_ espere \(tradução de _await_\) até que essa outra função \(por exemplo, a _functionTwo_\) termine sua operação assíncrona e retorne seu valor final para que a função-pai \(_functionOne_\) continue a sua execução. 

Então se, por exemplo, a _functionTwo_ for uma função que lê um determinado arquivo, a _functionOne_ irá ficar parando naquela linha, esperando até que a _functionTwo_ termine a sua execução e retorne o que tiver de retornar.

