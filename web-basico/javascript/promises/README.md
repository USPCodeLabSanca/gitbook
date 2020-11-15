# Promises

Promises \(Promessas\) é um tópico muito importante e que causa muita confusão.

De forma bem simplificada, quando uma função demora um tempo indeterminado para ser concluída, invés dela parar a execução do seu código, ela retorna uma promessa de que ela vai acabar de executar e te retornar o valor que você quer usar.

Uma função que retorna uma promessa invés de esperar até a função terminar é chamada de assíncrona, já que ela não trava a execução do código

Vamos ver um trecho em pseudo código para tentar exemplificar a situação

Você chama uma função que faz procura um motorista para uma viagem \(Uber ou 99 por exemplo\), e essa função demora um tempo **indeterminado** para terminar de rodar, da pra encontrar um motorista em alguns segundos, ou até levar vários minutos

```javascript
// Quando a funcao terminar será retornado um objeto com informacoes do motorista
const promesaDaViagem = buscarMotorista(meuEndereco, enderecoDestino);

// O codigo aqui pode ser executado antes da confirmação da viagem

// Estou esperando um motorista ser encontrado
while (true) {
    if (promessaDaViagem.terminou) {
        console.log(promessaDaViagem.nome); // José
        break;
    }
}

// Fim
```

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

Lembrando que o trecho acime não é javascript, esta em pseudocódigo apenas para exemplificar o funcionamento de uma promise

Uma versão síncrona do mesmo código, ou seja, que cada linha espera a anterior terminar antes de continuar

```javascript
let motorista = buscarMotoristaSincronamente();

// Viagem confirmada
console.log(motorista.nome); // João
```

```javascript
let itensDaBusca = buscarComidaNoMercadoSincronamente();

// Ja sai e voltei com a comida!

console.log(itensDaBusca); // 2
```

Lembrando que o trecho assíncrono não é javascript, feito só para exemplificar

A função que é passada como primeiro argumento na função `then` recebe um argumento que é o valor que a promise retorna quando termina de executar

```javascript
// Aqui a promessa é criada
const promesaDaViagem = buscarMotorista()

// Aqui estamos passando uma função (callback) que vai rodar quando a promesa terminar
promesaDaViagem.then((motorista) => {
    // O codigo aqui é executado quando a função encontrar um motorista
    // O argumento do callback da funcao then, é o valor que a promessa retornou 
        // Nesse caso, o objeto com as informações do motorista
    console.log('A funcao da viagem terminou!');
    console.log(motorista.nome); // Maria
});

// O codigo aqui roda mesmo sem a função acima ter terminado
console.log('Procurando motorista');
console.log('Aguardando confirmação da viagem');
```

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

