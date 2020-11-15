---
description: 'O que são funções, como executa-las, o que são callbacks?'
---

# Funções

## O que são

A palavra função tem muitos significados na programação e ela varia um pouco dependendo do contexto ou linguagem. Para o JavaScript consideramos como função uma serie de instruções \(linhas de código\) que podem ser executadas/invocadas uma ou mais vezes e que pode receber dados de entrada \(inputs ou argumentos\) e pode dar dados de saída \(outputs ou valor de retorno\).

## Sintaxe Padrão

```javascript
function nomeDaSuaFuncao(parametro) {
    // Seu codigo
    return dadoDeRetorno;
}
```

O exemplo acima é uma **declaração** de função, ou seja somente com esse trecho de código a função não é executada, apenas se torna disponível para ser executada. A associação do identificador `nomeDaSuaFuncao` e da função em si acontece antes da execução, quando declarada desta forma.

Outra forma possível de declarar uma função:

```javascript
// Podemos usar const no lugar do let
let nomeDaSuaFuncao = function(parametro) {
    // Seu codigo
    return dadoDeRetorno;
};
```

Dessa forma a função é atribuída a variável `nomaDaSuaFuncao` em tempo de execução.

Note que as funções em JavaScript são variáveis normais e isso traz muita flexibilidade. Em muitas outras linguagens de programação, as funções são um tipo a parte, já no Javascript elas são valores como qualquer outro, ou seja, podemos reatribuir uma variável que era uma função com qualquer outro valor valido.

```javascript
let nomeDaSuaFuncao = function(parametro) {
    // Seu codigo
    return dadoDeRetorno;
};

nomeDaSuaFuncao = "Agora sou uma string";

console.log(nomeDaSuaFuncao ); // "Agora sou uma string"
```

### Executando uma função

```javascript
function testeOla() {
    console.log("Eu sou um teste!");
}

// Ao ser executada "Eu sou um teste!" será imprimido
testeOla();
```

Para executar uma função \(informalmente chamado de: _rodar_ uma função\) basta escrever seu nome e abrir e fechar parêntesis.

```javascript
function testeOla() {
    console.log("Eu sou um teste!");
}

let numeroTeste = 42;

numeroTeste(); // Uncaught TypeError: numeroTeste is not a function
```

No exemplo acima tentamos rodar uma função usando uma variável que não é uma função, essa operação da erro. Certifique-se de rodar apenas variáveis que funções no seu código.

## Valor de retorno

```javascript
teste1() // tudo certo
teste2() // Uncaught ReferenceError: teste2 is not defined

function teste1(parametro) {
    // Seu codigo
    return dadoDeRetorno;
}

let teste2 = function(parametro) {
    // Seu codigo
    return dadoDeRetorno;
};
```

No trecho acima a função `teste1` roda sem problemas, enquanto a `teste2` da erro. Essa diferença é devida a forma de declarar a função. Para a `teste1` a associação da função e seu identificador é feita antes da execução do código, enquanto para a `teste2` é feito durante a execução do código, ou seja, na linha 2, a variável `teste2` ainda não foi definida e a `teste1` sim

Esse processo é chamado de **hoisting** \(caso tenha curiosidade veja mais sobre ele [aqui](https://developer.mozilla.org/pt-BR/docs/Glossario/Hoisting)\), _\*\*_de maneira simplificada, é quando o Javascript leva algumas de suas variáveis para o topo do código para que você consiga ter acesso a elas mesmo antes da sua declaração

## Parâmetros

```javascript
function ola(nome) {
  console.log('Ola, ' + nome + '!');
}

ola("João");   // Ola João!
```

No trecho acima, `nome` é chamado de parâmetro, que atua como uma variável local que pode ser acessada de dentro da função.

Outro nome para a palavra parâmetro é argumento, os dois termos tem leve diferença, mas na pratica são usado como se fossem exatamente iguais.

Uma função pode ter nenhum, um ou mais parâmetros e seus valores são atribuídos em ordem posicional:

```javascript
function matematica(a, b, c) {
  console.log(a + 2*b + 3*c)
}

matematica(1, 2, 3); // 14
matematica(3, 2, 1); // 10
```

Funções também podem retornar um valor, usando a _keyword_ `return`:

```javascript
function ola(nome) {
  return 'Ola, ' + nome + '!';
}

let msg = ola("João");


console.log(msg);   // Ola, João!
```

Você so pode retornar um único valor em uma função com o `return`, e todo código depois dele não é executado. Se quiser retornar mais de um valor você pode usar um _objeto_ ou _array_ \(vamos explicar o que ele são posteriormente, não se preocupe!\).

Mesmo quando o `return` não é chamado explicitamente no fim de uma função, ela retorna um valor padrão, que é `undefined`

É como se o Javascript adicionasse um `return undefined;` sempre que você não coloca ele explicitamente

```javascript
// function ola(nome) {
//   console.log('Ola, ' + nome + '!');
//   return undefined;
// }

// A função abaixo e acima são equivalentes
function ola(nome) {
  console.log('Ola, ' + nome + '!');
}

let msg = ola("João"); // Ola, João!


console.log(msg); // undefined
```

## Callbacks

As referencias de funções, independente de como foram declaradas, são variáveis e por isso podem ser passadas como argumento para outras funções.

No trecho abaixo a função `rodarFuncao` recebe 3 argumentos.

Ela tenta executar o primeiro argumento como uma função, já que uma função é uma variável como qualquer outra e se ele não for uma função vai dar erro.

O segundo e terceiro argumento da função `rodarFuncao` vão ser passados como parâmetros para a função que ela executa \(o primeiro parâmetro\)

```javascript
function soma(a, b) {
  console.log('A soma é: 'a + b)
}

function rodarFuncao(fun, argA, argB) {
  fun(argA, argB)
}

rodarFuncao(soma, 10, 2) // A soma é: 12
```

`callback` é o nome de uma função que é passada como argumento para outra função De forma pratica um `callback` normalmente é usado em duas situações:

1. Quando queremos rodar uma função depois que outra coisa acabar

   ```javascript
   function lerDoDisco(nomeDoArquivo, callback) {
     // Aqui vai o codigo para ler os dados do arquivo
     callback()
   }

   function aviso() {
     console.log('Fim da leitura do disco');
   }

   // Primeiro o codigo da função roda e depois a callback roda
   lerDoDisco('t1.js', aviso); // 'Fim da leitura do disco'
   ```

2. Sempre que algo acontece \(um evento\)

   * No exemplo abaixo quando o botão é clicado a função `minhaFuncao` roda \(eventos serão explicados futuramente\)

   ```javascript
   function minhaFuncao() {
     console.log('Voce clicou no botao!');
   }

   botao.addEventListener('click', minhaFuncao);
   ```

Uma função pode receber mais um callback por parâmetro

```javascript
function lerDoDisco(nomeDoArquivo, callbackSuccesso, callbackErro) {
  // Aqui vai o codigo para ler os dados do arquivo
  if (conseguiLer) {
      callbackSuccesso()
  }
  else {
      callbackErro()
  }
}

function aviso() {
  console.log('Fim da leitura do disco');
}

// Primeiro o codigo da função roda e depois a callback roda
lerDoDisco('t1.js', aviso); // 'Fim da leitura do disco'
```

## Resumo

Neste capítulo vimos o básico de funções:

* Como declarar e rodar funções
  * Diferentes formas de declarar
* Valores de retorno
* Passando argumentos para funções
* O que são e como usar callbacks

