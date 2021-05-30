# O que é o DOM e como manipulá-lo

## O que é DOM?

O DOM \(Document Object Model\) é uma interface API para as páginas web. Ele permite que o programador possa:

* Adicionar, alterar e remove elementos HTML, como pegar uma div específica pela sua id.
* Adicionar, alterar e remover atributos e estilos \(CSS\) dos elementos HTML, como alterar o text-color de algum h1.
* Adicionar, alterar e remover eventos e interagir com esses eventos. Um exemplo de evento é o "onClick", ele acontece quando o clique do mouse acontece em algum elemento do HTML.

## Como referenciar elementos do DOM

Esta seção apresentarará como encontrar elementos de uma página web com o JavaScript, é possível procurar os elementos pelas suas tags, ids, classes. Ainda é possível alterar as propriedades dos elementos, como seu estilo, seu texto e até seu HTML.

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
    console.log(`Foi encontrado o elemento com id ${elemento.?} com a classe especificada`)
}
```
{% endtab %}
{% endtabs %}

\[exemplo com document.getElementById\]

### document.getElementsByTagName

\[texto\]

### document.querySelector

\[texto\]

## Acessar e Alterar propriedades de elementos do DOM

\[texto aqui\]

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

\[texto\]

### tagName

### attributes

### hasAttribute\(\) , getAttribute\(\), setAttribute\(\)

### classList

### style

#### setAttribute\("style", ""\)

#### style.property

## Navegar pelo DOM

\[texto aqui\]

### .children, childNodes

