---
description: 'O que são objetos, e pra que servem?'
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

// imprime 'valor1', igual ao método acima
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

## Resumo

Neste capítulo vimos o básico de objetos:

* Como declarar objetos
* Como ler e escrever de objetos
* O que acontece quando atribuímos objetos a várias variáveis

