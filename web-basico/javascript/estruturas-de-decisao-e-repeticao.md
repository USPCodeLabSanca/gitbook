---
description: 'If, else'
---

# Estruturas de Decisão

Permitem implementar uma **condição lógica** que define se um **bloco de código** será executado ou não.

```javascript
estrutura_de_decisão(condicao){
    bloco de código
}
```

* **estrutura de decisão**: Pode ser `if`, `else if` ou `else`
* **condição**: Qualquer expressão em javascript que retorne `true` ou `false`
* **bloco de código**: definido entre **chaves `{}`**. É executado somente se **condição** for verdadeira.

### if

Inicia uma **cadeia independente** de estruturas de decisão. É **Obrigatório** e **único** por cadeia.

Exemplo 1:

```javascript
condicao = true
if(condicao){ // Condição Verdadeira
    console.log('A condição é verdadeira') //Imprime 'A condição é verdadeira'
}
```

Exemplo 2:

```javascript
condicao = false
if(condicao){ // Condição falsa. Bloco não é executado. 
    console.log('A condição é verdadeira')
}
```

Exemplo 3:

```javascript
let temperatura = 18

if(temperatura <= 15){ //Condição falsa. Bloco não é executado. 
    console.log('Está muito frio') 
}
```

## else if

Dá continuidade a uma cadeia de decisão. É **opcional** e é possível definir inúmeras condições adicionais utilizando `else if`.

A condição do `else if` só é testada caso a condição do `if` inicial e de todos os `else if` anteriores sejam falsas. Uma condição `else if` verdadeira executa seu código de bloco, e **impede a tentativa de verificação de `else if`s posteriores**.

Portanto, a **condição** de um `else if` só é testada se:

* 1: `if` possui condição falsa
* 2: **Todos** os `else if` antes do atual possuem condição falsa.

Além disso, assim como o `if`, o **bloco de código** de um `else if` só é executado se:

* 3: A **condição** do `else if` é verdadeira. 

Exemplo 5:

```javascript
let temperatura = 18

if(temperatura <= 15){ // Condição falsa. Bloco não é executado
    console.log('Está muito frio')
}
else if(temperatura < 25){ // Condição verdadeira. 
    console.log('Clima perfeito!') //imprime "Clima perfeito!"
}
```

É possível definir **diversos `else if` para um mesmo `if`**:

```javascript
if(condição_1){ //Sempre testado
    //bloco 1
    //executado se condição_1 for true
}
else if(condição_2){ //Só é testado se if for falso
    //bloco 2
    //executado se condição_1 for false e condição_2 true
}
else if(condição_3) //Só é testado se todos else ifs anteriores forem falsos
    //bloco 3
    //executado se condição_1 for false, condição_2 for false e condição_3 true
}
```

É importante estar ciente de que:

* É necessário um `if` para que um `else if` seja definido. Não existe `else if` "solto" no código. 
* É perfeitamente possível que nenhum `else if` do bloco condicional rode, caso a condição de `if` e de todos os `else if` sejam falsas. 
* A "testagem" das condições de `else if` é **sequencial** e **nunca "anda para trás""** \(não é retroativa\). Ou seja:

  ```javascript
  if(c0){}
  else if(){c1} // 1 
  else if(){c2} // 2
  else if(){c3} // 3
  else if(){c4} // 4
  ```

  * `c4` só será testado depois que, **nesta ordem**, `c0`, `c1`, `c2` e `c3` tenham sido testados e falsos. 
  * Todas as condições são checadadas **apenas uma única vez**. `c4` **não** faz com que `c3` seja testada de novo, isto teria custo computacional absurdo. Se é necessário que `c3` seja testada inúmeras vezes, será necessário utilizar vários blocos condicionais iniciados por `if`, ou utilizar uma **estrutura de repetição**. 

## else

Encerra uma cadeia de decisão. É **opcional** e **única**, impedindo a inserção de novos `else if` ou mesmo outros `else` posteriores.

`else` **sempre executa** quando se chega ao final do bloco de repetição, ou seja, se **foram testados todos os `if` e `else if` mas nenhuma das condições foi verdadeira**.

```javascript
if(c1){ //Sempre testado uma única vez
    //executado se c1 for true
}
else if(c2){ //Só é testado se if for falso
    //executado se c1 for false e c2 true
}
else if(c3) //Só é testado se todos else ifs anteriores forem falsos
    //executado se c1 == false, c2 == false e c3 == true
}
else{ //Só é testado se todos else ifs anteriores forem falsos E mata o bloco condicional. 

}
```

Exemplo 6:

```javascript
let temperatura = 40

if(temperatura <= 15){ // Condição falsa. Bloco não é executado
    console.log('Está muito frio')
}
else if(temperatura < 25){ // Condição falsa. Bloco não é executado
    console.log('Clima perfeito!')
}
else{ //
    console.log('Está muito quente!')
}
```

A diferença de um `else if` e um `else` é que o segundo definitivamente termina o bloco de decisão. Além disso, ao contrário de `if` e `else if`, `else` **não possui condição**, pois sua condição intrínseca é todas as anteriores terem falhado \(o que é sua grande utilidade!: A condição do else é **a negação do conjunto das condições anteriores**\).

