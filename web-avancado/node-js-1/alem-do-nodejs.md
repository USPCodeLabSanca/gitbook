---
description: O além do grande universo do NodeJS
---

# Além do NodeJS

Entrando no mundo de desenvolvimento web, você já deve ter se reparado com várias pessoas falando sobre diferentes frameworks ou bibliotecas diferentes que você não tem  nenhuma ideia do que se trata.

Este capítulo foi pensado para mostrar algumas dessas tecnologias que provavelmente serão muito mencionadas neste universo Node.

### React

React é uma biblioteca utilizada para desenvolver o Single-Page Applications \(ou SPA\), isto é, uma página que carrega dinamicamente através de javascript. Seu forte é a facilidade de conseguir replicar pedaços de HTML \(mais conhecido como componentes\) de um site em várias partes deste site sem precisar copiar o mesmo pedaço de HTML várias vezes; tendo também a habilidade de rotear entre páginas dinamicamente.

### React Native

Igual ao React, esse framework possibilita a criação de uma SPA. Porém, o React Native é usado para a criação de aplicativos mobile.

### GraphQL

Na verdade o graphQL não é uma biblioteca ou framework, o graphQL é uma linguagem de consulta para APIs. Sua principal característica é a facilidade a consulta de dados pelo cliente.

Diferentemente da arquitetura REST, o graphQL não acessa diferentes endpoints \(ou URLs\); para recuperar algum dado, tudo o que o cliente precisa fazer é pedir exatamente o que ele quer. Por exemplo:

```javascript
{
    user{
        name
        age
    }
}
```

No código acima, possivelmente feito pelo cliente, não se vê nenhuma menção ao servidor que a API está hosteada. E é isso que o torna tão atraente aos novos desenvolvedores! 

Além disso, o graphQL provê uma documentação limpa e correta toda vez que você codifica mais "objetos" para sua API.

### Typescript

O typescript foi construído em cima do javascript, adicionado tipos. Tipos melhoram a descrição de objetos, além de melhorar a verificação de erros.

Não é necessário nenhum código adicional ao digitar em typescript, pois o código é transformado em Javascript quando é compilado e, o resultado dessa compilação, pode ser executado em qualquer ambiente que um javascript roda!  

### Flutter

O Flutter é um framework open-source construído pela Google para auxiliar o desenvolvimento mobile. Sua ideia é se utilizar de combinação de "widgets" para formar a interface do usuário. Cada um desses widgets definem algum elemento \(como um botão\), estilo \(cor de um parágrafo\) ou layout \(tamanho da margem do aplicativo\) da sua aplicação. 

Além disso, o Flutter é um framework que não se utiliza de javascript. Então a construção de seus códigos não precisam ser compilados em algo que o aplicativo mobile possa entender. O código do Flutter já é compilado para diversas plataformas logo quando você está no meio dad digitação do seu código! 

\(em construção\)

