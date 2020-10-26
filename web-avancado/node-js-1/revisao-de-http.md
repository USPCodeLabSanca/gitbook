# Revisão de HTTP

O protocolo HTTP é um protocolo de comunicação da internet, sendo o HTTP uma das principais maneiras de se tratar trocas de informação quando se trata de desenvolvimento web

A comunicação do HTTP é feita no modelo **cliente-servidor.** Este modelo é dividido em duas partes: o cliente, que pede que o servidor execute alguma função, isto é, faz uma requisição  ao servidor; e o servidor, que recebe essas requisições, executa funções específicas e retorna ao cliente uma resposta de como procedeu a requisição.

### Formato da Requisição

Uma requisição tem algumas partes que a compõem:

* Método de Requisição
* URLs
* Body
* Headers

###  Métodos da Requisição

Os métodos são ações que mostram o que deve acontecer pela requisição: 

* GET - Recuperar alguma informação.
* POST - Enviar informação ao servidor
* PUT - Atualizar alguma informação no servidor
* DELETE - Deletar informação

### URLs 

A URL é geralmente descreve onde que vai ser feito a requisição, normalmente é composto por:

* Host - Descreve o endereço do servidor a ser feito a requisição
* Port \(ou porta\) - Descreve o ponto de entrada para acessar a aplicação no servidor
* Path \(ou caminho\) - Descreve onde vai ser solicitado algum recurso da aplicação
* Query - Dados que são enviados junto a, normalmente, uma requisição GET

### Body da Requisição

O body é o corpo da requisição. Nele você envia qualquer tipo de informação relevante a requisição; normalmente são utilizados para compor dados referentes a uma requisição POST.

### Headers da Requisição

Headers são informações adicionais referentes a requisição. Mostra, por exemplo, que software foi utilizado pra realizar a requisição, qual é o tipo de conteúdo está sendo aceito na requisição, entre outros.

### Resposta da Requisição

A resposta de uma requisição é um "cabeçalho" descrevendo como o servidor lidou com a requisição enviada pelo cliente.

As partes que compõem a resposta são:

* Status Code
* Headers
* Conteúdo da Resposta

### Status Code

O status code é um código que mostra o que aconteceu com a requisição após ser realizada pelo servidor. Há uma grande gama de status code; porém, seguem uma regra determinada:

* 1XX - Mostra que a requisição foi recebida, mas nada foi feito ainda.
* 2XX - A requisição foi aceita e teve sucesso.
* 3XX - A requisição precisa ser redirecionada para que a requisição tenha sucesso.
* 4XX - O formato da requisição enviada pelo cliente está errada.
* 5XX - O servidor teve problemas ao realizar a requisição e não pode proceder.

### Headers de Resposta

Descreve informações adicionais referente a requisição, como o tamanho da resposta, qual é o tipo de conteúdo, quando foi aceita a requisição, entre outros.

### Conteúdo da Requisição

Descreve o que foi retornado pelo servidor após a requisição ser enviada pelo cliente. 









