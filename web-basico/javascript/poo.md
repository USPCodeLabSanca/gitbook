# POO

## O que é POO?

POO \(Programação Orientada a Objetos\) é um paradigma de programação que busca utilizar objetos para representar coisas do mundo real dentro de um programa, facilitando o entendimento e acesso a funcionalidades do código.

Um dos exemplos mais utilizados para demostrar conceitos de POO é modelar a classe Pessoa.

### O que é uma classe?

Classe é como uma planta arquitetônica, assim como podemos construir diferentes casas utilizando uma mesma planta, com uma classe podemos instanciar vários objetos de Pessoa seguindo uma estrutura básica predefinida.

No Javascript podemos definir uma classe da seguinte forma:

```javascript
class Pessoa {
  constructor(nome, idade) {
    this.nome = nome;
    this.idade = idade;
  }

  seApresentar() {
    console.log(`Olá, meu nome é ${this.nome}.`);
  }
}
```

Agora que temos uma classe Pessoa podemos instanciar \(criar\) objetos a partir dela.

```javascript
const pessoa1 = new Pessoa('Josias', 34);
const pessoa2 = new Pessoa('Flávia', 23);

pessoa1.seApresentar();
// Olá, meu nome é Josias.


pessoa2.seApresentar();
// Olá, meu nome é Flávia.
```

## Princípios de POO

### Encapsulamento

Encapsulamento consiste em esconder informações que não devem ser acessadas de forma direta mas sim por meio de funções auxiliares que definem regras de como essa informação deve ser manipulada e visualizada.

```javascript
class Pessoa {
  constructor(nome, idade) {
    this._nome = nome;
    this._idade = idade;
  }
  
  get nome() {
    return this._nome;
  }
  
  get idade() {
    return this._idade;
  }
  
  fazerAniversario() {
    this._idade++;
  }
  
  seApresentar() {
    console.log(`Olá, meu nome é ${this._nome} e tenho ${this._idade} anos.`);
  }
}

const pessoa1 = new Pessoa('Josias', 34);

pessoa1.fazerAniversario();

pessoa1.seApresentar();
// Olá, meu nome é Josias e tenho 35 anos.
```

No exemplo acima é possível notar o uso do carácter \_ como prefixo do nome das variáveis nome e idade. É convencionado que variáveis que começam com o underline são consideradas privadas, isto é, não devem ser acessadas diretamente pelo programador, apenas pelo uso dos setters e getters.  

### Abstração

Abstração significa esconder detalhes de implementação, mostrando apenas o essencial para o mundo externo ao objeto.

```javascript
class Pessoa {
  constructor(nome, idade) {
    this._nome = nome;
    this._idade = idade;
  }
  
  get nome() {
    return this._nome;
  }
  
  get idade() {
    return this._idade;
  }
  
  fazerAniversario() {
    this._idade++;
  }
  
  seApresentar() {
    if (Math.random() < 0.5) {
      console.log(`Olá, meu nome é ${this._nome} e tenho ${this._idade} anos.`);
    } else {
      console.log(`Oii, me chamo ${this._nome} e tenho ${this._idade} anos.`);
    }
  }
}

const pessoa1 = new Pessoa('Josias', 34);

pessoa1.fazerAniversario();

pessoa1.seApresentar();
// Olá, meu nome é Josias e tenho 35 anos.

pessoa1.seApresentar();
// Oii, me chamo Josias e tenho 35 anos.
```

### Herança

Muitas vezes os objetos acabam sendo bem similares, compartilhando uma lógica comum, porém sem serem exatamente iguais. Uma forma de reutilizar essa lógica comum, extraindo a lógica única para uma classe à parte, é chama de **herança**. Esse processo consiste em criar uma classe filha que deriva de uma classe pai.

```javascript
class Estudante extends Pessoa {
  constructor(nome, idade, curso) {
    super(nome, idade);
    this._curso = curso;
  }
  
  get curso() {
    return this._curso;
  }
  
  estudar() {
    console.log(`Estudando ${this._curso}`)
  }
}

const estudante1 = new Estudante('Josias', 34, 'Administração');

estudante1.seApresentar();
// Olá, meu nome é Josias e tenho 34 anos.

estudante1.estudar();
// Estudando Administração.
```

### Polimorfismo

O termo **polimorfismo** é originário do grego e significa "muitas formas" \(_poli_ = muitas, _morphos_ = formas\). Em POO, isso ocorre quando diferentes objetos chamam o mesmo método e recebem respostas adequadas ao contexto de cada um.

```javascript
class Estudante extends Pessoa {
  constructor(nome, idade, curso) {
    super(nome, idade);
    this._curso = curso;
  }
  
  get curso() {
    return this._curso;
  }
  
  estudar() {
    console.log(`Estudando ${this._curso}`)
  }
  
  seApresentar() {
    console.log(`Olá, meu nome é ${this._nome}, tenho ${this._idade} anos e faço ${this._curso}.`);
  }
}

const estudante1 = new Estudante('Josias', 34, 'Administração');
const pessoa1 = new Pessoa('Flávia', 23);

pessoa1.seApresentar();
// Olá, meu nome é Flávia e tenho 23 anos.
estudante1.seApresentar();
// Olá, meu nome é Josias, tenho 34 anos e faço Administração.
```

