# Tamanho de um elemento

O layout do CSS é baseado no **modelo de caixas.** Isso significa que podemos pensar em seus elementos como caixas que colocamos uma em cima da outra ou uma dentro da outra, e que modificamos sua cor, tamanho, posição entre outras características. 

Todos os elementos possuem 3 propriedades:

* _padding:_ o espaço ao redor do conteúdo \(_content_\) até o _border_ .
* _border:_ uma linha \(borda\) entre o _padding_ e _margin._
* _margin:_ espaço externo \(expansão\) do elemento.

Abaixo temos um exemplo genérico, retirado de [W3Schools](https://www.w3schools.com/css/css_boxmodel.asp):

![](../../.gitbook/assets/image%20%2810%29.png)

Abaixo temos um exemplo prático. Na aba "HTML" temos o código em HTML, em "CSS" o código em CSS e em "Resultado" temos a página resultante.

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

Agora que você observou o exemplo e concluiu que tem algumas coisas que não fazem sentindo, vamos deixar mais claro ao responder algumas perguntas!

* A `<div>` tem `margin: 0px`; mas ela não toca o `<h1>`, porque? 
  * Isso acontece porque `<h1>` tem uma margem de  10px, que é o espaço entre `<h1>` e `<div>`.
* Porque a `<div>` não toca os cantos da margem sendo que tem`margin: 0px` ?
  * Isso acontece porque o `body`também tem uma margem.

Outra parte que você provavelmente reparou foi que em `<p>` está escrito `padding-top: 0px;` . Isso acontece pois podemos definir qual "canto" do elemento queremos modificar e, portanto, atribuir valores específicos a cada um deles. Você pode usar:

* `top`: muda a parte de cima do elemento.
* `bottom`: muda a parte de baixo do elemento.
* `right`: muda a parte direita do elemento
* `left`: muda a parte esquerda do elemento.

Você pode aplicar essas definições nas três propriedades: _padding_, _border_, _margin_.

#### Altura e Largura de um elemento

Podemos também definir a altura e largura de um elemento com os comandos `height` e `width` respectivamente. Quando fazemos isso, estamos definindo somente o tamanho do conteúdo \(_content_\). O tamanho total do elemento é soma de todas as suas propriedades.

Por exemplo,

```css
p{
    margin: 0px;
    padding-top: 0px;
    padding-bottom: 50px;
    border: dashed blueviolet 1px;
    height: 30px;
}
```

O tamanho total desse elemento é 82px.

* Margin = 0 px 
* Padding = 50px \(bottom\) 
* Border = 2px \(top + bottom\) 
* Height = 30px
* Total = 82px

