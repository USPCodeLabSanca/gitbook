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

Essa propriedade irá definir a define o alinhamento dos itens. Os valores da propriedades podem ser:

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

