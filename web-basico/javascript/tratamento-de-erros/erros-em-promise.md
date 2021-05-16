# Erros em Promises

Promises, além de bonitas, também tornam o tratamento de erros elegante ao utilizar o método `catch`.

### .catch\(\)

Imagine que você está usando o método `.fetch()` de uma biblioteca que faz o `GET` para pegar o HTML de uma página. Esse método retorna uma promise e é possível que ela seja rejeitada caso aconteça um erro \(como não encontrar a página web por problemas de conexão etc\).

Segue um código de exemplo:

```javascript
someLib.fetch("https://url.com").then((html) => console.log(html))
```

Se deixarmos o código assim, podemos ter o seguinte erro:

```text
Uncaught (in promise) [Mensagem do erro]
```

O `Uncaught (in promise)` acontece quando a promise é rejeitada \(ou é dado um throw\), ou seja, aconteceu um erro e não lidamos com ele.

O método `.catch()` vai servir justamente para isso. O código abaixo mostra a sua utilização:

```javascript
someLib.fetch("https://url.com")
    .then((html) => console.log(html))
    .catch((error) => {
        console.log(`Erro! Informações: ${error}`)
    })
```

#### Encadeamento com o catch

O `catch`pode lidar com erros de múltiplas promises:

```javascript
someLib.fetch("https://url.com")
    .then(return something)
    .then(return somethingAgain)
    .catch(error => console.log(error))
```

Nesse caso, a promise vai lidar com qualquer erro que aconteça dentro do `fetch` ou do primeiro/segundo `then`.

Se fizermos outro `then`, vai ser necessário um `catch`logo após para lidar com o erro, como no exemplo abaixo:

```javascript
someLib.fetch("https://url.com")
    .then(return something)
    .then(return somethingAgain)
    .catch(error => console.log(error) // Lida com qualquer erro do fetch ou do primeiro/segundo then
    .then(return anotherSometing)      // O catch de cima não pode lidar com o erro desse then
    .catch((error) => console.log(error)) // Lida com erro do then de cima
```

