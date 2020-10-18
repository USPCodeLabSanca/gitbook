# A estrutura básica

A **estrutura básica** de um arquivo HTML é o que você **sempre** deve escrever ao começar qualquer projeto. Ela é tão primordial que ao digitar a tag &lt;html&gt; no editor de texto Sublime ele insere essa estrutura automaticamente.

{% code title="Estrutura Básica" %}
```markup
<!DOCTYPE html>
<html>
<head>
    <title></title>
</head>
<body>
</body>
</html>
```
{% endcode %}

Lembrando que na tag &lt;title&gt; é necessário que você escreva o título da sua página.

Outra tag interessante de você utilizar no código está abaixo.

```markup
<meta charset=”UTF-8”>
```

Ela deve ser colocado no &lt;head&gt;, e indica ao navegador qual tabela de caractéres você está usando. No caso, indicamos a [Unicode](https://home.unicode.org/), que é a tabela mais usada universalmente.

