# Erros em promise

Promise além de bonitas, também tornam o tratamento de erros em um formato elegante, usando o seu método `catch`.

### .catch\(\)

Imagine que você está usando o método `.fetch` de uma biblioteca que faz o `GET` para pegar o html de uma página, esse método ele retorna uma promise e é possível que a promise seja rejeitada caso aconteça um erro \(como não encontrar a página web por problemas de conexão, etc\).

Segue um código de exemplo:

```javascript
.fetch("https://url.com").then((html) => console.log(html))
```

Se deixarmos o código assim, podemos ter o seguinte erro:

```text
Uncaught (in promise) [Mensagem do erro]
```

O `Uncaught (in promise)` acontece quando a promise é rejeitada \(ou é dado um throw\), ou seja, aconteceu um erro e não lidarmos com ele.

O metodo `.catch()` vai servir justamente para isso. O código abaixo mostra a sua utilização:

```javascript
.fetch("https://url.com")
    .then((html) => console.log(html))
    .catch((error) => {
        console.log(`Erro! Informações: ${error}`)
    })
```

#### Encadeamento com o catch

O catch pode lidar com erros de múltiplas promises:

```javascript
.fetch("https://url.com")
    .then(return something)
    .then(return somethingAgain)
    .catch(error => console.log(error))
```

Nesse caso a promise vai lidar com qualquer erro que aconteça dentro de `fetch`, ou do primeiro, ou do segundo `then`.

Se fizermos outro then, vai ser necessário um catch logo após para lidar com o erro, como no exemplo&gt;

```javascript
.fetch("https://url.com")
    .then(return something)
    .then(return somethingAgain)
    .catch(error => console.log(error) // Lida com o erro de fetch, o primeiro e segundo then
    .then(return anotherSometing)      // O catch de cima não pode lidar com o erro desse then
    .catch((error) => console.log(error)) // Lida com erro do then de cima
```

