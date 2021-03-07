# Chaining

Um dos maiores problemas com o uso de callbacks em operações assíncronas é o conhecido como **callback hell**. Ele acaba tornando seu código horizontal, dificultando a legibilidade.

```javascript
façaAlgo(function(resultado) {
  façaOutraCoisa(resultado, function(novoResultado) {
    façaOutraCoisaDiferente(novoResultado, function(resultadoFinal) {
      console.log(`Resultado final: ${resultadoFinal}`);
    }, callbackErro);
  }, callbackErro);
}, callbackErro);
```

Para contornar esse \(e outros\) problema\(s\) foram idealizadas as **Promises** que, por meio do chamado **chaining**, contornam o callback hell.

```javascript
façaAlgo()
.then(function(resultado) {
  return façaOutraCoisa(resultado);
})
.then(function(novoResultado) {
  return façaOutraCoisaDiferente(novoResultado)
})
.then(function(resultadoFinal) {
  console.log(`Resultado final: ${resultadoFinal}`);
})
.catch(callbackErro);
```

Mesmo com o exemplo acima sendo pequeno fica claro o ganho de legibilidade com o uso de chaining em promises ao inves do callback hell.

Um erro comum é tentar fazer promise chaining adicionando varios .then a uma mesma promise.

```javascript
const promise = new Promise(function(resolve, reject) {
  setTimeout(function() {
    resolve(1);
  }, 1);
});

promise.then(function(resultado) {
  consol.log(resultado); // 1
  return resultado + 1;
});

promise.then(function(resultado) {
  consol.log(resultado); // 1
  return resultado + 1;
});

promise.then(function(resultado) {
  consol.log(resultado); // 1
  return resultado + 1;
});
```

Como não esta sendo feito o chaining e sim apenas adicionando varios .then na promise acima a execução desses .then são feitas de forma independente.

Tambem é possivel retornar uma promise dentro de outra promise.

```javascript
new Promise(function(resolve, reject) {
  setTimeout(function() {
    resolve(1);
  }, 1);
}).then(function(resultado) {
  console.log(resultado); // 1

  return new Promise(function(resolve, reject) {
    return setTimeout(function() {
      resolve(resultado + 1)
    }, 1);
  });
}).then(function(resultado) {
  console.log(resultado); // 2

  return new Promise(function (resolve, reject) {
    return setTimeout(function() {
      resolve(resultado + 1), 1);
    }
  });
}).then(function(resultado) {
  console.log(resultado); // 3
});
```

