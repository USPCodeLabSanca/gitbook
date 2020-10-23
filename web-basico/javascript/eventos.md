---
description: O que são e como usar eventos em JavaScript.
---

# Eventos

### O que são eventos?

Eventos são, essencialmente, qualquer coisa que pode acontecer em um momento indeterminado \(ex: usuário clica num botão, uma tecla do teclado é pressionada, informações do servidor chegam, etc...\). Em JavaScript, podemos escrever código que é executando quando um evento acontece através de um _Event Listener_ \(ouvidor de eventos\). Um _Event Listener_ é uma função que é executada quando um evento específico ocorre. Veja esse exemplo:

```javascript
// Seleciona um botão com ID 'button'.
const button = document.getElementById('button');

// Adiciona um "Event Listener" ao botão, que "ouve" o evento de click do mouse.
// Quando o usuário clickar nesse botão, a função sayHi será chamada, e aparecerá "hi" para o usuário.
button.addEventListener('click', sayHi);

// Função que será executada quando o evento ocorrer.
function sayHi () {
    alert('hi');
}
```

Aqui, vemos a chamada de `button.addEventListener`. Todos os objetos do DOM implementam a função `addEventListener`, que recebe dois argumentos: o tipo do evento \(`click`, `keydown`, `focus`, etc...\), e uma função que será executada quando esse evento ocorrer. Nesse caso, o tipo de evento é "`click`" e a função é "`sayHi`", então sempre que acontecer o evento "`click`" no botão, a função "`sayHi`" será executada.

Na esmagadora maioria das páginas web, queremos poder responder a ações do usuário. Por isso, eventos são uma parte vital da web moderna.

### O objeto de eventos

A função que é chamada quando um evento é disparado recebe exatamente um argumento: um objeto de evento. Esse objeto contém informações relacionadas ao evento, e algumas funções que podem modificar o comportamento desse evento. Veja esse exemplo:

```javascript
// Seleciona um botão com ID 'button'.
const button = document.getElementById('button-id');

// Aqui, ao invés de declarar uma função separada do evento, e "linkar" os dois juntos depois,
// só declaramos uma Arrow Function direto na função de evento.
button.addEventListener('keydown', event => {
    // Para eventos relacionados ao teclado, o objeto de eventos possui uma propriedade
    // "key", que contém a tecla que o usuário apertou.
    alert('Você apertou ' + event.key);
});
```

Veja que agora a função do evento recebe um argumento, que usamos para descobrir qual tecla o usuário apertou. Cada tipo de evento \(_MouseEvent_, _KeyboardEvent_, _FocusEvent_, etc...\) gera um objeto de eventos com informações diferentes. Por exemplo, os eventos de mouse tem informações da posição do mouse na tela, os eventos de teclado tem informações sobre as teclas pressionadas, os eventos de foco tem informações de qual elemento recebeu foco, e qual perdeu o foco.

O objeto de eventos também possui algumas funções que podem modificar o seu comportamento. Entre elas, a mais popular é, sem dúvida, a "`preventDefault`".

#### `preventDefault()`

Essa é uma função disponível dentro de qualquer tipo de objeto de eventos. Quando chamada, a função impede o browser de realizar as ações "padrão" que ele realizaria com esse evento. Por exemplo, quando o usuário clica numa tag de âncora \("`<a>`"\), ele é redirecionado para o link que foi especificado na propriedade `href` dela, a não ser que algum _Event Listener_ chame a função `preventDefault` no objeto de eventos do click. Veja esse exemplo:

```javascript
const anchor = document.getElementById('anchor-link');

anchor.addEventListener('click', event => {
    // Essa chamada de função impede que o click na âncora redirecione o usuário para outra página.
    event.preventDefault();
});
```

O exemplo acima descreve exatamente a situação de um link que, quando clicado, não faz nada \(ao invés de redirecionar o usuário\). Isso é extremamente útil, porquê agora nós podemos fazer o que quisermos quando o usuário clicar nesse link. Veja agora um exemplo mais realista:

```javascript
const anchor = document.getElementById('anchor-link');

anchor.addEventListener('click', event => {
    // Não implementamos essas funções, mas fingimos que elas existem em outro lugar.
    if (!isUserLoggedIn() || !doesUserHaveAccesstToPage()) {
        // Mostra uma mensagem para o usuário, e impede o redirecionamento do browser.
        alert ('Você não tem acesso a essa página!');
        event.preventDefault();
    }
});
```

Aqui, nós verificamos se o usuário tem permissão de acessar uma página antes de permitir ele de realizar esse acesso.

### Uma peculiaridade dos eventos de teclado

Alguns eventos tem um disparo bastante óbvio. Por exemplo, ao clicar num botão, o evento "`click`" é disparado no botão. Entretanto, eventos de teclado dependem de um requisito mais sutil: foco.

O conceito de foco na web significa qual elemento receberá as ações de teclado do usuário. Quando você clica num elemento, ele automaticamente ganha foco. Um elemento com foco receberá todos os eventos de teclado do usuário. Esse é o motivo do porquê você precisa clicar num campo de texto para começar a digitar nele.

Quando o usuário clica em um segundo elemento, o primeiro elemento perde o foco \(evento denominado "`blur`"\), e o segundo elemento ganha foco \(evento denominado "`focus`"\). Assim, o primeiro elemento para de receber os eventos de teclado do usuário, enquanto o segundo elemento começa a receber esses próximos eventos.

Outra maneira de se adquirir foco num elemento é através da tecla `tab`. Quando você aperta `tab` numa página, o browser começa a selecionar, em ordem de cima para baixo e da esquerda para a direita, todos os elementos possíveis.

Por fim, é possível forçar um elemento a adquirir foco por JavaScript, através da função `focus()` de um elemento, como no exemplo:

```javascript
const button = document.getElementById('button-id');
// Sempre que a função "focus" de um elemento é chamada, ele ganha foco.
button.focus();
```

### Removendo _Event Listeners_

Já aprendemos a adicionar _Event Listeners_, mas as vezes precisamos poder remover eles. Para isso, usamos a função `removeEventListener`. Veja o exemplo:

```javascript
const button = document.getElementById('button-id');

function sayHi () { console.log('hi') }

// Adiciona o Event Listener
button.addEventListener('click', sayHi);

// Remove o Event Listener
button.removeEventListener('click', sayHi);
```

Basta chamar a função `removeEventListener` no objeto, com o primeiro argumento sendo o tipo do evento que você quer remover \(no caso, um evento de 'click'\), e o segundo argumento a função que você usou para ser executada com esse evento \(no caso, a função "`sayHi`"\).

### Duas outras formas de se ouvir por eventos

Existem duas outras formas de se escutar por eventos no JavaScript, mas que são desencorajadas.

#### Por atributos no HTML

Todas as tags HTML podem receber um atributo para cada evento, com o nome da função em JavaScript para ser executada quando o evento acontece. Veja esse exemplo:

```markup
<!-- index.html -->
<html>
    <body>
        <p>Um site qualquer</p>

        <!-- O atributo "onclick" é responsável por ouvir pelo evento de click -->
        <button onclick="sayHi()">Dizer oi</button>
    </body>
    <script src="index.js"></script>
</html>
```

```javascript
// index.js

// Função que será executada quando o botão for clicado.
function sayHi () {
    alert('hi');
}
```

Veja que, no exemplo acima, o botão tem um atributo "`onclick`", que recebe uma string "`sayHi()`". Isso indica que, quando o evento de click acontecer no botão, a função "`sayHi`", que foi definida no arquivo `index.js`, será chamada. Isso é válido pra qualquer atributo que começa com "on" e termina com o nome de um evento \(ex: "`onmousedown`", "`onkeydown`", "`onload`", etc...\). A função que é chamada também pode ter qualquer nome, contanto que ela seja definida por algum `script`.

Essa forma de se ouvir por eventos não é muito recomendada por três principais motivos:

1. **Requer que a sua função de eventos esteja declarada no escopo global**: Com código modular o suficiente, é possível \(e até bastante provável\) que nós queiramos registrar funções não globais a nossos eventos. Além disso, se você começar a declarar todas as suas funções de eventos no escopo global, é bem possível que a você acabe dando o mesmo nome pra duas funções diferentes, causando bugs difíceis de encontrar.
2. **Dificulta remover o** _**Event Listener**_ **no futuro**: As vezes, queremos poder remover funções que estão ouvindo por eventos \(como mostrado acima\). Com essa forma de _Event Listeners_, bem mais difícil de remover.
3. **Menos suporte de sua IDE**: A maioria das ferramentas modernas de desenvolvimento web tem funções que permitem verificar quando você está cometendo um claro erro \(ex: referenciando uma variável inexistente\). Essa verificação não é muito bem feita quando você usa eventos por atributos, porquê é muito difícil da sua IDE saber exatamente quais funções são visíveis para os eventos dos elementos HTML. Então, se você errar o nome da função, ou o nome do atributo do evento, a sua IDE não tem como te ajudar.

#### pela propriedade `oneventname`

Os objetos DOM no JavaScript possuem uma propriedade para cada evento. Veja esse exemplo:

```javascript
// Seleciona um elemento com id "button-id"
const button = document.getElementById('button-id');

// Função que será chamada quando o evento "click" acontecer
function sayHi () {
    console.log('hi');
}

// Aqui, a função "sayHi" é atribuida como Event Listener
button.onclick = sayHi;
```

Aqui, ao invés de adicionar o _Event Listener_ através da função `addEventListener`, nós simplesmente atribuímos a função para a propriedade `onclick` do botão. Quando o botão é clicado, ele verifica se há uma função em sua propriedade `onclick`, e se tiver, ele a executa. Isso também funciona com outras propriedades de outros eventos. Mais especificamente, qualquer propriedade que começa com "`on`" e termina com o nome de um evento \(ex: "`onmousedown`", "`oufocus`", "`oukeydown`", etc...\).

Esse método pode parece mais simples, mas tem um problema fatal: **Permite apenas um** _**Event Listener**_ **por tipo de evento**. Com o `addEventListener`, nós podemos adicionar quantos eventos do mesmo tipo quisermos. Entretanto, com esse método só conseguimos adicionar um por vês, pois subsequentes tentativas sobrescrevem os eventos anteriores. Veja esse exemplo:

```javascript
const button = document.getElementById('button-id');

// Adiciona um Event Listener
button.onclick = () => alert("Fui clickado");

// Sobrescreve o primeiro Event Listener com um novo.
button.onclick = () => alert("Fui clickado de novo");
```

No código acima, clickar no botão resulta em apenas a mensagem "Fui clickado de novo" aparecer num alert para o usuário. Em projetos maiores, com muitos eventos acontecendo, é bem comum sobrescrever, sem querer, alguns eventos usando esse método, e não há nenhuma forma de permitir dois eventos no mesmo tipo do objeto. Isso pode ser uma fonte de bugs bastante difícil de encontrar.

### Alguns dos eventos mais conhecidos

Existem centenas de diferentes tipos de eventos \(você pode ver uma lista [aqui](https://developer.mozilla.org/en-US/docs/Web/Events)\), mas alguns são mais usados que outros. Aqui vai uma lista dos mais famosos, para que você tenha uma ideia do que pode ser feito com _Event Listeners_:

* `click` - Dispara quando um elemento é clicado com o botão esquerdo do mouse.
* `mousedown` - Dispara quando algum botão do mouse é pressionado sobre o elemento.
* `mouseup` - Dispara quando algum botão do mouse é solto sobre o elemento.
* `mousemove` - Dispara quando o cursor do usuário se você sobre o elemento.
* `keydown` - Dispara quando o usuário pressiona alguma tecla do teclado com o elemento em foco.
* `keyup` - Dispara quando o usuário solta alguma tecla do teclado com o elemento em foco.
* `focus` - Dispara quando o elemento ganha foco.
* `blur` - Dispara quando o elemento perde foco.
* `load` - Dispara quando o elemento é carregado \(mais usado em imagens, para detectar quando a imagem terminou de carregar\).
* `submit` - Dispara quando um formulário é submetido.
* `input` - Dispara quando uma caixa de texto recebe um novo valor.

Lembrando que eventos diferentes podem ter objetos de eventos diferentes, que contém informações diferentes. Os eventos relacionados ao mouse contém informações sobre a posição do mouse, e quais botões estão pressionados. Os eventos relacionados ao teclado contém informações sobre quais teclas estavam pressionadas. E cada um dos demais eventos tem as suas informações especificas.

### _Event Bubbling_

#### O que é _Event Bubbling_

Os eventos na web raramente são disparados em um só elemento. Em geral, um click do usuário dispara vários eventos de "`click`" em múltiplos elementos. Isso acontece por causa de um comportamento chamado _Event Bubbling_. Esse termo significa que quando um evento é disparado em um elemento, esse elemento primeiro processa o evento \(chama todos os _Event Listeners_ que foram criados com o "`addEventListener`"\), para depois disparar o mesmo evento para o elemento pai. Esse processo acontece recursivamente até atingir o elemento raiz do documento \(normalmente a tag "`<html>`"\). Veja esse exemplo:

```markup
<!-- index.html -->
<html id="html-id">
    <body id="body-id">
        <div id="div-id">
            <button id="botao-id">Botão</button>
        </div>
    </body>
    <script src="index.js"></script>
</html>
```

```javascript
// index.js
const htmlElem = document.getElementById('html-id');
const bodyElem = document.getElementById('body-id');
const divElem = document.getElementById('div-id');
const botaoElem = document.getElementById('botao-id');

htmlElem.addEventListener('click', () => console.log('click no html'));
bodyElem.addEventListener('click', () => console.log('click no body'));
divElem.addEventListener('click', () => console.log('click na div'));
botaoElem.addEventListener('click', () => console.log('click no botão'));
```

O código acima simplesmente adiciona um _Event Listener_ a cada elemento da página, que chama um `console.log` com o nome do elemento.

Quando o usuário clicar no botão, o primeiro elemento que receberá o evento de click é o botão. O botão então vai processar o evento, isto é, executar todos os _Event Listener_ que estiverem ouvindo pelo evento de "`click`". É nesse ponto que o primeiro `console.log` será chamado, e a mensagem "`cick no botão`" deve aparecer no console. Após executar todos os _Event Listeners_ do botão, o exato mesmo evento será disparado no elemento pai \(nesse caso, o elemento _div_\). O exato mesmo processo acontecerá com o elemento _div_: primeiro os _Event Listeners_ são processados \(vemos então a mensagem "`click na div`" no console\), e o evento é então disparado no evento pai da _div_, que nesse caso é o elemento _body_. Esse processo acontecerá até chegar no elemento _html_, que é a raiz do documento.

Assim, após o click do usuário, devemos ter como resultado no console a seguinte ordem de mensagens:

```text
> "click no botão"
> "click na div"
> "click no body"
> "click no html"
```

Todo esse processo é chamado _Event Bubbling_, e ele acontece com a maioria dos eventos, não só com clicks. Existem alguns eventos que não sofrem esse processo \(mais notáveis os eventos de "`focus`", "`blur`" e "`change`"\), mas a grande maioria dos eventos é afetada por _Bubbling_.

Com esse conhecimento, se quisermos capturar qualquer tecla que o usuário pressionar, seria necessário apenas criar um _Event Listener_ de teclas na raiz do documento \(normalmente o elemento "`<html>`"\), ao invés de criar um _Event Listener_ pra cada elemento do documento.

#### Como impedir um evento de sofrer _Bubbling_

É uma situação bem rara, mas é possível que seja desejável impedir um evento de sofrer _Bubbling_ \(impedir o evento se ser disparado no pai do elemento\). Para isso, o objeto de eventos possui uma função especial: `stopPropagation`. Veja esse exemplo:

```markup
<!-- index.html -->
<html id="html-id">
    <body id="body-id">
        <div id="div-id">
            <button id="botao-id">Botão</button>
        </div>
    </body>
    <script src="index.js"></script>
</html>
```

```javascript
// index.js
const htmlElem = document.getElementById('html-id');
const bodyElem = document.getElementById('body-id');
const divElem = document.getElementById('div-id');
const botaoElem = document.getElementById('botao-id');

htmlElem.addEventListener('click', () => console.log('click no html'));
bodyElem.addEventListener('click', () => console.log('click no body'));
divElem.addEventListener('click', event => {
    console.log('click na div');
    event.stopPropagation();
});
botaoElem.addEventListener('click', () => console.log('click no botão'));
```

Aqui, todos os elementos do documento recebem um _Event Listener_ que simplesmente imprime o nome do elemento no console, com exceção da _div_, que além de imprimir algo no console, também faz uma chamada pra função `stopPropagation` do objeto de eventos. Isso impede o evento de subir para o pai da _div_, o que impede o evento de "`click`" de disparar nos elementos _body_ e _html_. Assim, a saída do console deve ser algo assim:

```text
> "click no botão"
> "click na div"
```

### Resumo

Aqui, tivemos uma introdução extensa sobre eventos, que discutiu os seguintes tópicos:

1. O que são eventos
2. O objeto de eventos
3. Como remover _Event Listeners_
4. Outras formas \(não recomendadas\) de se criar _Event Listeners_
5. Os eventos mais conhecidos
6. O que é _Event Bubbling_, e como impedir esse processo.

