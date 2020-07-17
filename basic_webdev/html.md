# HTML

## O que é

**H**yper**T**ext **M**arkup **L**anguage é a linguagem de marcação das páginas web. A criação de códigos em HTML exige somente um editor de texto e um navegador. Basta criar o documento com extensão .html, utilizar a sintaxe correta e abrí-lo via Browser. Páginas HTML são essencialmente estáticas e sem grande personalização de estilo. Para deixá-las estilizadas e dinâmicas é necessário o uso de **CSS** e **JavaScript**, respectivamente. As principais referências de HTML estão disponíveis em:

* [https://www.w3schools.com/](https://www.w3schools.com/) 
* [https://developer.mozilla.org/en-US/docs/Web/HTML](https://developer.mozilla.org/en-US/docs/Web/HTML)

O funcionamento de uma página HTML depende do uso de **tags**, marcadores entre &lt;&gt; que indicam ao navegador como o conteúdo alí delimitado deve se comportar e ser gerado. A maioria das tags possui abertura \(\) e fechamento \(**&lt;/nome\_da\_tag&gt;**\). Há exceções que se auto-fecham e não precisam de fechamento explícito. Neste caso, a sintaxe é apenas . Via de regra, **toda tag que não é auto-fechada tem marca de fechamento**.

Por exemplo, a tag que marca o início do HTML é:

```markup
    <html>
    </html>
```

Já imagens são auto fechadas:

```markup
    <img src = "./caminho_ou_url_da_imagem">
```

Existem mais de 100 tags que definem o atual HTML5. Entretanto, poucas delas são essenciais e definem a estrutura-base de tóda página HTML. Este é o esqueleto padrão de um HTML:

```markup
<!DOCTYPE html>
<html lang="en">
    <head>
        <title></title>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link href="./main.css" rel="stylesheet">
        <script src="./main.js"> </script>
    </head>
    <body>
    </body>
</html>
```

