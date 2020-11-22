---
description: >-
  Declarar Strings, Strings Multilinhas, Construção de Strings, concat vs
  template strings, Operações Básicas: lengthindexOf, substring, replace, trim[
  ], charAttoUpperCase(), toLowerCase(). Comparação
---

# Strings

### O que são Strings

Strings representam um texto qualquer. Em Javascript strings são um tipo, e não possuem tamanho pré definido. Além disso, não é necessário alocar memória para criar uma String, isso é feito automaticamente ao declará-la. 

### Declarando uma String

Strings são declaradas entre aspas simples `''` ou duplas `" "`:

```javascript
let my_string = "Exemplo de string "
let other_string = 'Outro exemplo'
```

Não há regra para utilizar uma ou outra. No geral, Strings de aspas simples deixam o código menos poluído. Entretanto, aspas duplas são mais práticas para texto em inglês, no qual a contração de `is`, `'s`, requer aspas simples, o que quebraria Strings abertas por aspas simples.

```javascript
let text = "it's a good idea to use double quotes for english text."
```

### Acessar caracteres de Strings

É possível acessar caracteres de strings utilizando o operador `[]`

```javascript
let my_string = 'abcde'
console.log(my_string[2]) //Imprime C
```

Caracteres em uma Strings são indexados do 0. 

### Imutabilidade de Strings

Ao contrário de outras linguagens, Strings são **Imutáveis** em Javascript. Isso significa que mesmo sendo possível acessar a terceira letra de uma string com `[2]`, o valor pode ser apenas lido, **não sendo possível modificá-lo**. 

![&#xC9; poss&#xED;vel acessar posi&#xE7;&#xF5;es de strings, mas n&#xE3;o modificar seu conte&#xFA;do](../../.gitbook/assets/image%20%288%29.png)



