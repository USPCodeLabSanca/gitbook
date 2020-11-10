# Promises

Promises \(Promessas\) é um tópico muito importante e que causa muita confusão.

De forma bem simplificada, quando uma função demora um tempo indeterminado para ser concluída, invés dela parar a execução do seu código, ela retorna uma promessa de que ela vai acabar de executar e te retornar o valor que você quer usar.

Uma função que retorna uma promessa invés de esperar até a função terminar é chamada de assíncrona, já que ela não trava a execução do código.

São uma alternativa em relação aos \[callbacks\]\([https://uclsanca.gitbook.io/learn/web-basico/javascript/funcoes\#callbacks](https://uclsanca.gitbook.io/learn/web-basico/javascript/funcoes#callbacks)\) que vimos no capitulo de \[Funções\]\([https://uclsanca.gitbook.io/learn/web-basico/javascript/funcoes](https://uclsanca.gitbook.io/learn/web-basico/javascript/funcoes#callbacks)\)

Vamos ver um trecho em pseudo código para tentar exemplificar a situação

```javascript
// Quando a funcao terminar de buscar, ela retorna o numero de itens que foram buscados
let promesaDaBusca = buscarComidaNoMercadoAssincronamente();

// Ja sai para buscar comida, mas ainda nao acabei;

// O codigo aqui pode ser executado antes da busca terminar

while (true) {
    if (promessaDaBusca.terminou) {
        console.log(promessaDaBusca.itens); // 2
        break;
    }
}
```

Uma versão síncrona do mesmo código, ou seja, que cada linha espera a anterior terminar antes de continuar

```javascript
let itensDaBusca = buscarComidaNoMercadoSincronamente();

// Ja sai e voltei com a comida!

console.log(itensDaBusca); // 2
```

Lembrando que o trecho assíncrono não é javascript, feito só para exemplificar

Para fazer algo parecido em Javascript nos usamos o método `then` da Promise, ele recebe um argumento, que é uma função que sera executada quando a promessa terminar

```javascript
buscarComidaNoMercadoAssincronamente().then((itens) => {
    // O codigo aqui é executado quando a a função da busca termina
    // O argumento do callback da funcao then, é o valor que a promessa retornou
    console.log('A busca terminou!');
    console.log(itens); // 2
});

// O codigo aqui roda mesmo sem a função acima ter terminado
console.log('A busca comecou!')
```

