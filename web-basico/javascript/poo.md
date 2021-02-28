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

Encapsulamento consiste em esconder informações que não devem ser acessadas de forma direta mas sim por meio de funções auxiliares que definem regras de como esse informação deve ser manipulada e visualizada.

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

Muitas vezes os objetos acabam sendo bem similares, compartilhando uma lógica comum porem sem ser exatamente iguais. Uma forma de reusar essa lógica comum extraindo a lógica unica para uma classe a parte é chama de herança. Esse processo consiste em criar uma classe filha que deriva de uma classe pai.

```javascript
class Estudante extends Pessoa {
  constructor(nome, idade, curso) {
    this._nome = nome;
    this._idade = idade;
    this._curso = curso;
  }
  
  get nome() {
    return this._nome;
  }
  
  get idade() {
    return this._idade;
  }
  
  get curso() {
    return this._curso;
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
  
  estudar() {
    console.log(`Estudando ${this._curso}`)
  }
}

const estudante1 = new Estudante('Josias', 34, 'Administração');

pessoa1.seApresentar();
// Olá, meu nome é Josias e tenho 34 anos.

estudante1.estudar();
// Estudando Administração.
```

