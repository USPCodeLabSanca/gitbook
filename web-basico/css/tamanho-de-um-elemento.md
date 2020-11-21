# Tamanho de um elemento

O layout do CSS é baseado no **modelo de caixas.** Isso significa que podemos pensar em seus elementos como caixas que colocamos uma em cima da outra, e que modificamos sua cor, tamanho, posição entre outras características. 

Todos os elementos possuem 3 propriedades:

* _padding:_ o espaço ao redor do conteúdo até o _border_ .
* _border:_ uma linha entre o _padding_ e _margin._
* _margin:_ espaço externo do elemento.

Abaixo temos um exemplo genérico:

![](https://lh5.googleusercontent.com/M3WvG6GO-DxNqqGAtMbt8FtNzANWoRS9QmMlOdJRNnnW6KjlxkNGGgHuLkiAaU2hw9no__4FncjzWpRuwycq6OlU_cBvSSS49D6WA5pUs1eAFIuB005Rhc5iNN4B6iP-4Umg1li-c8E)

Abaixo tema um exemplo prático. Na aba "HTML" temos o código em HTML, em "CSS" o código em CSS, em "Resultado" temos a página resultante.

{% tabs %}
{% tab title="HTML" %}
```markup
<!DOCTYPE html>
<html>
    <head>
        <title>Exemplo</title>
        <link rel="stylesheet" type="text/css" href="style.css">
    </head>
    <body>
        <h1 id="titulo">Eu sou um parágrafo</h1>
        <div>
            <p>eu sou um parágrafo dentro da div</p>
            <p>eu tb...</p>
        </div>
    </body>
</html>
```
{% endtab %}

{% tab title="CSS" %}
```css
h1 {
    margin: 10px;
    border: solid black 2px;
    padding: 2px;
}

div{
    margin: 0px;
    padding: 10px;
    border: solid red 2px;
}

p{
    margin: 0px;
    padding-top: 0px;
    padding-bottom: 50px;
    border: dashed blueviolet 1px;
}
```
{% endtab %}

{% tab title="Resultado" %}
![](../../.gitbook/assets/image%20%285%29.png)
{% endtab %}
{% endtabs %}

Agora que você observou o exemplo, e concluiu que tem algumas coisas que não faz sentindo, vamos deixar mais claro ao responder algumas perguntas!

* A `<div>` tem `margin: 0px`; mas ela não toca o `<h1>`, porque? 
  * Isso acontece porque `<h1>` tem uma margem de  10px, que é o espaço entre `<h1>` e `<div>`.
* Porque a `<div>` não toca os cantos da margem sendo que tem`margin: 0px` ?
  * Isso acontece porque o `body`também tem uma margem.

Outra parte que você provavelmente reparou foi em `<p>` , em que está escrito `padding-top: 0px;` . Isso acontece, pois podemos definir qual parte do elemento queremos definir. Você pode usar:

* `top`: muda a parte de cima do elemento.
* `bottom`: muda a parte de baixo do elemento.
* `right`: muda a parte direita do elemento
* `left`: muda a parte esquerda do elemento.

Você pode aplicar essas definições nas três propriedades: _padding_, _border_, _margin_.  



