# Seletores



Seletores são responsáveis por selecionar os elementos HTML que queremos modificar. Existem vários tipos, nessa seção iremos mostrar os principais, porém se você quiser saber mais sobre eles pode acessar a página da [Mozilla](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors).

Os principais seletores são:

* **Tipo:** selecionam todos os elementos de determinado tipo, por exemplo `p`  seleciona todos os `<p>`
*  **Id:** seleciona todos os elementos com o mesmo id. Apesar de poder dar o mesmo id para mais de um elemento é recomendado apenas um id por elemento. Para usar basta colocar uma **\#** antes do id. Por exemplo, `#eusoulindo` seleciona o elemento que tiver `< id="eusoulindo" >`
* **Classe:** seleciona todos os elementos com a mesma classe. Para usar basta colocar um . antes do nome da classe. Por exemplo, `.nossomoslindos` seleciona os elementos que tiverem `< class="nossomoslindos" >`
* **Atributos:** seleciona os elementos de determinado tipo com certos atributos. Para usar basta colocar o atributo entre **\[ \]** depois do tipo. Por exemplo, se queremos selecionar imagens com src devemos escrever `img[src]`, serão selecionados `<img src="minhaimagem.jpg">` , mas não `<img>`.
* **Pseudo-classe:** seleciona os elementos de determinados tipos somente quando estiver no estado escolhido. Por exemplo, queremos que selecionar um link somente quando o mouse estiver em cima dele. Iremos usar `a:hover` para selecionar `<a>` quando o mouse estiver em cima dele.
* **Baseados na sua relação**: seleciona elementos baseado em sua relação com outros. É modo de criar seletores específicos para o que você precisa. Na tabela abaixo temos os mais comuns.

| Seletores | **O que ele seleciona** |
| :--- | :--- |
| A E | Qualquer elemento E que seja descendente de A \(como  filhos, filhos de filhos, etc\) |
| A &gt; E | Qualquer elemento de E que seja filho de A \(ou seja, um descendente direto\) |
| E: first-child | Qualquer elemento de E que seja seu primeiro filho |
| B + E | Qualquer elemento de E que seja irmão de B |

**Especificidade:** em alguns casos pode ocorrer de um elemento receber mais de uma propriedade. Nesses casos, o CSS dará prioridade ao seletor com uma maior especificidade. Um seletor é mais específico que classes, pseudo-classe e atributos, que por sua vez são mais específicos do que uma tag. Você pode evitar esse problema ao criar seletores mais específicos os combinado. Por exemplo `.key` seleciona todos os elementos da classe `key`, porem `p.key` seleciona todos os parágrafos da classe `key`.

Abaixo tema um exemplo dos seletores. Na aba "HTML" temos o código em HTML, em "CSS" o código em CSS, em "Resultado 1" temos a página resultante com o mouse fora da imagem, e em "Resultado 2" temos a página resultante com o mouse em cima da imagem. 

{% tabs %}
{% tab title="HTMl" %}
```markup
<!DOCTYPE html>
<html>
    <head>
        <title>Exemplo</title>
        <link rel="stylesheet" type="text/css" href="arquivo.css">
    </head>
    <body>
        <h1 id="titulo">USPCodeLab</h1>
        <p class="texto">Nosso objetivo: </p>
        <p class="texto">Grupo de extensão universitária que tem como objetivo estimular a inovação tecnológica na USP.</p>
        <img src="logo.png">
    </body>
</html>
```
{% endtab %}

{% tab title="CSS" %}
```css
body {
    background-color: indigo;
}
#titulo {
    color: red;
}

.texto {
    color: greenyellow;
}

img[src] {
    width: 100px;
    height: 100px;
}

img:hover {
    width: 300px;
    height: 300px;
}
```
{% endtab %}

{% tab title="Resultado 1" %}
![](../../.gitbook/assets/image%20%286%29.png)
{% endtab %}

{% tab title="Resultado 2" %}
![](../../.gitbook/assets/image%20%287%29.png)
{% endtab %}
{% endtabs %}

