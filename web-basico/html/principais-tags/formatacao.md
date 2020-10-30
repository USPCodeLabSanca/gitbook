# Formatação

**&lt;h1&gt;&lt;/h1&gt;** — Permite que coloque um título no corpo da sua página. O número depois do "h" pode variar de 1 a 6. Ele indica o quão importante é o seu título. Por exemplo, &lt;h1&gt; é o seu título, &lt;h2&gt; é o seu sub-título, &lt;h3&gt; o seu sub-sub-título, e assim por diante. Vamos falar porquê é importante fazer essa distinção na seção "Como construir um bom HTML".

**&lt;p&gt;&lt;/p&gt;** — Permite que você coloque um parágrafo no corpo da sua página.

**&lt;br&gt;** — Permite colocar uma única quebra de linha. Útil para escrever endereços ou poemas. Essa é uma **tag vazia**, ou seja, ela não tem tag de fechamento.

## Exemplo

Abaixo mostramos um exemplo de como essas tags devem ser escritas. Na aba "Código" está o código, e na aba "Resultado" está a página resultante.

{% tabs %}
{% tab title="Código" %}
```markup
<!DOCTYPE html>
<html>
<head>
    <title>Exemplo</html>
</head>
<body>
    <h1>Primeiro</h1>
    <h6>Ultimo</h6>
    <p>Isso é um parágrafo</p>
    <p>Isso é uma quebra <br> de linha</p>
</body>
</html>
```
{% endtab %}

{% tab title="Resultado" %}
![](../../../.gitbook/assets/formatacao.png)
{% endtab %}
{% endtabs %}

