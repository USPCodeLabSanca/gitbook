# Principais propriedades

O CSS possui MUITAS propriedades para estilizar uma página web, você consegue facilmente modificar a cor de fundo, a cor do texto, a fonte, os tamanhos e tanta coisa de um item, uma classe de itens e tanta coisa

Mesmo tento tantas, você vai usar apenas algumas nas maiorias das ocasiões, seja criando uma classe para definir um botão e diferentes classes só para mudar de cor de acordo com o nome da classe.

### Algumas propriedades

Abaixo vamos apresentar as principais propriedades utilizadas no CSS. Você pode conferir uma lista completa das propriedades [aqui](https://www.w3schools.com/cssref/).

* **background-color** : modifica a cor de fundo do seu elemento. Você pode utilizar o nome das cores \(em inglês\), o sistema RGB, RGBA, HEX, HSL ou HSLA.
* **color** : modifica a cor do texto do seu elemento. Você pode utilizar o nome das cores \(em inglês\), o sistema RGB, RGBA, HEX, HSL ou HSLA.
* **text-align**: define o alinhamento do texto de um elemento na horizontal. Você pode utilizar os seguintes valores: left \(esquerda\), right \(direita\), center \(centro\), justify \(estica a linha para que tenha a mesma largura\) , initial \(define para o padrão\), inherit \(herda a propriedade do elemento pai\).
* **font-family**: define qual a fonte que será utilizada no elemento. Essa propriedade pode ter vários valores ao mesmo tempo, isso permite que, caso o browser não suporte a opção inicial, ele poderá ir para a próxima.
* **font-size**: define o tamanho da fonte. Os valores que podem ser utilizado são: medium, xx-small, x-small, small, large, x-large, xx-large, smaller, larger, length \(define um tamanho fixo em uma das unidades permitidas\), initial \(define para o padrão\), inherit \(herda a propriedade do elemento pai\);

{% hint style="info" %}
Você pode ler sobre as diferentes unidades para tamanha que o CSS suporta [aqui](https://www.w3schools.com/cssref/css_units.asp).
{% endhint %}

Abaixo um exemplo de como as propriedades podem ser utilizadas. Na primeira aba está o código em HMTL, na segunda o código em CSS, e na última a página resultante. 

{% tabs %}
{% tab title="HTML" %}
```markup
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" type="text/css" href="style.css">
    <title>Exemplo</title>
</head>
<body>
    <h1>Eu sou o título</h1>
    <p>Mas eu sou mais importante, pois sou um parágrafo!</p>
</body>
</html>
```
{% endtab %}

{% tab title="CSS" %}
```css
body {
    margin: 0;
}

h1 {
    color: white;
    background-color: #5EC8AE;
    margin: 0;
    text-align: center;
    padding-top: 10px;
    padding-bottom: 10px;
    font-family: monospace;
}

p {
    border: 10px solid purple;
    margin: 0;
    text-align: end;
    font-size: medium;
    font-family: Verdana, Tahoma, sans-serif;
}
```
{% endtab %}

{% tab title="Resultado" %}
![](../../.gitbook/assets/image%20%2815%29.png)
{% endtab %}
{% endtabs %}

