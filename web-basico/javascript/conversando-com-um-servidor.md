---
description: Como fazer requisições HTTP usando um comando simples?
---

# Conversando com um servidor

## A função fetch

Há infinitas maneiras de fazer requisições HTTP em Javascript. Neste capítulo mostraremos uma das maneiras mais simples de se fazer isso.

Para tal, iremos utilizar a função `fetch`. Essa função faz requisições, de qualquer método HTTP, e retorna uma promise com a qual teremos que lidar.

### Definição da função

A função `fetch` vai aceitar um ou dois parâmetros como entrada, ela tem a seguinte cara:

```javascript
fetch("URL");

fetch("URL", options); // Options é um objeto
```

* No primeiro formato a função vai fazer requisição ao servidor utilizando o método `GET` \(é como se a função entrasse na página web igual um usuário normal\).
* No segundo formato é possível especificar diferentes configurações, como o método \(GET, PUT, POST, etc\), headers, mode e outros que é possível encontrar em: [https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch)

## Exemplo

Neste exemplo iremos consumir imagens de uma API pública disponível na seguinte URL: [https://jsonplaceholder.typicode.com](https://jsonplaceholder.typicode.com).

Primeiramente, iremos criar uma função:

{% tabs %}
{% tab title="example.html" %}
```markup
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Exemplo</title>
</head>
<body>
    <h1> Belo Exemplo </h1>
    <script src="example.js"></script>
</body>
</html>
```
{% endtab %}

{% tab title="example.js" %}
```javascript
// Cria uma constante para a URL 
// em que iremos realizar a requisição.
const URL = 'https://jsonplaceholder.typicode.com'

const getPhotos = async () => {
    const response = await fetch(`${URL}/photos`)
    return response.json()
}
```
{% endtab %}
{% endtabs %}

Após isso, iremos adicionar uma resposta para lidar com a promise da função `getPhotos()`:

```javascript
getPhotos()
.then((res) => {
    let body = document.getElementsByTagName('body')[0]

    for (let i = 0; i < 150; i++) {
       let img = document.createElement('img')
       img.src = res[i].url
       img.width = 300
       img.height = 300
       body.appendChild(img)
   }
})


```

Com isso, teremos um resultado parecido com isto:

![Resultado do exemplo](../../.gitbook/assets/example01.png)

Dessa forma, e com as dicas dadas, você poderá realizar qualquer requisição HTTP de forma simples.

