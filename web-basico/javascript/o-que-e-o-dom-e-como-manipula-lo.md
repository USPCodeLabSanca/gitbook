# O que é o DOM e como manipulá-lo

## O que é DOM?

O DOM \(Document Object Model\) é uma interface API para as páginas web. Ele permite que o programador possa:

* Adicionar, alterar e remove elementos HTML, como pegar uma div específica pela sua id.
* Adicionar, alterar e remover atributos e estilos \(CSS\) dos elementos HTML, como alterar o text-color de algum h1.
* Adicionar, alterar e remover eventos e interagir com esses eventos. Um exemplo de evento é o "onClick", ele acontece quando o clique do mouse acontece em algum elemento do HTML.

## Como referenciar elementos do DOM

Esta seção apresentará como encontrar elementos de uma página web com o JavaScript, é possível procurar os elementos pelas suas tags, ids, classes. Ainda é possível alterar as propriedades dos elementos, como seu estilo, seu texto e até seu HTML.

### document.getElementById

Uma das formas mais utilizadas para se acessar um elemento do HTML da página é usando `document.getElementById(id)`.

O seu parâmetro "id" é uma String, nessa string deve ser colocada a id do element HTML que se deseja buscar. Caso esteja definido na página o método retorna o elemento, caso contrário retorna NULL.

{% hint style="warning" %}
O parâmetro **“id” é case-sentive**, ou seja, para ele é importante se as letras são maiúsculas ou minúsculas, logo um “id” como `"algumaid"` difere de `"algumaID"`.
{% endhint %}

{% tabs %}
{% tab title="HTML" %}
```markup
<!DOCTYPE html>
<html>
    <head>
        <title>Minha página</title>
    </head>
    <body>
    <p id="algumaID">
        Um texto bonito aqui.
    </p>
    <p id="teste">
        Essa div vai ser alterada...
    </p>
    <script>
        // Disponível na aba "Javascript"
    </script>
    </body>
</html>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
var elemento = document.getElementById("algumaID");

document.getElementById("teste").innerHTML = "O texto do elemento com id = intro, é: " + elemento.innerHTML;
```
{% endtab %}
{% endtabs %}

### document.getElementByClassName

Outra forma de procurar elementos é utilizando o `document.getElementByClassName(nome)`, essa função quando utilizada retorna todos os elementos que encontrar que tiver as classes que estiverem no parâmetro nome.

{% hint style="info" %}
O parâmetro nome vai ser utilizado para pesquisar as classes da seguinte forma:

* `document.getElementByClassName("azul")`: vai procurar elementos que contenham a classe azul.
* `document.getElementByClassName("azul verde")`: vai procurar elementos que contenham a classe azul e verde.
{% endhint %}

{% tabs %}
{% tab title="HTML" %}
```markup
<!DOCTYPE html>
<html>
    <head>
        <title>Minha página</title>
    </head>
    <body>
    <p class="azul">
        Uma div azul.
    </p>
    <p class="azul verde">
        Uma com tons de azul e verde.
    </p>
    <script>
        // Disponível na aba "Javascript"
    </script>
    </body>
</html>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
var elementos = document.getElementByClassName("azul");

for (let elemento in elementos) {
    console.log(`Foi encontrado o elemento com id ${elemento.id} com a classe especificada`)
}
```
{% endtab %}
{% endtabs %}

Você pode ter observado que a função `document.getElementByClassName` retorna vários elementos da página web, podemos usar essa mesma função em um elemento em si:

* Utilizando a `document.getElementById("algumaID")` retornamos apenas um elemento da página web com a id "algumaID".
* Dentro desse elemento podemos querer encontrar elementos com a classe "algumaClasse".
* Observe o exemplo abaixo:

{% tabs %}
{% tab title="HTML" %}
```markup
<!DOCTYPE html>
<html>
    <head>
        <title>Minha página</title>
    </head>
    <body>
    <p id="algumaID">
        <span class="algumaClasse">Elemento 1</span>
        <span class="algumaClasse">Elemento 2</span>
    </p>
    <script>
        // Disponível na aba "Javascript"
    </script>
    </body>
</html>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
var elementos = document.getElementById("algumaID").getElementByClassName("algumaClasse");

for (let elemento in elementos) {
    console.log(`Foi encontrado o elemento com o texto ${elemento.innerText} com a classe especificada`)
}
```
{% endtab %}
{% endtabs %}

### document.getElementsByTagName

Bem parecido como a função `getElementsByClassName(nome)`, a `getElementsByTagName(nome)` vai procurar elementos na página web a partir do nome da sua tag.

{% tabs %}
{% tab title="HTML" %}
```markup
<!DOCTYPE html>
<html>
    <head>
        <title>Minha página</title>
    </head>
    <body>
    <p id="algumaID">
        <span class="algumaClasse">Elemento 1</span>
        <span class="algumaClasse">Elemento 2</span>
    </p>
    <script>
        // Disponível na aba "Javascript"
    </script>
    </body>
</html>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
var elementos = document.getElementsByTagName("p"); // Vamos procurar os elementos que possuem a tag <p></p>

for (let elemento in elementos) {
    console.log(`Foi encontrado o elemento com o texto ${elemento.innerText} com a tag especificada`)
}

// Também podemos usar o getElementById
var elementos = document.getElementById("algumaID").getElementsByTagName("span"); // Vamos procurar os elementos que possuem a tag <span></span>

for (let elemento in elementos) {
    console.log(`Foi encontrado o elemento com o texto ${elemento.innerText} com a tag especificada`)
}
```
{% endtab %}
{% endtabs %}

### document.querySelector e document.querySelectorAll

Uma forma fácil de procurar elementos com uma diversidade de tags, classes e id é usando o `document.querySelector(seletores)`, nessa função podemos encontrar um elemento de acordo com seletores CSS, logo podemos em uma mesma função procurar um elemento com uma tag específica e classe específica, entre outras formas.

```javascript
var elemento = document.querySelector("tag.classe"); // Nesse exemplo procuramoos o primeiro elemento com a <tag></tag> especifica e que possua a #classe especificada
```

Podemos usar qualquer seletor CSS na string seletores, utilizando o `document.querySelector`, teremos apenas um elemento retornado, caso queira retornar todos os elementos com os seletores utilizados existe a função `document.querySelectorAll` que retorna todos os elementos que tiver os seletores CSS dentro do parâmetro da função.

## Acessar e Alterar propriedades de elementos do DOM

Agora que você já sabe como procurar por um elemento em uma página HTML utilizando Javascript, é importante aprender como modificar as propriedades desse elemento, como:

* O texto do elemento;
* O próprio HTML;
* Estilizar;
* Etc.

### .innerText

O innerText é usado para obter o texto de algum elemento ou fazer a alteração. Observe o exemplo abaixo:

{% tabs %}
{% tab title="HTML" %}
```markup
<!DOCTYPE html>
<html>
    <head>
        <title>Minha página</title>
    </head>
    <body>
    <p id="algumaID">
        Um texto bonito aqui.
    </p>
    <script>
        // Disponível na aba JavaScript
    </script>
    </body>
</html>
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
var elemento = document.getElementById("algumaID")

console.log(elemento.innerText) // Output: Um texto bonito aqui.

element.innerText = "Outro texto bonito." // O elemento sofrerá alteração no seu texto da página web
```
{% endtab %}
{% endtabs %}

### .innerHTML

O innerHTML é utilizado para retornar o próprio HTML do elemento em formato de String. Também é possível fazer alterações nele para modificar o HTML de um elemento.

{% tabs %}
{% tab title="HTML" %}
```markup
<!DOCTYPE html>
<html>
    <head>
        <title>Minha página</title>
    </head>
    <body>
    <p id="algumaID">
        Um texto bonito aqui.
    </p>
    <script>
        // Disponível na aba JavaScript
    </script>
    </body>
</html>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
var elemento = document.getElementById("algumaID")

console.log(elemento.innerHTML)
/* Output:
    <p id="algumaID">
        Um texto bonito aqui.
    </p>
*/

element.innerHTML = '<p id="algumaID"> Modificando o texto utilizando o .innerHTML</p>' // O elemento sofrerá alteração no seu texto da página web, a partir das alterações no seu  HTML
```
{% endtab %}
{% endtabs %}

### .tagName

O tagName pode ser usado em um elemento, ele simplesmente retorna a tag de um elemento. O elemento não sofre alterações na sua tag se modificarmos ele através de tagName.

{% tabs %}
{% tab title="HTML" %}
```markup
<!DOCTYPE html>
<html>
    <head>
        <title>Minha página</title>
    </head>
    <body>
    <p class="azul">
        Uma div azul.
    </p>
    <div class="azul verde">
        Uma com tons de azul e verde.
    </div>
    <script>
        // Disponível na aba "Javascript"
    </script>
    </body>
</html>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
var elementos = document.getElementByClassName("azul");

for (let elemento in elementos) {
    console.log(`Foi encontrado o elemento com a tag ${elemento.tagName} com a classe especificada`);
}
```
{% endtab %}
{% endtabs %}

### .attributes

O attributes retorna uma lista de atributos de um elemento, nessa lista podemos encontrar cada atributo e o seu valor. Segue o exemplo:

{% tabs %}
{% tab title="HTML" %}
```markup
<!DOCTYPE html>
<html>
    <head>
        <title>Minha página</title>
    </head>
    <body>
    <p id="minhaID" class="azul" algumAtributo="ComUmValor">
        Uma div azul.
    </p>
    <script>
        // Disponível na aba "Javascript"
    </script>
    </body>
</html>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
var elemento = document.getElementById("minhaID");
var atributos = elemento.attributes

for (let i = 0; i < atributos.length; i++) {
    console.log(`Foi encontrado o atributo ${atributos[i].name} com o valor ${atributos[i].value}`);
}
```
{% endtab %}
{% endtabs %}

### hasAttribute\(\) , getAttribute\(\), setAttribute\(\)

Uma forma simples de verificar se um elemento possui um atributo é utilizado `hasAttribute(nome)`, com o nome sendo uma String com o nome do atributo que deseja ser verificado, a função retorna verdadeiro caso o elemento possua o atributo com o nome especificado e falso caso o contrário.

A função `getAttribute(nome)` é utilizado para retornar o atributo especificado, com o atributo podemos pegar o valor dele, dentro outras coisas. A função retorna `null` ou uma string vazia caso não encontre o atributo especificado.

A função `setAttribute(nome, valor)` é utilizada para setar o valor do atributo com o nome especificado, com o valor dado no seu parâmetro.

{% tabs %}
{% tab title="HTML" %}
```markup
<!DOCTYPE html>
<html>
    <head>
        <title>Minha página</title>
    </head>
    <body>
    <p id="minhaID">
        <input id="texto" type="text" value="Nenhum" />
    </p>
    <script>
        // Disponível na aba "Javascript"
    </script>
    </body>
</html>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
var elemento = document.getElementById("texto");

console.log(`Possui o atributo value? ${elemento.hasAttribute("value"}`); // Output: true
console.log(`O valor do atributo value: ${elemento.getAttribute("value".value}`); // Output: Nenhum

elemento.setAttribute("value", "Um novo valor"); // A modificação ocorrera na página web
```
{% endtab %}
{% endtabs %}

### .classList

O classList permite uma fácil alteração das classes de um elemento HTML, com ele podemos:

* `classList.add("classe", "outraClasse", ...)`: adicionar as classes especificadas para o elemento, caso ele ainda não contenha elas.
* `classList.remove("classe", "outraClasse", ...)`: remover classes de um elemento.
* `classList.contains("classe")`: verificar se o elemento contém a classe especificada.
* `classList.toggle("classe", "outraClasse", ...)`: caso o elemento contenha as classes especificadas, ele remove ela, caso contrário ele adiciona.

{% tabs %}
{% tab title="HTML" %}
```markup
<!DOCTYPE html>
<html>
    <head>
        <title>Minha página</title>
    </head>
    <body>
    <p id="minhaID" class="azul">
        Uma div azul.
    </p>
    <script>
        // Disponível na aba "Javascript"
    </script>
    </body>
</html>
```
{% endtab %}

{% tab title="Javascript" %}
```javascript
var elemento = document.getElementById("minhaID");

elemento.classList.add("vermelho"); // Adiciona a classe vermelha ao elemento
elemento.classList.remove("azul"); // Remove a classe azul do elemento

console.log(`O elemento possui a classe azul? ${elemento.classList.contains("azul")}`); // Output: false

elemento.classList.toggle("azul"); // Como o elemento não possui a classe azul, ele adiciona ela
```
{% endtab %}
{% endtabs %}

### style

Podemos utilizar o Javascript para estilizar o elemento e também retornar as propriedades do estilo do elemento.

O seguinte elemento vai ser utilizado como base para a explicação seguinte:

```markup
<p id="minhaID" style="background-color: red; color: white;">
    Um texto.
</p>
```

Para verificar a existência de uma propriedade CSS naquele elemento, pode ser utilizado o `style.getPropertyValue(nome)`, que retorna o valor da propriedade caso ela exista no atributo style do elemento e retorna uma string vazia caso não exista.

* `style.removePropertyValue(nome)`: pode ser usado para remover uma propriedade do estilo de um elemento.

A propriedade pode ser modificada utilizando diretamente `style.nomeDaPropriedade = "novo valor"`, que será aplicada ao estilo do elemento, mesmo que a propriedade não exista e uma forma de remover a propriedade é deixando o valor como uma string vazia.

```javascript
var elemento = document.getElementById("minhaID");

console.log(`A propriedade color possui como valor: ${elemento.style.color}`);

elemento.style.color = "black"; // O elemento sofrerá alterações no seu estilo
```

## Navegar pelo DOM

Além dos atributos, com um elemento HTML no seu código, também é possível navegar pelos elementos filho do elemento retornado.

```markup
<p id="pai">
    <span>Filho 1</span>
    <span>Filho 2</span>
</p>
```

No exemplo acima, temos o elemento com a id "pai", tendo dois filhos: o primeiro elemento com a tag span e o segundo com a mesma tag; ambos estão dentro do seu pai, o elemento com a tag  p com a id "pai".

### .children

Podemos usar children de um elemento para buscar pelos elementos filhos de um elemento pai. Segue o exemplo:

```javascript
var elemento = document.getElementById("pai");
var filhos = elemento.children;

for (let i = 0; i < filhos.length; i++) {
    console.log(`Foi encontrado o elemento filho com o texto ${filhos[i].innerText}`);
}
```

