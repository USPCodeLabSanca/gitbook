---
description: >-
  Declarar Strings, Strings Multilinhas, Construção de Strings, concat vs
  template strings. Operações Básicas: length,indexOf, substring, replace, trim[
  ], charAttoUpperCase(), toLowerCase().
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

Caracteres em uma Strings são indexados a partir de 0. 

### Concatenando Strings

O operador `+` concatena duas strings:

```javascript
let name = 'maria'
let surname = 'gonçalves'


let full_name = name + " " + surname // " " espaça as palavras 

console.log(full_name) //Imprime maria gonçalves
```

É inconveniente utilizar o operador `+` para gerar strings complexas. A melhor maneira de fazer isto é utilizar **template strings.**

### Template Strings

São definidas entre **crases** **\`\`.** É possível montar strings a partir de variáveis ou retorno de expressões javascripts notadas entre `${}`: 

```javascript
let name = 'maria'
let surname = 'gonçalves'

let full_name = `${name} ${surname}`

console.log(full_name) //Imprime maria gonçalves
```

```javascript
let radius = 5
let PI = 3.14

console.log(`A área do círculo de raio ${radius} é ${PI*radius**2}`)
```

Mesmo sendo possível adicionar o retorno de qualquer expressão entre `${}`, ainda é uma boa prática armazenar cálculos em variáveis com nomes descritivos:

```javascript
let radius = 5
let PI = 3.14
let area = PI*radius**2
console.log(`A área do círculo de raio ${radius} é ${area}`)
```

### .length : Comprimento de uma string

O atributo `.length`de uma string retorna seu comprimento..

```javascript
let my_string = 'uma frase longuíssima'

console.log(my_string.length) //imprime 21 
```

É possível utilizar `length` para iterar sobre uma string em por meio de um `for` carectere a caractere: 

```javascript
let my_string = 'uma frase longuíssima'

for(let i = 0; i < my_string.length; i++){
    console.log(my_string[i])
} //Imprime 21 linhas, cada uma com um caractere da string.
```

### Imutabilidade de Strings

Ao contrário de outras linguagens, Strings são **Imutáveis** em Javascript. Isso significa que não é possível modificar um caractere específico ao acessá-lo com o operador `[ ]`. 

![&#xC9; poss&#xED;vel ler caracteres de strings, mas n&#xE3;o modificar seu conte&#xFA;do](../../.gitbook/assets/image%20%288%29.png)

A tática adotada é sempre **criar uma nova string e atribuí-la à variável desejada.** 

### replace

Substitui **a primeira ocorrência** de uma substring por outra em uma string. `my_string.replace(old_substr, new_substr)`. 

```javascript
let my_string = 'o.rato.roeu.a.roupa.do.rei.de.roma'
my_string = my_string.replace('.', ' ')
console.log(my_string)
// Retorna o rato.roeu.a.roupa.do.rei.de.roma
```

### replaceAll

Substitui **todas as ocorrências** de uma substring por outra em um string`my_string.replace_all(old_substr, new_substr)`

```javascript
let my_string = 'o.rato.roeu.a.roupa.do.rei.de.roma'
my_string = my_string.replaceAll('.', ' ')
console.log(my_string) 
// imprime o rato roeu a roupa do rei de roma
```

**IMPORTANTE**: Novas funcionalidades do javascript não são implementadas ao mesmo tempo em todos os Browsers. **replaceAll AINDA NÃO FUNCIONA EM TODOS OS NAVEGADORS!**. Em especial, versões inferiores ao 85 do google chrome não implementaram o método ainda. 

Em situações como esta, não vale a pena economizar algumas linhas de código a custo de gerar um bug que certamente afetará muitos usuários. A preferência é por código **portátil**, que funcione em diversos navegadores. 

### split e join - MANEIRA RECOMENDADA de substituir substrings

O método **split** quebra uma string em um **array**, utilizando `old_substr` como  **separador**:

```javascript
'o.rato.roeu.a.roupa.do.rei'.split('.')
// retorna ["o", "rato", "roeu", "a", "roupa"]
```

O método **join** aglutina um array de strings em uma única strings, utilizando `new_substr` como **aglutinador**

```javascript
["o", "rato", "roeu", "a", "roupa"].join(' ')
//retorna 'o rato roeu a roupa'
```

É possível utilizar os métodos separadamente, mas é comum utilizá-los um logo após o outro: 

```javascript
my_str = 'o.rato.roeu.a.roupa.do.rei'
old_substr = "."
new_substr = " " 

my_str = my_str.split(old_substr).join(new_substr)
//retorna 'o rato roeu a roupa'

```

Os métodos `split` e `join` são amplamente implementados em diversos browsers. Portanto, esta maneira deve ser priorizada. 

### indexOf

Retorna o índice da **primeira ocorrencia** de uma `substr` em `my_str`. Caso não exista ocorrência, retorna -1. 

```javascript
'Olá, mundo!'.indexOf('mu') // Retorna 5
```

### .substring e substituir caractere em um índice específico

Infelizmente, ainda não existe função nativa que permita modificar um caractere em um index especifico de uma string. A estratégia atual gerar duas substrings, uma anterior e outra posterior ao index desejado. E então concatená-las com a nova substring no meio. 

O método `.substring(start, end)` permite gerar substrings a partir de índices. 

A seleção da substring é fechada em `start` mas aberta em `end`, semelhante ao \[\) da matemática. 

```javascript
let my_str = '01234567'
my_str.substring(2, 5)
// Retorna "234"
```

Em suma, o caractere no índice inicial é incluído mas o  no índice final não.

Caso `end` não seja passada de argumento, `.substring` o setta para `my_str.length+1` . Ou seja, retorna de `start` até o final da string, incluindo o último caractere. 

```javascript
let my_str = '01234567'
my_str.substring(5)
// retorna "567"
```

A estratégia consiste em concatenar a substrings anterior ao índice, a nova substring e a substring posterior ao índice,  

```javascript
let my_str = 'abcde'
let new_substr = 'Z'
let index = 2

let substr_start = my_str.substring(0,index) // Retorna 'ab'
let substr_end = my_str.substring(index+1) // Retorna 'de'

my_str = substr_start + new_substr + substr_end
// Retorna abZde
```

### trim

Remove espaços em branco e tabulações do início e fim da string.

```javascript
let my_string = "      abcde     "
console.log(my_string) // imprime "      abcde     "
console.log(my_string.trim()) // imprime "abcde"
```

### toUpperCase e toLowerCase

Passam todos os caracteres da string para letra maiúscula `toUppercase`  ou minúscula `toLowerCase`

```javascript
let my_string = 'TEXT'
my_string.toLowerCase() // retorna 'text'
```



