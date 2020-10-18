---
description: O que são e como usar Arrow Functions
---

# Arrow Functions





### O que são Arrow functions?

_Arrow function_ é o termo dado para uma sintaxe específica de declaração de funções. Exemplo:

```javascript
// Forma usual de declarar funções
function funcaoNormal (arg1, arg2) {
    // Add Code Here
}

// Arrow function.
const arrowFunction = (arg1, arg2) => {
    // Add Code Here
}
```

A sintaxe geral de uma _Arrow Function_ é uma lista de argumentos entre parêntesis, uma flecha "=&gt;", e um bloco de código \(entre chaves\). Então, uma _Arrow Function_ que recebe dois argumentos \(nomeados "A" e "B"\), e retorna a soma deles, pode ser declarada assim: `(A, B) => { return A + B }`.

Note no bloco de código acima que, diferente da declaração usual de funções, a declaração dessa _arrow function_ começou com a declaração de uma variável, que então recebeu a função em si. Isso é porquê as _Arrow Functions_ não tem um nome, e precisão então ser guardadas em variáveis. Esse comportamento só é possível porquê, em JavaScript, funções são um tipo de valor \(como números ou strings\), que pode ser atribuído para qualquer variável \(essa propriedade também é conhecida como _Functions as First Class Citizens_\).

Como _Arrow Functions_ são apenas um tipo de função, elas podem ser chamadas da exata mesma forma que funções normais. Usando o bloco acima de exemplo, as chamadas podem ser feitas assim:

```javascript
funcaoNormal('valor1', 'valor2');

// Chamada de uma Arrow Function. Idêntica a chamada de uma função normal.
arrowFunction('valor1', 'valor2');
```

### Por que usar Arrow Functions?

#### Não usa um nome

Como _Arrow Functions_ não necessariamente precisam ser nomeadas, elas podem ser mais facilmente usadas como argumentos de outras funções. Um exemplo claro disso é com o `setTimeout`:

```javascript
// ----------------------- Declaração usual de funções -----------------------
function timeoutCallback () {
    // Code
}

setTimeout(timeoutCallback, 1000);

// ----------------------------- Arrow Function ------------------------------
setTimeout(() => {
    // Code
}, 1000);
```

Com uma _Arrow Function_, não precisamos nomear a função de callback do `setTimeout`. Assim, não "sujamos" o nosso escopo de variáveis com um nome que poderia ser evitado, e ainda conseguimos deixar o código relativo ao `setTimeout` dentro da chamada deste, potencialmente facilitando a legibilidade.

#### A Arrow Function pode ser atribuída à uma variável constante

Na declaração usual de funções, é possível "redeclarar" funções, como no seguinte exemplo:

```javascript
// Primeira declaração da função `fun`
function fun (arg) {
    return arg;
}

// Segunda declaração da função `fun`. Vai sobrescrever a primeira
function fun (arg) {
    return arg ** 2; // Operador de potênciação. É equivalente a "arg * arg"
}
```

No código acima, a função "fun" é declarada duas vezes. Quando isso acontece, o JavaScript ignora a primeira declaração, e todas as chamadas posterioes à função "fun" se referenciarão à segunda declaração. Isso se deve porquê a declaração de funções em JavaScript usa, internamente, o mesmo comportamento do `var`. O bloco acima é \(aproximadamente\) equivalente ao seguinte:

```javascript
var fun = function (arg) {
    return arg;
}

var fun = function (arg) {
    return arg ** 2;
}
```

Como no JavaScript é permitido declara a mesma variável duas vezes usando o `var`, esse código não gera erros, e a segunda declaração vai sobrescrever a primeira declaração. Muito raramente os desenvolvedores usam esse comportamento propositalmente, e ele quase sempre é a causa de um bug.

Com _Arrow Functions_, se for usado o `const` para declarar a variável que receberá a função, não será possível sobrescrever o valor antigo da função. Veja o seguinte exemplo:

```javascript
const fun = (arg) => {
    return arg;
}

// Aqui haverá um erro de syntaxe: a variável 'fun' já foi declarada.
const fun = (arg) => {
    return arg ** 2;
}
```

Assim, códigos que usam _Arrow Functions_ são ligeiramente mais seguros.

### Atalhos de Arrow Functions

Há algumas formas mais curtas de declarar algumas _Arrow Functions_ específicas.

#### Apenas um argumento

Se a sua _Arrow Function_ só recebe um argumento, pode-se emitir os parêntesis da lista de argumentos, como por exemplo:

```javascript
// Arrow function usual
const fun = (arg) => { /* code */ }

// Com parêntesis omitidos
const fun = arg => { /* code */ }
```

É sempre importante lembrar que isso só é possível se ela tiver **exatamente** um argumento. Para qualquer outro número de argumentos, são necessários parêntesis.

#### Apenas uma expressão de retorno

Se a sua _Arrow Function_ só precisa retornar uma única operação \(uma soma, subtração, ou chamada de função\), você pode emitir as chaves e o `return` do bloco, como por exemplo:

```javascript
// Arrow Function usual
const fun = (a, b) => { return a + b; }

// Arrow Function com as chaves omitidas
const fun = (a, b) => a + b
```

As duas declarações acima são equivalentes. Sempre que as chaves de uma _Arrow Function_ são omitidas, a expressão que estiver logo em seguida da flecha será o retorno da _Arrow Function_.

#### Um argumento e uma expressão

É possível misturar os dois casos anteriores, caso a sua _Arrow Function_ tenha exatamente um argumento e uma expressão de retorno, como por exemplo:

```javascript
// Arrow Function usual
const fun = (arg) => { return arg ** 2; }

// Arrow Function com parêntesis e chaves omitidas
const fun = arg => arg ** 2
```

### Por quê não usar Arrow Functions?

#### A declaração das funções não é tão clara

O maior argumento contra o uso de `Arrow Functions` se refere à legibilidade. Para muitos, a declaração de uma _Arrow Function_ não é tão evidente quanto a declaração de uma função usual. É argumentado que, como a declaração de uma _Arrow Function_ normalmente começa com a declaração de uma variável \(como "`const nomeDaFuncao =`"\), é mais difícil de separar a declaração de uma variável normal da de uma _Arrow Function_. Em contraste, quando uma linha começa com a palavra "`function`", já é evidente que estamos declarando uma função usual, o que ajuda a ler códigos muito grandes.

#### Não usa um nome

O fato de uma _Arrow Function_ não usar um nome é tanto uma vantagem quanto um perigo. Veja o seguinte exemplo:

```javascript
// OBS: A função 'fetchFromServer' não será implementada aqui, mas
// ela essencialmente só busca informações de um servidor pela internet,
// e chama a callback passada como argumento com a resposta do servidor.

setInterval(() => {
  fetchFromServer((data) => {
    setTimeout(() => {
      console.log(data.message);
    }, data.time);
  });
}, 1000);
```

Aqui fica bastante clara uma das desvantagens de não ter nome explícito para as coisas: pior legibilidade. Agora veja esse mesmo código, mas com funções nomeadas:

```javascript
function setupAlarm (data) {
    function displayAlarmMessage () {
        console.log(data.message);
    }

    setTimeout(displayAlarmMessage, data.time);
}

function checkForNewAlarms () {
    fetchFromServer(setupAlarm);
}

setInterval(checkForNewAlarms, 1000);
```

Aqui fica muito mais evidente que esse código está relacionado à alarmes, e que esses alarmes são buscados de um servidor. É claro que existem muitas maneiras de se aumentar a legibilidade de um código, mas a simples atribuição de nomes é, em geral, suficiente.

### Resumo

Nesse capítulo vimos sobre _Arrow Functions_:

* O que são
* Por que usar
* Alguns atalhos
* Vantagens
* Desvantagens

