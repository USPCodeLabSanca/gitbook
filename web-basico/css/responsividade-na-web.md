# Responsividade na Web

Com certeza você já deve ter ouvido falar em design responsivo e entenda que ele indica se um site é acessível de forma satisfatória em dispositivos com diferentes tamanhos de tela, mas você sabe quais são os fundamentos que devem ser aplicados durante o desenvolvimento para que uma página seja responsiva?

Primeiro vamos citar todos fundamentos com uma breve explicação e mais abaixo dar detalhes sobre cada um deles.

**1. Grids flexíveis:** Organizam a estrutura do site buscando por meio de linhas e colunas mostrar de forma satisfatória as informações de um site.

**2. Imagens flexíveis:** As imagens devem ser mostradas com seu tamanho original em telas grandes e caso necessário eles devem ser diminuídas para caber em telas menores.

**3. Media Queries:** Funcionam como uma especie de _if_ para estilos de uma página. Aqui vamos utilizá-las pensando apenas em condicionais para tamanho de tela porem elas tem algumas funções bem interessantes que fogem um pouco do escopo desse tópico.

## Grids Flexíveis

Com a adição da Flexbox e posteriormente do Grid foi possível organizar o  conteúdo de uma página de forma bem simples. Aqui não vamos falar de como utilizar essas duas tecnologia já que isso foi abordado nos tópicos de Flexbox e Grid ao lado.

Quando falamos de grids flexíveis devemos pensar em como utilizar tanto a Flexbox quanto o Grid para adaptar nosso conteúdo a diferentes tamanhos de tela, mais precisamente precisamos utilizamos para que em telas pequenas nosso conteúdo tenha apenas uma coluna e conforme maior for a largura da tela que esse conteúdo ocupe um numero adequado de colunas deixando a visualização agradável.

## Imagens Flexíveis

Como dito anteriormente é esperado que as imagens de uma página tenham no máximo seu tamanho original em telas grandes e que elas se adequem ao tamanho de telas menores. Isso é alcançado por meio do CSS:

```css
img {
  max-width: 100%:
} 
```

## Medias Queries

O ultimo fundamento do desenvolvimento responsivo \(e o mais importante\) se trata de uma especie de if para nossos estilos:

```css
@media screen and (min-width: 768px) {
  .coluna {
    width: 25%;
  }
} 
```

Talvez com o exemplo acima voce já tenha entendido como as Media Queries funcionam mas ainda sim vamos dissecar esse pedaço de CSS.

A primeira palavra do comando é `@media`, ela sinaliza a declaração de uma Media Query. Logo após temos a palavra `screen`, ela diz que essa query será aplicada apenas em telas \(outro possível valor é `print`, utilizado para impressões\), em seguida temos o `and (min-width: 768px)`, intuitivamente essa queries será aplicadas em telas com largura minima de 768px. Dentro da media query colocamos o CSS que será aplicado quando sua condição for satisfeita, no caso:

```css
.coluna {
  width: 25%;
}
```

Acredito que com esse exemplo fica claro o uso de media queries para adaptar nosso grid a diferentes tamanhos de tela. Outra aplicação bem utilizada para as queries é mostrar ou não alguma parte da página por meio do `display: none;`.

