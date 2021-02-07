---
description: 'O que é o Event Loop, e como ele funciona'
---

# Event Loop

### O que é o _Event Loop_?

Um dos principais fatos sobre o JavaScript é que é uma linguagem inerentemente _Single Thread_ \(tradução: _Fio único_\), isto é, em qualquer instante apenas um comando pode estar sendo executado ao mesmo tempo. Essa é uma das características principais da linguagem, independente de onde ela esteja sendo executada. Além disso, o JavaScript é um linguagem _Assíncrona_, isto é, a ordem de execução das funções não é sempre bem definida. Isso quer dizer que dependendo de como o código for escrito, cada execução do código pode ter uma ordem diferente de execução de suas funções.

Como o JavaScript é _Single Thread_ e _Assíncrono_, apenas uma função pode estar sendo executada em qualquer momento, mas a ordem de execução delas deve ser definida durante a execução do código. Assim, o _Event Loop_ \(tradução: _Ciclo de Eventos_\) é o mecanismo que o JavaScript usa para escolher qual será a próxima função a ser executada.

### O problema

Numa página web, quase sempre que o usuário faz uma ação, a interface deve ser atualizada de alguma forma. Seja para mudar a cor de um link que foi visitado, ou para descer o _scroll_ da página. Entretanto, em todos os _browsers_ modernos, a interface não pode ser atualizada enquanto houver código JavaScript sendo executado, e não se pode executar código JavaScript enquanto a interface estiver sendo atualizada \(os dois não podem ser feitos ao mesmo tempo\).

Assim, se nosso código JavaScript for muito demorado, a tela do usuário ficara travada e irresponsiva, causando uma péssima experiência. Veja um exemplo de código que tem esse comportamento:

```markup
<html>
    <body>
        <button onClick="click()">Click me!</button>
        <script>
            function click () {
                // Função ficticia que faz uma requisição HTTP para um servidor.
                fetchDataFromServer();

                alert('Operação terminada!');
            }
        </script>
    </body>
</html>
```

No exemplo acima, quando o usuário clickar no botão, toda a interface ficará travada até a função "`click`" terminar, o que pode demorar múltiplos segundos

### A solução

Para mitigar o problema descrito acima, foi-se desenvolvida a ideia de "agendar" a execução de funções num momento futuro, liberando o _browser_ para atualizar a interface do usuário, ou executar outras partes do código JavaScript.

No caso do exemplo descrito no problema, a maior parte da "demora" numa requisição HTTP vem da espera pela resposta, e enquanto se espera por essa resposta outra parte do código poderia estar sendo executada, ou a interface do usuário poderia estar sendo atualizada. Outro exemplo parecido é num temporizador, onde uma função só deve ser executada depois de uma quantidade determinada de tempo. Enquanto se espera para executar essa função, o _browser_ poderia ser liberado para terminar outras tarefas.

Assim, algumas funções disponibilizadas pelo _browser_ recebem outras funções como argumento \(também conhecidas como _Callbacks_\), que serão executadas apenas quando a operação da primeira função terminar. Veja esse exemplo:

```markup
<html>
    <body>
        <button onClick="click()">Click me!</button>
        <script>
            function timerEnded () {
                alert('O temporizador acabou!');
            }

            function click () {
                // Espera 5 segundos para executar a função "timerEnded"
                setTimeout(timerEnded, 5000);
            }
        </script>
    </body>
</html>
```

Aqui, quando o usuário clickar no botão, o código vai esperar 5 segundos para mostrar um alerta. Enquanto esse tempo passa, a interface do usuário não ficara travada ou irresponsiva. Isso é porque a função "`setTimeout`" apenas "agenda" a execução da sua _callback_ para quando o temporizador de 5 segundos terminar.

Veja esse outro exemplo, mas dessa vez fazendo uma requisição.

```markup
<html>
    <body>
        <button onClick="click()">Click me!</button>
        <script>
            function responseTextFinished (responseText) {
                alert(responseText);
            }

            function responseReceived (response) {
                // Tenta extrair o texto da requisição HTTP
                response.text().then(responseTextFinished);
            }

            function click () {
                // Faz uma requisição HTTP
                fetch('https://my-server-url.com').then(responseReceived);
            }
        </script>
    </body>
</html>
```

Este é um exemplo um pouco mais complicado, mas que essencialmente faz a mesma coisa que o temporizador. Nesse caso, o código faz uma requisição para um servidor, e agenda a função "`responseReceived`" para ser executada quando uma resposta do servidor for recebida. Essa função, por sua vez, tenta extrair o corpo da resposta na forma de texto, e agenda a função "`responseTextFinished`" para ser executada quando esse texto estiver pronto. Durante todo esse processo, enquanto essas operações estavam sendo feitas, o _browser_ estava livre para atualizar a interface do usuário.

### Como funciona

#### As ferramentas

Para gerenciar as operações e funções agendadas, o browser usa três construtos: a "_Call Stack_", as "_Web APIs_" e a "_Queue_".

A _Call Stack_ \(tradução: _Pilha de chamadas_\) é uma pilha de funções que estão sendo executadas no atual instante. Quando uma função do JavaScript é chamada, ela é posta no topo da _Call Stack_. Quando uma função do JavaScript termina de executar, ela é removida da _Call Stack_. Se a _Call Stack_ estiver vazia, quer dizer que nenhuma função está sendo executada no momento.

As _Web APIs_ são funções especiais que realizam tarefas complexas por trás dos panos. A maior parte dessas funções são implementadas de forma que utilizam eficientemente os recursos do computador. Essas funções não pertencem ao JavaScript em si, mas são disponibilizadas pelo ambiente de execução \(no nosso caso, o _browser_\). Exemplos de _Web APIs_ são: "`fetch`", "`setTimeout`" ou "`setInterval`". Você pode ver uma lista das _Web APIs_ mais amplamente implementadas nos _browsers_ modernos [aqui](https://developer.mozilla.org/en-US/docs/Web/API).

A _Queue_ \(tradução: _Fila_\) é uma fila de _callbacks_ que estão prontas para serem imediatamente executadas, mas que ainda estão aguardando uma oportunidade.

#### O fluxo

Tudo começa com a primeira execução do código JavaScript. Primeiro, o código que está escrito na página é embrulhado numa grande função e posto no início da _Call Stack_. Como a _Call Stack_ é a pilha que define qual função está sendo atualmente executada, o código fonte é executado, linha a linha.

Eventualmente, algumas linhas fazem chamadas a algumas _Web APIs_. Por exemplo, podem-se ter sido feitas chamadas de `setTimeout`, ou `fetch`. Essas _Web APIs_ sempre recebem uma _callback_ e alguns outros parâmetros. Essas _callbacks_ vão ser "guardadas" até que a _Web API_ termine a sua tarefa. Uma vez que essa tarefa é terminada, a sua callback é imediatamente enviada para o fim da _Queue_.

Por último vem o trabalho do _Event Loop_. Pode-se pensar nele como um _loop_ infinito que constantemente verifica se a interface do usuário precisa ser atualizada, se há algo na _Queue_ esperando para ser executado, e se a _Call Stack_ está vazia. A sua lógica pode ser bem descrita de acordo com o seguinte pseudo-código:

```javascript
function eventLoop () {
    while (true) {
        // Sempre antes de olhar para a Queue, verifica se a interface precisa ser atualizada.
        if (shouldUpdateUserInterface()) updateUserInterface();

        // Apenas age se houver elementos na Queue e se a callStack esiver vazia.
        if (queue.isNotEmpty() && callStack.isEmpty()) {
            // Transfere o elemento do início da Queue para a Call Stack.
            queue.sendFirstElementToCallStack();

            // Executa a função no topo da Call Stack.
            // Note que quando essa função terminar de executar, ela será automaticamente removida da Call Stack, deixando-a vazia de novo.
            callStack.executeFunctionOnTop();
        }
    }
}
```

#### Um exemplo simples

Considere o código abaixo:

```javascript
console.log('Início');

function sayHi () {
    console.log('Oi!');
}

// Agenda a função "sayHi" para executar em 5 segundos
setTimeout(sayHi, 5000);

console.log('Fim do código principal');
```

Nesse exemplo, a primeira coisa que acontece é o código ser imediatamente movido para a _Call Stack_, e ser imediatamente executado. Assim, a primeira linha imprime a palavra "Início". Na terceira linha, declaramos a função "`sayHi`". Na oitava linha, fazemos uma chamada para a _Web API_ "`setTimeout`", que agenda a _callback_ "`sayHi`" para ser executada em 5 segundos. Por fim, na décima linha, imprime-se a string "Fim do código principal".

Ao finalizar a execução desse código, a _Call Stack_ ficará vazia, e o _Event Loop_ começará o seu trabalho de constantemente verificar se há algo na _Queue_, pronto para mover para a _Call Stack_. Nesse caso, a única coisa que o nosso código ainda está fazendo é esperar a _Web API_ do "`setTimeout`" terminar a contagem do temporizador de 5 segundos, enquanto a _Call Stack_ e a _Queue_ ficam vazias. Logo, pelos próximo 5 segundos, nada acontece.

Passados os 5 segundos, a _Web API_ do "`setTimeout`" termina o seu trabalho e move a _callback_ "`sayHi`" para a _Queue_. O _Event Loop_, que durante todo este tempo estava esperando algo aparecer na _Queue_, finalmente vê que a _Call Stack_ está vazia e que há algo na _Queue_. Assim, o _Event Loop_ move a _callback_ "`sayHi`" da _Queue_ para a _Call Stack_ e a executa.

Finalmente, com a função "`sayHi`" na _Call Stack_ e sendo executada, o `console.log` da linha 4 é executado, e a string "Oi!" aparece no _console_. Assim, a impressão final deste código é:

```text
Início
Fim do código principal
Oi!
```

#### Um exemplo mais complicado

```javascript
console.log('Início');

// simpleFetch é uma função fictícia (não existe).
// Apenas imagine que ela faz uma requisição HTTP.

simpleFetch ('http://my-server.com', () => console.log('Requisição 1 concluída'));
simpleFetch ('http://my-server.com', () => console.log('Requisição 2 concluída'));
simpleFetch ('http://my-server.com', () => console.log('Requisição 3 concluída'));

console.log('Fim do código principal');
```

Neste exemplo fazemos 3 requisições HTTP diferentes para o nosso servidor, imprimindo uma string única ao terminar. O processo básico é o mesmo:

* Código movido para a _Call Stack_, com sua execução iniciada.
* As três requisições HTTP são iniciadas \(através de uma _Web API_, com suas respectivas _callbacks_.
* A execução do código principal termina, e a _Call Stack_ fica vazia.
* As requisições terminam, e suas _callbacks_ são movidas para a _Queue_.
* O _Event Loop_ move as _callbacks_ da _Queue_ para a _Call Stack_, e inicia a sua execução.

Mas nesse exemplo há algo de mais interessante: são três requisições acontecendo ao mesmo tempo, sem ter ideia de qual vai acabar primeiro. É possível que as duas primeiras levem 3 segundos enquanto a terceira leve 15 segundos. É possível que todas terminem no mesmo exato momento. É possível que uma termine enquanto a _callback_ da outra está sendo executada. São inúmeras possibilidades.

Em casos como esse, quem terminar primeiro poderá empurrar a sua _callback_ para a _Queue_ primeiro. E a ordem de execução das _callbacks_ é a ordem de chegada delas na _Queue_. Mesmo que as três requisições terminem ao mesmo tempo, alguma delas será tratada primeiro, enquanto a _callback_ da outras espera na _Queue_ a _Call Stack_ se liberar.

### Resumo

Neste capítulo, vimos:

* Os tipos de problemas que inspiraram a invenção do _Event Loop_
* A solução dos problemas, usando _Web APIs_.
* Como o _Event Loop_ funciona
* Alguns exemplos de códigos que usaram _Web APIs_.

