# Entrada de Dados

{% tabs %}
{% tab title="Código" %}
```markup
<head>
    <title>Exemplo</title>
</head>
<body>
    <input type="text">
    <input type="submit" value="Enviar">
    <button>Eu sou um botão!</button>
    <form action="/action_page.php">
        <!-- Ao clicar em "Enviar de novo" a informação do forms
        irá para um servidor chamado "action_page.php" -->
        <input type="text"><br><br>
        <input type="enviar" value="Enviar de novo">
    </form>
</body>
</html>
```
{% endtab %}
{% endtabs %}

**&lt;input&gt;** — Essa tag é utilizada para a entrada de informação. Para definir o tipo de informação que se receberá, você irá utilizar o atributo "*type*". Por exemplo, se você quiser criar um espaço para que o usuário entre um texto, você irá digitar:

```markup
<input type="text">
```

**&lt;button&gt;** — Essa tag é utilizada para criar um elemento clicável, ou seja, um botão!

{% hint style="info" %}
Por que existe uma tag de botão se é possível criar o mesmo efeito com a tag &lt;input&gt;?

Dentro da tag &lt;button&gt; é possível colocar texto e outras tag \(como &lt;img&gt;\).
{% endhint %}

**&lt;form&gt;** — Irá criar uma seção na sua página que irá conter outras tags que irão interagir e permitir que o usuário submeta informações a um determinado servidor web. O atributo "action" irá receber a URL do programa que irá processar a informação.

## Exemplo

Abaixo mostramos um exemplo de como essas tags devem ser escritas. Na aba "Código" está o código, e na aba "Resultado" está a página resultante.

{% tabs %}
{% tab title="Código" %}
```markup
<head>
    <title>Exemplo</title>
</head>
<body>
    <input type="text">
    <input type="submit" value="Enviar">
    <button>Eu sou um botão!</button>
    <form action="/action_page.php">
        <input type="text"><br><br>
        <input type="submit" value="Enviar de novo">
        <!-- Ao clicar em "Enviar de novo" a informação do forms
        irá para um servidor chamado "action_page.php" -->
    </form>
</body>
</html>
```
{% endtab %}

{% tab title="Exemplo" %}
![](../../../.gitbook/assets/image%20%283%29.png)
{% endtab %}
{% endtabs %}

