# Revisão de HTTP

O protocolo HTTP é um protocolo de comunicação da internet, sendo o HTTP uma das principais maneiras de se tratar trocas de informação quando se trata de desenvolvimento web

A comunicação do HTTP é feita no modelo **cliente-servidor.** Este modelo é dividido em duas partes: o cliente, que pede que o servidor execute alguma função, isto é, faz uma requisição ao servidor; e o servidor, que recebe essas requisições, executa funções específicas, normalmente salvando informações dentro de um banco de dados, e retorna ao cliente uma resposta de como procedeu a requisição.

No próximo capítulo seguinte, iremos nos focar em como realizar as requisições HTTP; enquanto neste, a anatomia de uma requisição será o nosso foco.

## Formato da Requisição

Uma requisição tem algumas partes que a compõem:

* Método de Requisição
* URLs
* Body
* Headers

## Métodos da Requisição

Os métodos são ações que mostram o que deve acontecer pela requisição:

* GET - Recuperar alguma informação.
* POST - Enviar informação ao servidor
* PUT - Atualizar alguma informação no servidor
* DELETE - Deletar informação

## URLs

A URL é geralmente descreve onde que vai ser feito a requisição, normalmente é composto por:

* Host - Descreve o endereço do servidor a ser feito a requisição
* Port \(ou porta\) - Descreve o ponto de entrada para acessar a aplicação no servidor
* Path \(ou caminho\) - Descreve onde vai ser solicitado algum recurso da aplicação
* Query - Dados que são enviados junto a, normalmente, uma requisição GET

### Exemplos:

Por exemplo, uma requisição GET pode ser da seguinte maneira:

{% api-method method="get" host="http://google.com/search?q=bolos" path="" %}
{% api-method-summary %}
Acessar o google 
{% endapi-method-summary %}

{% api-method-description %}
Método que acessa uma página pesquisando bolos.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

A URL acima pode ser decomposta em diferentes partes:

* **http://google.com** - este é o host da URL
* **/search** - este é o caminho que algum recurso vai ser solicitado
* **?q** - esse é o query string que dará os parâmetros pro recurso a ser solicitado, no caso, bolos.

Pode ser usado um um exemplo fictício de uma API tbm:H

{% api-method method="post" host="http://localhost:3000/item" path="" %}
{% api-method-summary %}
Inserir um item
{% endapi-method-summary %}

{% api-method-description %}
Esse método cria um novo item 
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="title" type="string" required=true %}
Titulo do item
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
Item Criado!T
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

No exemplo acima, pode-se ver as seguintes partes:

* **http://localhost:** - Esse é o host da URL, onde está o servidor.
* **3000** - Essa é a porta de entrada da aplicação, ela aqui não é opcional, pois não é a porta 80.
* **item/** - este é o caminho que algum recurso vai ser solicitado.

Nessa requisição, que requer um body. Este body só precisa de um parâmetro obrigatório, chamado "title".

## Body da Requisição

O body é o corpo da requisição. Nele você envia qualquer tipo de informação relevante a requisição; normalmente são utilizados para compor dados referentes a uma requisição POST.

## Headers da Requisição

Headers são informações adicionais referentes a requisição. Mostra, por exemplo, que software foi utilizado pra realizar a requisição, qual é o tipo de conteúdo está sendo aceito na requisição, entre outros.

## Resposta da Requisição

A resposta de uma requisição é um "cabeçalho" descrevendo como o servidor lidou com a requisição enviada pelo cliente.

As partes que compõem a resposta são:

* Status Code
* Headers
* Conteúdo da Resposta

## Status Code

O status code é um código que mostra o que aconteceu com a requisição após ser realizada pelo servidor. Há uma grande gama de status code; porém, seguem uma regra determinada:

* 1XX - Mostra que a requisição foi recebida, mas nada foi feito ainda.
* 2XX - A requisição foi aceita e teve sucesso.
* 3XX - A requisição precisa ser redirecionada para que a requisição tenha sucesso.
* 4XX - O formato da requisição enviada pelo cliente está errada.
* 5XX - O servidor teve problemas ao realizar a requisição e não pode proceder.

## Headers de Resposta

Descreve informações adicionais referente a requisição, como o tamanho da resposta, qual é o tipo de conteúdo, quando foi aceita a requisição, entre outros.

## Conteúdo da Resposta

Descreve o que foi retornado pelo servidor após a requisição ser enviada pelo cliente.

