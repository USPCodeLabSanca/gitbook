---
description: Tratamento de erros usando try/catch.
---

# Tratamento de erros

Executando códigos em Javascript é possível acontecer um erro aqui e ali, eles podem ter acontecidos por funções que retornam `throw`, erros na sintaxe do código, etc.

O tratamento de erros no código é importante para impedir que a execução do código seja interrompida. Para imaginar a importância pense em um servidor que trata os logins de um serviço grande como a Netflix, se com um erro o serviço todo parasse iria demorar vários minutos até que o servidor ligasse novamente e essa interrupção poderia ser evitada com o tratamento de erros.

## Situações de usos mais comum

Em algumas situações é bastante comum ter que tratar os erros, dado que podem ocorrer em uma alta frequência.

### Requisições e async/await

Em requisições usando a função `fetch(URL)` podemos tratar o erro diretamente com o bloco `try/catch` e posteriormente retornar o nosso valor desejado. Segue o exemplo:

```javascript
function fazRequisicao(algumaCoisa) {
    let req = fetch(`API.URL/BLA/${algumaCoisa}`);
    
    return req;
}

async function trataOErroERequisita(algumaCoisa) {
    try {
        return await fazRequisicao(algumaCoisa);
    } catch {
        return {"status": "notOk"};
    }
}

async function teste() {
    let valorEncontrado = await trataOErroERequisita("teste");
    
    console.log(valorEncontrado);
}
```

Verifique que a primeira função `fazRequisicao`, vai ser responsável por usar a função `fetch` na API e retornar uma `promise` com a resposta, caso acontença um erro no `fetch`, iremos tratar ele e retornar um objeto em que podemos utilizar no nosso código.

### NaN

??

## try e catch

Em javascript é possível evitar erros atráves da utilização do bloco:

```javascript
try {
    // Colocamos o nosso código aqui
    // Esse código pode gerar algum erro
} catch (error) {
    // Caso tenha acontecido algum erro a execução do código pula para aqui
}
```

No código acima podemos perceber dois blocos diferentes:

* Dentro do `try` podemos colocar o nosso código e esse código pode gerar algum erro ou ter a sua execução sem erros.
* No bloco `catch` podemos detectar o erro a partir do seu primeiro parâmetro \(`error`\), a execução do código pula para o `catch` assim que um erro acontece.

O parâmetro `error` dentro do `catch` vai ter a seguinte definição:

```javascript
{
    "name": String,
    "message": String
}
```

* **name:** string com o nome do erro.
* **message:** string representando a descrição do erro.

### Exemplo

Para demonstrar a utilização do bloco o seguinte código sera usado:

```javascript
let num = 1;

try {
    num.toUpperCase(); // Tenta converter um número para letras máisculas
    console.log("A exeucção do código parou no erro.");
} catch (error) {
    // Exibe o nome e a mensagem do erro no console
    console.log(`Nome do erro: ${error.name}, descrição: ${error.message}`)
}
```

Como não podemos converter um número para letras maiúsculas \(só seria possível se a variável `num` fosse uma string\) o `TypeError` é gerado, logo a execução do código parou no erro e o console retornou:

{% hint style="info" %}
**Retorno do console:**

Nome do erro: TypeError, descrição: num.toUpperCase is not a function
{% endhint %}

### catch sem o parâmetro

É possível utilizar o bloco try/catch sem precisar colocar um parâmetro no catch, caso não seja necesário utilizar o erro. Segue o exemplo:

```javascript
try {
    fazAlgumaCoisa();
} catch {
    fazOutraCoisa(); // Sem usar o parâmetro error
}
```

## finally

Além do `try`  e `catch`, também existe o bloco `finally`, ele é executando após a execução do `try/catch` mesmo que um erro não tenha acontecido, segue o exemplo:

```javascript
try {
    // Executa um código que talvez cause um error
} catch (error) {
    // Trata o erro
} finally {
    // Se acontecer o erro a ordem de execução dos blocos é dada por:
    // try -> catch -> finally
    // Se não acontecer erros a ordem é:
    // try -> finally
}
```

Como no exemplo inicial do servidor de login da Netflix, agora o servidor pode tentar fazer o login e em caso de erro tratar ele, até que posteriormente ele pode finalizar o login e logar o usuário no site.

## throw

Além de tratar erros, também é possível gerar erros customizados no código a partir throw. Diferentemente do erro normal do JavaScript o `throw` pode ser customizado para diferentes tipos e ter as próprias propriedades, como:

```javascript
throw "Erro #1"; // O argumento error do catch se torna uma string
throw 404; // O argumento error do catch se torna um número

// Podemos retornar um objeto que se assimila ao erro padrão do JavaScript
throw {
    "name": "Erro #2",
    "message": "Descrição do erro #2"
};

// Também é possível retornar instância de objetos
throw new ErrorClass("Nome do error");

// Funções também podem ser retornadas
throw function() { /* Faz alguma coisa */ };
```

Com o `throw` é possível flexibilizar o tratamento de erros no código e ter mais controle no comportamento do código.

