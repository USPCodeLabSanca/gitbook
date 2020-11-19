---
description: O que são objetos e pra que servem?
---

# Objetos

## O que são objetos?

Objetos em JavaScript são uma estrutura que associa chaves com valores. Pode-se fazer a analogia de objetos com um dicionário: da mesma forma que cada palavra num dicionário tem um significado, cada chave num objeto tem um valor. Objetos são definidos da seguinte forma:

```javascript
let objetoVazio = {}; // Objeto sem nenhum par chave-valor

let objetoComUmaChave = { chave: 'valor' };

let objetoComDuasChaves = { chave1: 'valor1', chave2: 'valor2' };

let objetoComMuitasChaves = {
    chave1: 'valor1',
    chave2: 'valor2',
    chave3: 'valor3',
    chaveNumerica: 42,
    chaveComFuncao: function () { console.log('Sou uma função'); },
    chaveNula: null,
    chaveBooleana: true,
    chaveIndefinida: undefined
    chaveComOutroObjeto: {
        chaveDentroDeOutroObjeto: 'Mais um valor'
    }
};
```

Como mostrado acima, objetos são sempre declarados entre pares de chaves \(curly brackets, '{' e '}'\). Dentro destas chaves, fazemos as associações entre chaves e valor. Cada par chave-valor é descrito da forma `chave: valor`. A chave pode ser qualquer número ou string, e o valor pode ser absolutamente qualquer tipo de valor suportado pelo JavaScript \(números, booleanos, funções, strings, etc...\).

Podemos acessar os valores destes objetos da seguinte forma:

```javascript
// imprime 'valor1', que é o valor associado à chave1
console.log(objetoComDuasChaves.chave1);

// imprime 'valor1', igual à forma acima
console.log(objetoComDuasChaves['chave1']);
```

Assim, se quisermos acessar o valor de uma chave 'key' que está dentro de um objeto 'obj', podemos simplesmente escrever `obj.key`. Essa mesma sintaxe também é usada para atualizar valores, ou adicionar valores novos, como por exemplo:

```javascript
// Trocamos o valor antigo 'valor1', associado à chave1, por 'novo valor'
objetoComDuasChaves.chave1 = 'novo valor';

// Agora, o valor 42 está associado à chave1.
objetoComDuasChaves.chave1 = 42;

// Aqui criamos uma nova chave chamada 'novaChave',
// e imediatamente associamos ela ao valor 'Olá, mundo!'.
objetoComDuasChaves.novaChave = 'Olá, mundo!';
```

## Para que servem objetos?

Objetos podem inicialmente parecer desnecessários ou inúteis, pois eles não representam diretamente um dado, mas sim um grupo de dados. Aqui, vamos discutir alguns dos mais comuns usos de objetos em JavaScript:

### **Agrupar dados**

Um dos usos mais comuns de objetos em JavaScript é agrupar vários dados relacionados a uma entidade. Por exemplo, se nosso programa for lidar com vários dados de um usuário \(como nome, senha, email, telefone, etc...\), podemos agrupar essas informações num objeto só:

```javascript
// Sem um objeto
let name = 'joão';
let password = 'senha123';
let email = 'joaopedro@gmail.com';

// Com um objeto
let user = {
    name: 'joão',
    password: 'senha123',
    email: 'joaopedro@gmail.com'
};
```

Organizando nossos dados dentro de um objeto, fica muito mais claro que as variáveis `name`, `email` ou `password` estão associadas a um usuário e, ainda mais importante, estão associadas ao mesmo usuário.

Outra vantagem que ganhamos com agrupamento é que, se houvessem informações de vários usuários diferentes, cada um com seu nome, email e senha, seria muito mais difícil misturar sem querer as informações dos usuários. Cada usuário teria o seu próprio objeto, que armazena os dados desse usuário.

### **Reduzir quantidade de variáveis declaradas**

Ao invés de criar múltiplas variáveis, cada uma com um dado diferente, podemos agrupar tudo num objeto só \(como exemplificado no ponto acima\). Com menos variáveis criadas, reduzimos as chances de, sem querer, declarar duas variáveis com o mesmo nome \(o que pode causar bugs bem difíceis de se encontrar\).

Retomando o exemplo anterior, ao invés de declarar três variáveis com nomes extremamente genéricos \(`name`, `email` e `password`\), declaramos apenas uma \(`user`\), e liberamos as outras três variáveis para serem usadas em outro lugar.

### **Dicionário**

Um Dicionário é uma estrutura de dados. Ela é descrita exatamente como são os objetos de JavaScript: um conjunto de associações de chave-valor. Dicionários são conhecidos por terem tempo de leitura e de escrita constante \(logo, muito rápidos\). Assim, se você tem uma coleção de dados muito grande, onde você terá que rapidamente buscar por algo específico, você pode armazenar esses dados num objeto \(onde a chave é o ID do dado, e o valor é o dado em si\) para uma busca rápida.

## Objetos e passagem por referência

Uma das mais importantes peculiaridades dos objetos no JavaScript é que eles são o único tipo de valor que, quando atribuídos a outra variável, não são copiados para essa variável, apenas a sua referência é passada.

### O que é passagem por referência?

Num computador, o valor de toda variável é armazenado em um espaço específico da memória. Cada variável tem reservado o seu espaço na memória.

"Passagem por valor" é o processo de copiar o valor de uma variável para outra, isto é, copiar o valor que está em uma região da memória \(referente à primeira variável\) para outra região da memória \(referente à segunda variável\). Assim, a expressão `a = b` faz com que o valor de `b` seja copiado para o espaço da memória de `a`.

"Passagem por referência" é quando ao invés de copiar o valor de um lugar da memória para outro, o programa faz com que as duas variáveis apontem para o mesmo espaço na memória. Então, a expressão `a = b` faz com que a variável `a` aponte para o mesmo lugar da memória que a variável `b`.

### Exemplo de passagem por referência

```javascript
// ------- Passagem por valor -------
let num1 = 10;
let num2 = num1; // Números sofrem passagem por valor.
num2 = 20;

console.log(num1); // 10
console.log(num2); // 20

// ------- Passagem por referência -------
let obj1 = { num: 10 };
let obj2 = obj1; // Objetos sofrem passagem por referência

obj2.num = 20;

console.log(obj1.num); // 20
console.log(obj2.num); // 20
```

Acima temos um exemplo de passagem por valor e passagem por referência. Na passagem por valor \(entre `num1` e `num2`\) note que mudar o valor de uma variável \(`num2`\) não faz a outra variável \(`num1`\) mudar de valor também. Assim, ao imprimir as duas variáveis, temos dois valores diferentes \(`10` e `20`\).

Na passagem por referência \(entre `obj1` e `obj2`\), definimos um objeto \(`obj2`\) e atribuímos `obj1` para ele. Essa atribuição faz com que a variável `obj2` aponte para o mesmo objeto de `obj1`. Assim, ao realizar a atribuição `obj2.num = 20`, tanto `obj1` quanto `obj2` enxergam `num` como `20`. Por fim, ao imprimir `obj1.num` e `obj2.num`, temos o mesmo valor.

### Por que passagem por referência é importante?

Na tradicional "passagem por valor", como o valor de uma variável é copiado \(logo, cada variável tem o seu valor independente\), se uma variável aplicar uma mudança no seu valor, a outra variável continua com o seu valor intacto, pois as cópias não são relacionadas.

Entretanto, na "passagem por referência", como as duas variáveis apontam para o mesmo lugar da memória, mudar o valor de uma das variáveis faz com que a outra variável também perceba a mudança.

Com essas características em mente, há uma clara vantagem na passagem por referência: não há nenhum custo de performance ao se atribuir objetos de uma variável à outra. Suponhamos que exista um objeto `obj` que contém um milhão de pares chave-valor. Caso atribuíssemos esse objeto para outra variável \(`const obj2 = obj`\), se houvesse passagem por valor, seria necessário duplicar todos os pares chave-valor contidos no objeto. Mas nesse caso, como a passagem é por referência, essa operação tem um custo negligenciável.

## Copiando objetos

Tendo em mente que atribuir objetos a variáveis apenas faz uma passagem por referência, e não uma cópia do objeto, fica dúvida de como podemos copiar um objeto. Entretanto, a resposta dessa pergunta não é tão clara quando nós começamos a introduzir objetos mais complexos, especificamente, objetos cujos valores são outros objetos. Veja esse exemplo:

```javascript
const pessoa = {
    nome: 'Rita oliveira',
    idade: 22,
    endereco: {
        cidade: 'São Carlos',
        estado: 'São Paulo',
        pais: 'Brasil'
    }
};
```

Aqui, uma forma bastante intuitiva de copiar o objeto `pessoa` é só criar um novo objeto, e copiar todas as propriedades do objeto antigo no novo, por exemplo:

```javascript
const pessoaCopia = {};
pessoaCopia.nome = pessoa.nome;
pessoaCopia.idade = pessoa.idade;
pessoaCopia.endereco = pessoa.endereco;
```

Esse método funciona bem até quando chegamos na propriedade `endereco`. Como o valor de `endereco` é um objeto, quando fazemos `pessoaCopia.endereco = pessoa.endereco`, nós não estamos exatamente copiando o endereço do objeto `pessoa` para o objeto `pessoaCopia`, estamos apenas passando uma referência dele. Isso pode inicialmente parecer inofensivo, mas pode acabar gerando comportamentos indesejados. Veja esse exemplo:

```javascript
// Pessoa se mudou.
pessoa.endereco.cidade = "Araraquara";

// Como nós mudamos o valor de `pessoa.endereco.cidade`
// na linha acima, e o `pessoa.endereco` aponta para o mesmo
// objeto que `pessoaCopia.endereco` (por referência),
// o valor de `pessoaCopia.endereco.cidade` vai mudar também.
// Logo, a linha seguinte imprime "Araraquara".
console.log(pessoaCopia.endereco.cidade);
```

Aqui fica bem claro um dos problemas de apenas copiar as propriedades de um objeto em outro. Se nós formos mudar a propriedade de um dos objetos da variável original, a variável cópia também será afetada.

Esse tipo de cópia é chamado _Shallow Copy_ \(cópia rasa\). É a forma mais simples e menos custosa de se copiar objetos. Em contraste, existe o que é chamado de _Deep Copy_ \(cópia profunda\), onde não só as propriedades do objeto são copiadas, como também as propriedades dos objetos que ele contém. No exemplo dado, o equivalente a uma operação de _Deep Copy_ seria:

```javascript
const pessoaCopiaProfunda = {};
pessoaCopiaProfunda.nome = pessoa.nome;
pessoaCopiaProfunda.idade = pessoa.idade;
pessoaCopiaProfunda.endereco = {};
pessoaCopiaProfunda.endereco.cidade = pessoa.endereco.cidade;
pessoaCopiaProfunda.endereco.estado = pessoa.endereco.estado;
pessoaCopiaProfunda.endereco.pais = pessoa.endereco.pais;
```

Tendo em mente as diferenças entre _Shallow Copy_ e _Deep Copy_, podemos explorar melhor as ferramentas que o JavaScript nos oferece para resolver esse problema:

### _Shallow Copy_

Como visto nos exemplos acima, _Shallow Copy_ é o ato de copiar apenas as propriedades diretas de um objeto. O JavaScript tem um operador para isso, chamado _Spread Operator_ \(Operador de espalhamento\). Veja um exemplo de seu uso:

```javascript
const gato = {
    nome: 'Luna',
    idade: 3,
    sexo: 'feminino',
    guardiao: {
        nome: 'Lucas Amaral',
        idade: 34
    }
}

const gatoCopia = {...gato};
```

Se quisermos fazer uma _Shallow Copy_ de um objeto, apenas envolvemos ele em chaves e colocamos uma reticências atrás de seu nome, como visto no exemplo acima: `{...gato}`.

Note que esse é apenas um dos muitos usos para o _Spread Operator_. Caso você tenha curiosidade de saber os outros usos, veja esse [artigo](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Operators/Spread_syntax).

### _Deep Copy_

Como já mencionado,  _Deep Copy_ é a cópia de todas as propriedades de todos os valores de um objeto, e de todos os outros objetos que são valores do objeto raiz. Infelizmente, realizar _Deep Copy_ de um objeto qualquer é algo bastante difícil de fazer, pois esse algoritmo teria que saber como lidar algumas situações bastante específicas e pouco intuitivas \(com por exemplo referências cíclicas, ou referências que aparecem em duas propriedades diferentes\). Entretanto,, há um truque que normalmente usamos quando precisamos copiar profundamente um objeto:

```javascript
const notebook = {
    marca: 'Dell',
    peso: 2.34, // Kg
    processador: {
        marca: 'intel',
        nome: 'i5 3570',
    }
};

const notebookCopia = JSON.parse(JSON.stringify(notebook));
```

Aqui usamos as ferramentas de JSON do JavaScript. A função `JSON.stringify` transforma o objeto em uma string no formato JSON, e a função `JSON.parse` transforma uma string no formato JSON num objeto equivalente. Assim, no exemplo acima nós estamos primeiro transformando o objeto numa string, e depois voltando essa string para um objeto novo, efetivamente copiando ele profundamente.

É importante lembrar que as funções de JSON tem suas limitações: ignora funções e não permite referências cíclicas \(um objeto cuja propriedade aponta para si mesmo\). Note também que essa operação é bastante custosa, e deveria ser usada apenas quando necessário.

## Resumo

Neste capítulo vimos o básico de objetos:

* Como declarar objetos
* Como ler e escrever de objetos
* O que acontece quando atribuímos objetos a várias variáveis
* Como copiar objetos
  * _Shallow Copy_
  * _Deep Copy_

