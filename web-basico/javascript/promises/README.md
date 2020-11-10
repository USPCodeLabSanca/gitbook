# Promises

Promises \(Promessas\) é um tópico muito importante e que causa muita confusão.

De forma bem simplificada, quando uma função demora um tempo indeterminado para ser concluída, invés dela parar a execução do seu código, ela retorna uma promessa de que ela vai acabar de executar e te retornar o valor que você quer usar.

Uma função que retorna uma promessa invés de esperar até a função terminar é chamada de assíncrona, já que ela não trava a execução do código.

As promises são uma alternativa aos callbacks que vimos no capitulo de Funções

Vamos ver um trecho em pseudo código para tentar exemplificar a situação

```javascript
// Quando a funcao terminar será retornado a o tempo estimado para entrega em minutos
const promesaDoPedido = fazerPedidoNoiFood('marmita media');

// O codigo aqui pode ser executado antes da confirmação do pedido

// Estou esperando o restaurante confirmar o pedido
while (true) {
    if (promessaDoPedido.terminou) {
        console.log(promessaDaBusca.tempoEstimadoEntrega); // 21
        break;
    }
}
```

Lembrando que o trecho assíncrono não é javascript, esta em pseudocódigo apenas para exemplificar o funcionamento de uma promise

Uma versão síncrona do mesmo código, ou seja, que a função vai travar seu código até que ela termine de executar:

```javascript
let tempoEstimadoEntrega = fazerPedidoNoiFoodSincrono();

// Pedido confirmado
console.log(tempoEstimadoEntrega); // 19
```

Para fazer a versão assíncrona em Javascript nos usamos o método `then` da promise, ele recebe um argumento, que é uma função que sera executada quando a promessa terminar \(um callback\)

```javascript
// Aqui a promessa é criada
const promesaDoPedido = fazerPedidoNoiFood()

// Aqui estamos passando uma função (callback) que vai rodar quando a promesa terminar
promesaDoPedido.then((tempoEstimadoEntrega) => {
    // O codigo aqui é executado quando a função do pedido termina
    // O argumento do callback da funcao then, é o valor que a promessa retornou
    console.log('A funcao do pedido terminou!');
    console.log(tempoEstimadoEntrega); // 15
});

// O codigo aqui roda mesmo sem a função acima ter terminado
console.log('O pedido foi deito!');
console.log('Aguardando confirmação');
```

Até aqui não parece muito diferente do que vimos sobre callbacks, mas ainda vamos ver outras formas de lidar com promises que deixam o código mais limpo e legível

