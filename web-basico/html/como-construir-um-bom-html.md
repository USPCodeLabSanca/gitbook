# Como construir um bom HTML

Além de aprender sobre como utilizar as tags do HTML, se você se aprofundar ainda mais, descobrirá que tem como criar suas próprias tags e utilizar CSS para personalizar elas. Existe um mar enorme de possibilidades de como você pode construir a sua página com um simples HTML.

Nesse contexto serão apresentadas algumas boas práticas que você pode levar em conta na hora de criar sua página, claro que nada aqui é regra, mas são dicas que a longo prazo podem fazer uma longa diferença.

## Formatação do código

### Identação

João é um cara que está aprendendo HTML, ele deseja aprender para criar o seu próprio portfólio. João é um cientista de dados que só sabe um pouco de Python e manja bastante de R, mas para ele HTML é algo totalmente novo e ainda tá pegando o jeito.

João está fazendo uma página em HTML que já tem mais de 300 linhas, ele vê a página dele e acha GENIAL, tanto que ele apresenta ela para um amigo programador. O amigo vai ver o código-fonte da página e se impressiona em como está difícil entender como funciona. Simplesmente o código é grande, está mal identado e vira um bicho de sete cabeças para entender toda a genialidade de João.

Para visualizar melhor, observe o exemplo abaixo de um código mal identado:

```markup
  <footer id="footer">
<div class="container">
 <div class="row">
 <div id="footer-copyrights" class="col-md-6">
<p>2020 Criado pelo João.</p>
  </div>
  <div id="footer-menu" class="col-md-6">
  <ul><li>Página inicial</li>
  <li>Projetos</li>
  <li>Contato</li></ul>
</div>
</div>
</div>
  </footer>
```

Esse código bem identado é da seguinte forma:

```markup
<footer id="footer">
    <div class="container">
        <div class="row">
            <div id="footer-copyrights" class="col-md-6">
                <p>
                    2020 Criado pelo João.
                </p>
            </div>
            <div id="footer-menu" class="col-md-6">
                <ul>
                    <li>Página inicial</li>
                    <li>Projetos</li>
                    <li>Contato</li>
                </ul>
            </div>
        </div>
    </div>
</footer>
```

Olhe como o detalhe de acrescentar o TAB entre as tags já deixa o código bem mais legível e facilita bastante a compreensão. Imagine tentar entender um código-fonte de 1000 linhas sem estar "identado"? Seria muito complicado e tedioso de entender o código.

#### Uso do espaço

Além de separar as tags entre linhas, também é possível encontrar casos de códigos como esse:

```markup
<h1>Tabela</h1><table><tr><th>Coluna 1</th><th>Coluna 2</th></tr>
<tr><td>Maçã</td><td>Açúcar</td></tr></table>
```

Assim como no exemplo acima devemos "identar" o código para que ele se torne o mais legível possível:

```markup
<h1>Tabela</h1>
<table>
    <tr>
        <th>Coluna 1</th>
        <th>Coluna 2</th>
    </tr>
    <tr>
        <td>Maçã</td>
        <td>Açúcar</td>
    </tr>
</table>
```

Então, use bastante as teclas **TAB**, **SHIFT-TAB** e **ESPAÇO** na hora de impressionar seu amigo programador!

### Comentários

Comentar o código é algo que é muito discutido quando se trata de linguagens de programação como JavaScript, Java, Rust, etc. No HTML a discussão é diferente, é justamente **não comentar** o código!

Uma das razões disso é que o código em HTML é de fácil compreensão e autoexplicativo. Então não precisa comentar cada seção da sua página, preocupe-se que seu código-fonte esteja bem organizado e fácil de entender como funciona!

Mesmo que você queira usar, prefira por poucos e breves comentários.

### Controle na quantidade de divs

É muito fácil e comum fazermos um uso exagerado de divs para estilizar e estruturar os componentes da página. Para evitar esses usos exagerados, devemos usar as diversas tags do HTML para evitar criar uma lista longa de divs. Uma boa forma é utilizar as tags que deixam a semântica do site bem compreensível, como separar o site com `<section>, <article>, <footer>`, etc. Essa página fala mais sobre: [https://blog.geekhunter.com.br/voce-conhece-html-semantico/](https://blog.geekhunter.com.br/voce-conhece-html-semantico/)

Segue o exemplo com o uso de uma enorme quantidade de divs para uma postagem de um site de notícias:

```markup
<div class="container">
    <div class="title">
        Título
    </div>
    <div class="subtitle">
        Subtítulo
    </div>
    <div class="content">
        Conteúdo da nótícia.
    </div>
</div>
```

Podemos simplificar esse código e utilizar outras tags HTML para facilitar a compreensão do código e também tornar mais bonito:

```markup
<section class="container">
    <h1>Título</h1>
    <h2>Subtítulo</h2>
    <p>
        Conteúdo da notícia.
    </p>
</section>
```

Observe como reduzimos a quantidade de divs para zero e ainda deixamos o código mais bonito.

## Estrutura da página

### &lt;DOCTYPE html&gt;

Talvez você esteja apenas tentando criar uma página simples e que não vá ter muitos elementos. Como um simples formulário de login, então apenas são usadas estruturas básicas do HTML, como:

```markup
<html>
    <h1>Faça o seu login:</h1>
    <form action="login.php">
        <span>Email:</span>
        <input type="text" />
        <span>Senha:</span>
        <input type="password" />
    </form>
</html>
```

Mesmo que a sua página seja simples como essa, ainda é necessário que você use toda a semântica do HTML, já que faltam elementos fundamentais como `<title>` no `<header>`, já que sua página nem sequer tem um título na aba do navegador.

No caso de criar uma página simples, não deixe de ser perfeccionista! Use toda a estrutura que o HTML pode proporcionar ao seu código, ter uma página com toda a estrutura do HTML facilita para as *engines* de busca para entender a sua página e também garante que vai funcionar em todo lugar.

O código com toda estrutura é o seguinte \(e com algumas pequenas edições para deixar o código mais limpo\):

```markup
<DOCTYPE html>
<html>
    <head>
        <title>Login</title>
    </head>
    <body>
        <section class="container">
            <h1>Faça seu login:</h1>
            <forms action="login.php">
                <div class="input">
                    <span>Email:</span>
                    <input type="text" />
                </div>
                <div class="input">
                    <span>Senha:</span>
                    <input type="password" />
                </div>
            </forms>
        </section>
    </body>
</html>
```

### &lt;h1&gt;

Nas páginas web a tag `<h1>` normalmente é utilizada pelos mecanismos de pesquisa para procurar elementos que representam o conteúdo da página. Logo, é importante que você use apenas um `<h1>` na sua página e se precisar de mais pode abusar dos `<h2>`, `<h3>`, etc.

### `style="color: green; font-family-size: Tahoma; font-size; 32px; font-weight: bold;"`

Em algumas situações queremos aplicar um estilo a apenas um elemento da página, ou queremos alterar uma propriedade do CSS, como a cor do texto, então atribuímos a tag `style="..."` ao elemento. 

Mesmo que seja um quebra-galho, em algumas situações o uso do `style="..."` pode ser uma má prática. Quanto mais precisarmos alterar as propriedades CSS do elemento, mais vamos tornar o código-fonte da página complexo e também teremos interferências com o próprio código CSS da página, dificultando a interpretação.

Então, quando quiser criar um estilo único a algum elemento da página é recomendável editar o próprio CSS da página.

