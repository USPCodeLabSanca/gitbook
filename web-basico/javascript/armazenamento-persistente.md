---
description: Como guardar dados que não se perdem quando o usuário sai da página
---

# Armazenamento persistente

## O que é armazenamento persistente?

Sempre que o usuário recarrega a página ou fecha o browser, todo o código JavaScript para completamente de executar, e toda a memória que foi utilizada por ele é limpa, apagando todos os valores de todas as variáveis que existiam. Esse comportamento é essencial para permitir que o usuário acesse várias páginas sem faltar memória em seu computador, mas as vezes as aplicações precisam salvar dados que não serão perdidos quando o usuário for embora. É esse problema que as tecnologias de armazenamento persistente tentam resolver.

O termo "armazenamento persistente" significa, essencialmente, um espaço de memória que é preservado quando o usuário fecha a aplicação. Para isso, temos três principais soluções: _Cookies_, _Local Storage_ e _Session Storage_. Cada uma dessas soluções tem um comportamento diferente, que iremos explorar nesse capítulo.

## Para o que é usado armazenamento persistente?

Há vários casos de uso para essa tecnologia. Um exemplo é o login de usuários. Quase qualquer plataforma nos permite fazer login apenas no primeiro acesso, sem ter que fazer login de novo toda vez que abrimos a página. Isso só é possível por causa de armazenamento persistente. Outro exemplo é alguns sites que permitem o usuário modificar o seu visual para melhorar a sua experiência \(ex: ativar o modo escuro\). Esses sites salvam as preferências do usuário em uma memória persistente, para que as configurações sejam aplicadas todas as vezes que o usuário voltar para a página. Por fim, mais um exemplo de uso para essa tecnologia é lembrar quais foram os acessos prévios desse usuário, para poder tentar recomendar produtos parecidos com o que ele viu anteriormente \(processo de _User Tracking_\).

Existem infinitas outras aplicações para armazenamento persistente que não foram mencionadas, e isso só mostra o quão importante essa tecnologia é para a web moderna.

## Formas de armazenamento persistente

### _Local Storage_

Esse método de armazenamento é essencialmente apenas uma tabela com chaves e valores. As funções de acesso a esse recurso estão na variável `localStorage`. Veja esse exemplo:

```javascript
// Escreve um valor no Local Storage.
localStorage.setItem('nome-do-item', 'valor-do-item');

// Lê um valor do Local Storage.
localStorage.getItem('nome-do-item'); // valor-do-item

// Deleta um valor do Local Storage.
localStorage.removeItem('nome-do-item');
```

O único tipo de dado que pode ser inserido no _Local Storage_ é a String. Caso você queira guardar outros tipos de dados, é necessário transforma-los em string primeiro. No caso de um objeto, pode-se usar a função `JSON.stringify` para transformara-los em string, e `JSON.parse` para transformar uma string \(no formato JSON\) em um objeto.

O _Local Storage_ de cada domínio é completamente isolado um do outro. Isto é, o _Local Storage_ da página "google.com" não tem acesso aos dados que foram gravados na página "youtube.com", e vice-versa. Entretanto, páginas com o mesmo domínio, mas caminhos diferentes tem acesso aos mesmos dados, isto é, scripts na página `meu-site.com/home` tem acesso aos dados gravados pela página `meu-site.com/contato`.

O _Local Storage_ não tem nenhuma forma de controle de acesso aos seus dados. Qualquer script executando na sua página tem acesso ao que está no _Local Storage_. Os dados do _Local Storage_ não tem uma data de expiração, e vão persistir até o usuário limpar a cache ou o Browser decidir que os dados são muito velhos e podem ser deletados.

**Limitações**

O _Local Storage_ pode guardar até 5 MB de informação, independente da quantidade de chaves e valores. Esse valor pode ser configurado pelo browser do cliente.

### Session Storage

Esse método é idêntico ao _Local Storage_, com exceção de que os dados guardados aqui vão expirar assim que a sessão do seu site for encerrada, isto é, quando o browser do seu usuário for fechado, os dados que foram salvos no _Session Storage_ serão deletados.

Essa API é acessada pela variável `sessionStorage`. Veja o exemplo:

```javascript
// Escreve um valor no Session Storage.
sessionStorage.setItem('nome-do-item', 'valor-do-item');

// Lê um valor do Session Storage.
sessionStorage.getItem('nome-do-item'); // valor-do-item

// Deleta um valor do Session Storage.
sessionStorage.removeItem('nome-do-item');
```

Todas as considerações discutidas na sessão do _Local Storage_ são válidas aqui.

**Limitações**

As limitações do _Session Storage_ são as mesmas do _Local Storage_

### Cookies

Essa foi a primeira solução desenvolvida pela web para persistir dados. Cookies se resumem a uma única string que pode ser acessada pela variável "`document.cookie`". Veja um exemplo dessa string:

```javascript
console.log(document.cookie);
// "nome1=valor1; nome2=valor2; nome3=valor3"
```

O valor de `document.cookie` é uma string, composta por um conjunto de pares valor-chave com a sintaxe "`valor=chave`". Os pares valor-chave são separados pelo caractere ";" e podem ou não ter um espaço depois do ";" \(depende do browser\).

Para ler o valor dos cookies, é preciso manipular a string do `document.cookies`. Por exemplo:

```javascript
function getCookie (cookieName) {
    return document.cookie
        // Separa todos os valores de cookies
        .split('; ')
        // Encontra o par valor-chave com o nome certo.
        .find(row => row.startsWith(cookieName))
        // Extrai o valor do cookie.
        .split('=')[1];
}

console.log(getCookie('nome1')); // "valor1"
```

Para se escrever um novo valor nos _Cookies_, é necessário apenas atribuir o novo valor ao `document.cookie`, como por exemplo:

```javascript
// Escreve um novo par chave-valor no cookie. Note que isso não sobrescreve
// os cookies antigos, apenas adiciona um par novo.
document.cookie = "novoNome=novoValor"
```

Note que, apesar de estarmos atribuindo uma nova string à variável `document.cookie`, não estamos sobrescrevendo todos os cookies da página, e sim criando um único novo cookie. Ao atribuir uma string à variável `document.cookie` só é possível modificar um único cookie por vez. Assim, se tivermos dois cookies já na página, e escrevermos `document.cookie = "novoNome=novoValor"`, não vamos sobrescrever os cookies anteriores.

Além de uma chave e um valor, cookies também tem alguns valores especiais chamados "atributos". Esses valores são usados pra indicar quem pode acessar esse _Cookies_, e até quando eles são válidos. Um dos atributos mais famosos se chama "Max-Age". Esse atributo controla o tempo \(em segundos\) de expiração do cookie, isto é, por quanto tempo esse cookie é válido. Quando esse tempo acaba, o cookie é automaticamente deletado. Veja esse exemplo:

```javascript
// Escreve um cookie que vai durar 10 segundos
document.cookie = "novoNome=novoValor; Max-Age=10"
```

Para se criar um atributo em um _Cookie_, é preciso adicionar um ";" logo depois do valor deste, e especificar o atributo como outro par valor-chave, como exemplificado acima. Múltiplos atributos podem ser atribuídos ao mesmo tempo, basta separa-los por "`;`".

Caso um _Cookie_ seja criado sem um atributo `Max-Age`, e sem um atributo `Expires` \(que não vimos ainda, mas será comentado sobre em breve\) será guardado apenas durante a sessão atual do seu site, isto é, apenas enquanto pelo menos uma aba do seu site ainda estiver aberta. Caso o usuário feche todas as abas e janelas do seu site, os _Cookies_ criados sem uma data de expiração são deletados.

A única forma de se deletar um _Cookie_ é forçando ele a expirar, como por exemplo:

```javascript
// O cookie com o nome `cookieParaDeletar` vai expirar instantâneamente (em zero segundos),
// efetivamente deletando ele.
document.cookie = "cookieParaDeletar=valor; Max-age=0"
```

Assim como os dados do _Local Storage_, os _Cookies_ de um domínio não podem ser acessados por outro domínio \(a não ser que explicitado através do atributo "Domain", que veremos em breve\), isto é, os _Cookies_ da página "google.com" não podem ser acessados pela página "youtube.com". Entretanto, páginas dentro de um mesmo domínio, mas com caminhos diferentes, tem acesso aos mesmos _Cookies_.

**Uma peculiaridade dos Cookies**

Toda requisição HTTP feita para um domínio envia no header "Cookie" a string do `document.cookie`, E toda resposta do servidor desse domínio pode conter um header "Set-Cookie", que vai escrever _Cookies_ no browser do seu usuário. Em sumo, o servidor que serve o seu site pode ler e escrever cookies no browser do seu usuário.

Esse comportamento foi implementado para permitir que alguns sites que utilizam tecnologias como _PHP_ consigam guardar dados sobre o usuário no próprio browser do usuário, podendo então identificar o usuário através desses _Cookies_. É um comportamento não opcional \(sempre vai acontecer\) e sempre envia **todos** os cookies.

**Limitações**

Há um limite de 4 KB de informação para cada _Cookie_, e um máximo de 50 cookies por domínio, totalizando 200 KB máximos que podem ser guardados num único domínio.

**Atributos mais comuns**

Aqui são os atributos mais comuns usados com os `Cookies`:

* **Expires:** Define uma data para o _Cookie_ expirar. Exemplo:

```javascript
const expiração = new Date('2020-11-08 15:30');
// Cria um cookie chamado Batata que exipira na data guardada em expiração.
document.cookie = "batata=tomate; Expires=" + expiração.toString();
```

* **Max-Age:** Número de segundo para o _Cookie_ expirar, a partir de quando ele é criado. Exemplo de um cookie que expira em 10 segundos: `document.cookie = "batata=tomate; Max-Age=10"`
* **Domain:** O domínio que pode acessar esse _Cookie_. Se nenhum domínio é especificado, usa o domínio do site atual, sem incluir subdomínios, logo uma página servida por "outro-site.meu-site.com" não teria acesso aos _Cookies_ de "meu-site.com" que não especificaram nenhum domínio no atributo `Domain`. Se um domínio foi especificado, então todos os subdomínios serão incluídos, isto é, um cookies atribuído para o domínio "meu-site.com" poderia ser acessado pelo "outro-site.meu-site.com". Um exemplo: `document.cookie = "batata=tomate; Domain=meu-site.com"`
* **Path:** O caminho do site que tem acesso a esse _Cookie_. Se especificar algo como `document.cookie = "batata=tomate; Path=/about"`, o _Cookie_ poderá só ser acessado por páginas no dentro do caminho "/about" \(exemplo: "/about", "/about/something" ou "/about/something/cool" terão acesso.\).
* **Secure:** Um _Cookie_ com atributo `Secure` só será enviado para o servidor se estiver sendo usado HTTPS, e não HTTP. Exemplo: `document.cookie = "batata=tomate; Secure"`
* **HttpOnly:** Um _Cookie_ com o atributo `HttpOnly` não pode ser acessado pelo JavaScript de nenhuma página, consequentemente ele só ser lido pelo servidor, através do header "Cookie" das requisições HTTP. Exemplo: `document.cookie = "batata=tomate; HttpOnly"`
* **SameSite:** Esse atributo especifica a política usada para decidir quando um _Cookie_ é enviado do browser do usuário para o servidor. Ele pode ter os seguintes valores:
  * **Strict:** O _Cookie_ só é enviado quando o usuário está no seu domínio que contém ele. Então, se houver um _Cookie_ com o atributo `SameSite` como `Strict` no domínio "meu-site.com", ele só será enviado para o servidor se o usuário estiver visualizando atualmente o "meu-site.com"
  * **Lax:** O mesmo que o `Strict`, mas o _Cookie_ também é enviado quando o usuário vai visitar o domínio a partir de um link externo.
  * **None:** Nenhum restrição. O _Cookie_ é enviado em todas as requisições feitas para o seu domínio, independente de onde o usuário estiver.

## Tantas opções, qual escolher?

Cada uma dessas opções tem suas vantagens e desvantagens, e sua escolha vai geralmente depender do tipo de dado que você quer guardar.

### _Cookies_

_Cookies_ são bastante difíceis de manipular no browser, tanto na leitura quanto na escrita. As operações ao redor do `document.cookie` dependem de muita manipulação de strings, que abrem margem para possíveis bugs. Além disso, as limitações dos _Cookies_ são mais restritas que as do _Local Storage_ e do _Session Storage_.

Entretanto, há um mecanismo implementado para os _Cookies_ que não tem equivalente para as outras opções: os atributos. Os atributos dos _Cookies_ permitem um controle bem maior sobre quem consegue acessar o que. Isso é extremamente importante quando estamos lidando com dados sensíveis dos nossos usuários, que não devem ser acessados por ninguém além do usuário em si.

A configuração ideal é sempre usar _Cookies_ com o atributo `Secure` ligado e com o `SameSite` valendo `Lax` ou `Strict`. Caso seja um dado que só o servidor precisa ler, o atributo `HttpOnly` deve também ser ligado. Essas configurações ajudam a mitigar os efeitos de alguns ataques muito comuns na web, como por exemplo XSS \(Cross Site Scripting\) e CSRF \(Cross Site Request Forgery\). Esses ataques não serão estudados agora, mas é importante

### _Local Storage_

Em contraste aos _Cookies_, o _Local Storage_ é mais simples de usar, e consegue guardar mais informações. Entretanto, como não há limitações sobre os seus recursos, qualquer script que executa na sua página tem acesso ao _Local Storage_, e pode ler e escrever nesses dados. Isso pode ser perigoso caso alguém consiga executar algum script malicioso na sua página \(através de técnicas como XSS\), e pode ser a causa de vazamento de dados de muitos usuários. Logo, o _Local Storage_ é ideal para guardar dados não sensíveis, como por exemplo a preferências de um usuário na página \(se ele prefere tema claro ou escuro, o volume em que ele deixa os vídeos etc.\).

### _Session Storage_

As vantagens e desvantagens do _Session Storage_ são idênticas às do _Local Storage_, com exceção do fato de que seus dados são mais frequentemente deletados. Por isso o _Session Storage_ tem esse nome: os dados guardados nele são geralmente relacionados a sessão do usuário. Uma "Sessão" é uma visita do usuário à sua página, então os dados de uma sessão costumam ser válidos até quando o usuário fechar a página. Alguns exemplos desses dados são os itens dentro de um carrinho de compras, ou a página do produto que o usuário estava vendo.

## Resumo do conteúdo

Aqui abordamos como guardar dados que persistem o recarregar da página. Para isso, vimos três soluções: _Cookies_, _Local Storage_ e _Session Storage_. Cada uma tem a sua forma de ser acessada, e possui suas vantagens e desvantagens, mas um dos pontos mais importantes de se lembrar é que o _Local Storage_ não deveria guardar dados sensíveis, por motivos de segurança.

