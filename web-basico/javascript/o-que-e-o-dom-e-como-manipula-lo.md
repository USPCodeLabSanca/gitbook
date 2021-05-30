# O que é o DOM e como manipulá-lo

## O que é DOM?

O DOM \(Document Object Model\) é uma interface API para as páginas web. Ele permite que o programador possa:

* Adicionar, alterar e remove elementos HTML, como pegar uma div específica pela sua id.
* Adicionar, alterar e remover atributos e estilos \(CSS\) dos elementos HTML, como alterar o text-color de algum h1.
* Adicionar, alterar e remover eventos e interagir com esses eventos. Um exemplo de evento é o "onClick", ele acontece quando o clique do mouse acontece em algum elemento do HTML.

## Como referenciar elementos do DOM

\[texto aqui\]

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

\[texto\]

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
var elementos = document.getElementByClassName("algumaclasse");

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

O innerText \[texto\]

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

