# Grid

O layout em ***Grid*** é uma forma de ter bastante controle nas duas dimensões.

Diferentemente do *flexbox*, que é mais fluído no posicionamento dos elementos em uma certa divisão da página. O *grid* te dá total controle em qual vai ser a largura e a altura de cada linha ou coluna da página, além de poder ditar quantas colunas quer que seja usada.

Para fazer que um elemento esteja em *grid*, inicialmente você precisa fazer:

```css
.start{
    display: grid
}
```

### Unidade de medida de fração \(fr\)

Essa unidade representa uma fração do espaço  disponível no `grid-container`. Então, for necessário que um elemento ocupe 1fr (uma parte) do *grid*, ele separa exatamente esse espaço para o elemento. Caso se for colocado 2fr, será separado exatamente o espaço de 2 frações do *container* etc...

### Repeat\(\) 

Essa função ajuda a separar mais facilmente um template para que o *grid* funcione. Dessa forma, se usarmos `repeat(5, 1fr)`, o *container*, seja coluna ou linha, vai separar os elementos em 5 espaços e fazer com que os elementos tenham a mesma largura ou altura. 

### Parâmetros

#### `grid-template`

Os dois primeiros parâmetros mais importantes são os `grid-template-row` e o `grid-template-columns`. Esses parâmetros definem o espaço no *grid* que os elementos podem ser colocados dentro do *container*.

```css
.container{
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    grid-template-rows: 50% 50% 
}

```

No exemplo acima, as colunas são separadas pra se fracionarem igualmente em 6 partes no *container* inteiro, enquantos as linhas se comportam para que cada elemento ocupe metade do *container*.

#### `grid-column-start` e `grid-column-end`

Esses parâmetros mostram em quais colunas o elemento tem que começar e terminar no *grid*. Isso é equivalente ao `grid-row-start` e `grid-row-end`.

```css
.elem1{
    grid-column-start: 2;
    grid-column-end: 4;
}
```

 O exemplo acima mostra que o elemento terá que ocupar entre as colunas 2 e 4 do *container*.

#### justify-itens

Alinha os itens do *grid* de acordo com a linha que ela está posta

```css
.wrapper{
    justify-itens: center
}
```

No exemplo acima, os itens do *grid* serão colocados no centro de cada área separada no grid, mesmo que o elemento não ocupe todo o espaço pré-determinado \(o parâmetro `align-itens` faz o mesmo, mas de acordo com a coluna que os elementos estão separados.\)

