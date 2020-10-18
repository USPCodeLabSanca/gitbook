# Introdução ao Javascript

## O que é Javascript?

Uma Linguagem feita originalmente para os browsers, que são **Runtine Environments \(Ambiente de execução\)**. Cada browser possui sua própria **JS Engine \(Ou interpretador javascript\)**. Não pode ter sua estrutura original modificada pois isso quebraria sites legados, mas recebe constantemente atualizações **\(ES6/ECMAscript2015\)** por instituições de padronização **\(ECMA\)**.

## Javascript Engine ou Motor Javascript

A JS engine **transforma o código .js em código de máquina e o executa**.A própria engine é quem **se comunica com a CPU** e executa o código de máquina. O processo é chamado de interpretação, logo **JS é interpretado**, o que é **diferente da compilação**, onde o compilador \(ex: GCC\) apenas compila o código para código de máquina, que deve ser executado posteriormente pelo próprio usuário.

* Exemplos de JS engines: Chackra\(Edge\) SpiderMonkey\(Firefox\) e **V8\(Google Chrome\)**

## Runtime Environment ou Ambiente de Execução

Acrescentam às engines um **ambiente com scripts, bibliotecas e APIS** úteis ao seu contexto.

* O **browser** implementa um runtime environment para **clientes**, e acrescenta por exemplo funções de **manipulação do DOM/HTML** \(`document.getElementById()`\)
* **Node** é um runtime environment para **servidores**, e acrescenta por exemplo funções de acesso aos **arquivos do sistema** \(`fs.readfile()`\)

![Runtime Environment](../../.gitbook/assets/js_intro_img1.png)

Tanto o Google Chrome quanto Node utilizam a mesma JS Engine, o V8.

## ECMA, ES6, ECMAScript2015

Sigla para European Computer Manufacturers Association. **ECMA é uma Instituição de padronização** altamente respeitada que já padronizou outras linguagens como o C\#. Lançam periodicamente novas versões do ECMAScript com **novas funcionalidades** do JS.

Versões demoram para serem implementadas nos browsers. Ferramentas como o **Babel.js transpilam código** de especificação nova para o dito **Vanila.js \(Javascript "Puro"**\).

* A **ECMAScript2015 ou ES6** é a versão que utilizaremos, por ter sido implementada na grande maioria dos browsers sem necessidade de transpilação.

![Imagem de Kostas Diakogiannis](../../.gitbook/assets/js_intro_img2.png)

![Funcionalidades mais &#xFA;teis do ES6 de acordo com 5000 programadores. Pesquisa de Nicol&#xE1;s Bevacqua](../../.gitbook/assets/js_intro_img3.png)

## Criando Código em JS

São necessários apenas um **navegador** e **editor de texto** para executar javascript.

Crie dois arquivos, um `index.html` e um `main.js`. Ao fim do `<body>` de`index.html` criar uma referência para `main.js`:

{% tabs %}
{% tab title="index.html" %}
```markup
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link rel="stylesheet" href="">
    </head>
    <body>
        <script src="main.js"></script>
    </body>
</html>
```
{% endtab %}

{% tab title="main.js" %}
```javascript
console.log('Hello World!')
```
{% endtab %}
{% endtabs %}

O código acima escreve \`Hello World!" no console do navegador.

## Console

Uma ferramenta de desenvolvimento embutida no navegador. Permite ver a saída de scripts linkados ao html ou mesmo escrever código.

* No **Google Chrome** e **Firefox**, é acessível via `Ctrl Shift I`
* Também pode ser acessado com `Right Click` -&gt; `Inspect`

![Ctrl Shift I ou Bot&#xE3;o Direito-&amp;gt;Inspecionar](../../.gitbook/assets/js_intro_img4.png)

![Aba Console das ferramentes de desenvolvedor](../../.gitbook/assets/js_intro_img_5.png)

É importante notar que a única maneira de **escrever código persistente** é utilizando arquivos `.js`. Códigos feitos a partir do console do navegador **não são salvos** em lugar algum, sendo portanto perdidos quando se encerra o browser.

### `console.log`

Imprime o resultado de uma **expressão em javascript** no console.

```javascript
console.log(3+4)            // Imprime 7
console.log("Hello World") //Imprime Hello World
```

### Declaração de variáveis: var vs let vs const

Os comandos `var`, `let` e `const` permitem declarar variáveis.

* `var`: **Legado**. Possui escopo da **função na qual foi declarada**, o que pode gerar efeitos colaterais indesejados.

  ```javascript
  function usesVar(){
    var outside_block = 1

    if (outside_block == 1){
        var inside_block = 2
    }

    console.log(inside_block)
  }
  usesVar()
  ```

  A função **funciona e imprime 2**. Na prática, o comportamento é indesejado, pois seria mais **seguro** que unidades declaradas dentro de blocos \(no caso, o **condicional if**\) existissem apenas dentro deles.

* `let`: **ES6: Melhor prática!**. Possui escopo do **bloco, instrução ou expressão** no qual foi declarada.

  ```javascript
  function usesLet(){
      let outside_block = 1

      if (outside_block == 1){
          let inside_block = 2
      }

      console.log(inside_block)
  }

  usesLet()
  ```

  lança o seguinte erro:

  ![](../../.gitbook/assets/js_intro_img6%20%281%29.png)

  Variáveis declaradas com let geram menos efeitos colaterais no código, sendo portanto recomendadas.

* `const`: **ES6: Melhor prática para valores constantes**, pois é imutável¹. Seu escopo é o mesmo de `let`.

  ```text
  let a = 'a'
  const b = 'b'
  a = 'c' // Permite mudança
  b = 'c' // TypeError: Assignment to constant variable
  ```

  ¹ \[Extra\]: const em objetos imutabiliza apenas sua referência e não conteúdo. `Object.freeze` imutabiliza um objeto, mas objetos podem tem outros objetos como atributos, o que só imutabiliza as referências dos objetos da "primeira camada". É necessário aplicar `Object.freeze`recursivamente para criar objetos verdadeiramente imutáveis. Verificar [Este artigo](https://stackoverflow.com/questions/34776846/how-to-freeze-nested-objects-in-javascript)

### Tipagem

Javascript possui tipagem **Dinâmica**:

* Não é possível declarar o tipo da variável, que é atribuído automaticamente.
* É possível modificar o tipo de uma variável.
* O comando `typeof()` permite descobrir o tipo atual.

#### Number

Armazena números, sejam eles inteiros ou floats.

```javascript
let inteiro = 3
let float = 3.5

console.log(typeof(inteiro), typeof(float)) //number number
```

#### Strings

Armazenam qualquer text entre parênteses simples ou duplos.

```javascript
let my_string = 'olá mundo'
console.log(typeof(my_string)) //string
```

Confira a aula 2 \(Strings\) para maiores informações sobre o tema.

#### Boolean

Armazena veracidade de expressões, que pode ser:

* `true`, equivalente a **1**
* `false`, equivalente a **0**

```javascript
let verdadeiro = true
console.log(verdadeiro, typeof(verdadeiro)) //true "boolean"
```

São normalmente utilizadas em conjunto a outros operadores lógicos:

* `!` representa NOT
* `&&` representa AND
* `||` representa OR

![Tabela de opera&#xE7;&#xF5;es l&#xF3;gicas](../../.gitbook/assets/js_intro_img6.png)

```javascript
let verdadeiro = true
let falso = false

console.log('!v', !verdadeiro)
console.log('!f', !falso)

console.log('v&&v: ', verdadeiro && verdadeiro)
console.log('v&&f: ',verdadeiro && falso)
console.log('f&&f: ', falso && falso)

console.log('v||v: ', verdadeiro || verdadeiro)
console.log('v||f: ',verdadeiro || falso)
console.log('f||f: ', falso || falso)
```

imprime

```java
!v false
!f true

v&&v:  true
v&&f:  false
f&&f:  false

v||v:  true
v||f:  true
f||f:  false
```

#### Verificação de igualdade

* `==` Verifica se operandos tem o mesmo valor, independente do tipo.
* `===` Verifica se operandos tem o mesmo valor e tipo.

```javascript
console.log(1 == '1')      //true
console.log(1 === '1')     //false
console.log(1 === 1)       //true

console.log(true == 1)     //true
console.log(true === 1)    //false
console.log(true === true) //true
```

#### undefined vs null

**undefined** Representa o acesso a uma variável existente mas não inicializada.

```javascript
let nao_inicializada
console.log(nao_inicializada, typeof(nao_inicializada)) // undefined undefined
```

Já **null NÃO É TIPO!** é apenas o estado de um objeto que propositalmente não tem conteúdo.

```javascript
a = null
console.log(a, typeof(a))//null object
```

**Tudo em JS que não é um dos tipos primitivos acima listados é objeto. Isto será estudado mais a frente.**

