# Flexbox

O Flexbox é um modelo de layout que permite organizar os elementos espacialmente dentro da sua interface. Nesse artigo vamos descrever suas principais propriedades, para mais informação  recomendamos esse [guia](https://css-tricks.com/snippets/css/a-guide-to-flexbox/).

Antes de entrarmos nas propriedades precisamos definir um elemento como fl_ex,_ isso significa que todos os elementos dentro dele \(que vamos chamar de _contêiner_ \) irão seguir as propriedades do contêiner. Abaixo mostramos como definir um elemento como _flex_.

```css
.container {
  display: flex; 
}
```

### **f**lex-direction

Essa propriedade irá definir a direção em que os itens serão posicionados. Os valores da propriedades podem ser:

{% tabs %}
{% tab title="row" %}
Os itens serão posicionados da esquerda para a direita \(opção padrão\).

![](https://lh4.googleusercontent.com/s5mB6TUzX0okFrn-le5hcuyakMODWcXJh24F0brSHEcGrcnVnILkN_ZoPhut3hnNSSEbHIe7u8s0zr5qZq_A6R7xWj1HKkYflPcvLS5KKoe_3izFRog2ezj9cF5hnQoqsGrmcD6VoRQ)
{% endtab %}

{% tab title="row-reverse" %}
Os itens serão posicionados da direita para a esquerda.

![](https://lh6.googleusercontent.com/XY-ZU7I40MXa1Od0WjtnkAHy6u9dTcUu8WdhQPrDAC9JxN420ZI5l0KC-wDMe7fJ0Rh62kBxlKb3f08GBzEe9fYeJr4defQvj6Mdk4LpbnW7WlhcqODcBXMPmU_ziCaO4QAoWFJknyk)
{% endtab %}

{% tab title="column" %}
Os itens serão posicionados de cima para baixo.

![](https://lh3.googleusercontent.com/EDlcP2p7oa7pEjJSXRgKSlEOS15rvPy02m7723qNOeCbuugm6NELLbbZ4TjaQcrGTgyvdyKscubq-Btb4neFOXFjtbw-j2UX2_mQ7SMcR3vScckoNdKFalfN7eKw--GwV329d-yMnJc)
{% endtab %}

{% tab title="column-reverse" %}
Os itens serão posicionados de baixo para cima.

![](https://lh3.googleusercontent.com/vYA7uu7dlNBdQP-t-M0zeuNkZSGk6gRYazloo3ho2FpIZhm3JqJsXXkwqqKipp8NMwr1NeWrP1xcoXaRmWX8tPwhndRaFxloUGy9miskRf_xjvBrMCh8JZ4yKxVb0fxxKRnP1Dg5vJI)

  
{% endtab %}
{% endtabs %}

### **justify-content**

Essa propriedade irá definir o alinhamento dos itens. Os valores da propriedades podem ser:

{% tabs %}
{% tab title="flex-start" %}
Os itens serão alinhados no começo da linha \(opção padrão\).

![](https://lh6.googleusercontent.com/K-JZv2TUqdhtm4JFdKb_ga4fqEI5k_KigZelhOXG01nbeQkzPiTnR9BkTE6p7vgOuUHvdDbqWXu6Z_0-U7Q7pMVNAk6xmaGfwb7k6zq5g3DlJvKJIsy3pSlsV88a96f7xzPL4ICijHg)
{% endtab %}

{% tab title="flex-end" %}
Os itens serão alinhados no fim da linha. 

![](https://lh6.googleusercontent.com/Bpt2pFCa1u2wahZtRArPaz_v2qb-d5c42h1-SCA-eHrGHJg-1GnOUhtkIPKIC3zU-RU8n1kbCmUhaVj2GBuVhp3j6ALIGTUjiwxB0ED06watsbNZb3IHZznOHPLP_ke2aX6PNHjUXoQ)
{% endtab %}

{% tab title="center" %}
Os itens serão alinhados centrados na linha.

![](https://lh6.googleusercontent.com/SEOtqwWXCen6qOE8PIipj0Kugoi3iNhaSkCOspDSWsAMWvHM-t1Y7kzefE-n_sZquddjp7O7nivcnNTTDMrT2Y-S1cKl_3Lscg2lD1hgEA0A_V84iNMRhyrTX_yovaSeGST6htFFRPY)
{% endtab %}

{% tab title="space-between" %}
Os itens serão alinhados de modo que fiquem divididos igualmente na linha.

![](https://lh3.googleusercontent.com/TXEXpPbwQm8duISjkXs3O77iRRkajQ7HGUdy2HgvXVFGvE-X_FnfyZele_UAyaugf-U-Ga_5lsv6fhQRe1dDf_7XgKV1_LYPQwYd9Efx-I8twYUE27wID5Ti_HuhBE7-rdUFYj7LlFI)
{% endtab %}

{% tab title="space-around" %}
Os itens serão alinhados de modo que fiquem divididos na linha com espaços iguais entre eles.

![](https://lh3.googleusercontent.com/INYy0wt_lWQD-uymKWUqBy3ADgJTw_sQIeOn3KAXjniicMaoshtExNBhbQ1K3JsvmHrct5cDQ1KK_0FL7yT0NOnac9-Zbfdv3PORnA1GqFGmvMixkt-bRZzika-82k8CinIzat5cH5U)

\*\*\*\*
{% endtab %}

{% tab title="space-evenly" %}
Os itens serão alinhados de modo que fiquem divididos de modo que dois itens sempre tenham o mesmo espaço entre eles.

![](https://lh3.googleusercontent.com/INYy0wt_lWQD-uymKWUqBy3ADgJTw_sQIeOn3KAXjniicMaoshtExNBhbQ1K3JsvmHrct5cDQ1KK_0FL7yT0NOnac9-Zbfdv3PORnA1GqFGmvMixkt-bRZzika-82k8CinIzat5cH5U)
{% endtab %}
{% endtabs %}

### **flex-wrap**

Por padrão todos elementos alinhados em uma linha, é possível modificar isso ****com a propriedade flex-wrap. Os valores da propridade podem ser:

{% tabs %}
{% tab title="nowrap" %}
Todos os itens serão alinhados em uma linha \(opção padrão\).

![](https://lh5.googleusercontent.com/UwtPNOoYYzjZFZx2sYKfz-KAfGJYVXRPXXKfqOt9z8H4FgfhJIv5vELIwONi5rY-377cwzGCjsDH-omwzFb5kXAfHDzkzh8WJET1rBspRHRAU64PJstbpslWNRU7brjzxIQJ5jOYyno)
{% endtab %}

{% tab title="wrap" %}
Os itens irão para a próxima linha conforme necessário.

![](https://lh5.googleusercontent.com/VnmxxfKCFRw_XtYWFYsFyJir9543C6-wwO52W20pmmf76JC65xz0J6v8y7GXH0EtDBPwL56yZllf2Srp0yUqLngi_3gUnIqsjIIl1WerrDU-zffgTJ1onNS_e3AVvsrAt4rWHBbGe94)
{% endtab %}

{% tab title="wrap-reverse" %}
Os itens irão para a próxima linha conforme necessário, porém do fim para o início.

![](https://lh6.googleusercontent.com/ngfyh27RSbQSp_2mJWUdg7ottUxohXzRETiNyKKuUZslWIY7dhWrA-7x13Q8iHE41lK-ie4r6Eahdk5WXRX5wYs8ySBWJel_bLS3FpWr2YOcjX8JbtrDVu1pueGzW2lrdbblUe509bw)
{% endtab %}
{% endtabs %}

### **align-content**

Organiza a distribuição dos itens no eixo y.

{% tabs %}
{% tab title="stretch" %}
Distribui os itens de modo que ocupem todo o espaço disponível do eixo y. \(opção padrão\).

![](https://lh5.googleusercontent.com/b7DV6ndyZbwLHUP0WDBcKPY2ZYnYfTp0TGd4EMyxDuKnJrv7IIM8wWEaBHSZJS-VjNduypbjV7TF3aNueVCfx2Nd0c43WHT3EF5D64DDsMfeGP14tCJmxBiLXyMd9mjkITDRtxLFo0A)

  
{% endtab %}

{% tab title="space-around" %}
Os itens são distribuídos igualmente e o espaço entre eles são iguais no eixo y.

![](https://lh3.googleusercontent.com/D-Pkisp2UHv10EvCk33Vl7qWbaptN6SjKIjAV8ee3VCOMcDDUqRmrEg7zERXKniSsysxGVJ2r4A-rp0CtE4aZc9POCt_Kqb58-wRUEpFY5Ytcr91aNd-qvqsJvkuQWRjVdO-y5MyO6o)

  
{% endtab %}

{% tab title="space-between" %}
Os itens são distribuídos igualmente no eixo y.

![](https://lh3.googleusercontent.com/xLnuOFQseN_hWNdTcoVl99Ttuak-Cxn2HVtquyvwAMYzPZWGi7wjseFrUgR2yQJyrBmFOP085zUwisQS1U0mQ-1qU8M0WvHWVVrYwQl7TEuBYjxRZMegXLac-EAL5SXJHurM_hH4Kc0)
{% endtab %}

{% tab title="center" %}
Os itens são posicionados no centro do eixo y.

![](https://lh5.googleusercontent.com/flkx0jNgZhKZw33XZ5R19ZD5liplimd_g9igKXGajbkeZgq-zbuGj71GrytUjgzsUzsmoNCGuFB87D-pyMi_LSibo4fRjXy0gORuw_yLt9eVaHGVxZa7T4o3Ti1SIfLuozcm8aAewYs)

  
{% endtab %}

{% tab title="flex-start" %}
Os itens são posicionados a partir do começo no eixo y.

![](https://lh3.googleusercontent.com/I6jFzLwImOLifigfH8k0brWZqDVW1pqWMMKPjl6AaeDtuvJEOslhLzoISWBv0N4JKkD4BIa7keavBbHI0HIS1u6sUtYNO-HPtL9qKyfscEma7omxvfgO3lqAGVjQuwZLa-ZhLEPxV-c)
{% endtab %}

{% tab title="flex-end" %}
Os itens são posicionados a partir do fim no eixo y.

![](https://lh6.googleusercontent.com/6jjEmw2b07p47yABQh-TStsJb7CQ9fh0RNoGrk0NhtkbdBQnGRJ4uE9NkPfDs78qiaWnW5s5v2f1ONJQawfz88CpKAntjEbOv6z-f2rQ5KgJaCUowkzkvvh8o7fs34rNXsC22bxbmjo)
{% endtab %}
{% endtabs %}

Abaixo temos um exemplo completo de como essas propriedades podem ser usadas. Na primeira aba temos o código em HTML, na segunda o CSS e por último a página resultante. 

{% tabs %}
{% tab title="HTML" %}
```markup
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" type="text/css" href="style.css">
    <title>Flexbox</title>
</head>
<body>
    <div id="Exe1">
        <p>Caixa 1</p>
        <p>Caixa 2</p>
        <p>Caixa 3</p>
    </div>

    <div id="Exe2">
        <p>Caixa 1</p>
        <p>Caixa 2</p>
        <p>Caixa 3</p>
        <p>Caixa 4</p>
        <p>Caixa 5</p>
        <p>Caixa 6</p>
        <p>Caixa 7</p>
    </div>
</body>
</html>
```
{% endtab %}

{% tab title="CSS" %}
```css
p {
    border: mediumvioletred 2px solid;
}

#Exe1 {
    border: black 2px solid;
    display: flex;
    flex-direction: row;
    justify-content: center;
}

#Exe2 {
    border: black 2px solid;
    display: flex;
    flex-direction: row-reverse;
    justify-content: space-between;
}
```
{% endtab %}

{% tab title="Resultado" %}
![](../../.gitbook/assets/image%20%2816%29.png)
{% endtab %}
{% endtabs %}

