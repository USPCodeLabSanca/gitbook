# Módulos \(em ES6\)

Em projetos grandes, os módulos, que foram adicionados no ES6, são essenciais. Ajudam na organização do sistema, no reuso de código e na diminuição da complexidade das funcionalidades do sistema.

Imagina que você tivesse que lidar com um código de mais de 3000 linhas em um mesmo arquivo, seria complicado de entender o código do inicio ao fim depois de duas semanas sem programar, não é mesmo?

## Importando e exportando módulos

### Export e Import

Para exportar módulos em JS, a maneira mais simples é exportar um único objeto, podendo ser: uma função, um JSON, um valor. O que você quiser, e a maneira mais simples de efetuar o export é como abaixo:

{% tabs %}
{% tab title="export" %}
```javascript
export default func1(x, y){
    console.log(x*y)
}
```
{% endtab %}

{% tab title="import" %}
```javascript
// Aqui eu importo a func1 para esse arquivo
import { func1 } from 'functions'

func1(7,9) //63
```
{% endtab %}
{% endtabs %}

#### Classe

Para importar ou exportar classes não se difere muito:

{% tabs %}
{% tab title="export" %}
```javascript
export class C1{
    constructor(arg1) {
        this._arg1 = arg1;
    }
    
    get arg1() {
        return this._arg1;
    }

};
```
{% endtab %}

{% tab title="import" %}
```javascript
import { C1 } from 'classes';

const c1 = new C1('arg2');
dev.arg1;
```
{% endtab %}
{% endtabs %}

#### Default

A exportação padrão só é permitida uma vez por script, ela é feita utilizando a keyword `export default`, ela é muito útil para definirmos um exportação padrão de um módulo. Um exemplo prático é você ter um arquivo `utlils-string.js` com várias funções que fazem alguma coisa com string que são utilizadas em vários arquivos.

Um exemplo de `export default` em uma função é feito abaixo:

{% tabs %}
{% tab title="export" %}
```javascript
export default function (x){
    console.log(x);
}
```
{% endtab %}

{% tab title="import" %}
```javascript
import func2 from 'func2';

func2(a);
```
{% endtab %}
{% endtabs %}

#### Combinando tudo

Agora que já sabemos como o import e export funcionam, podemos verificar como é feito a exportação e importações de múltiplos valores:

{% tabs %}
{% tab title="export" %}
```javascript
let adiciona = function(a, b) {
    return a + b;
}

let subtrai = function(a, b) {
    return a - b;
}

export adiciona;
export subtrai;

export default {
    adiciona: adiciona,
    subtrai: subtrai
};
```
{% endtab %}

{% tab title="import" %}
```javascript
import { adiciona } from 'export';
import { subtrai } from 'export';
import matematica from 'export';


console.log(adiciona(1, 2)) // Saída: 3
console.log(subtrai(1, 2)) // Saída: -1
console.log(matematica.adiciona(2, 2)) // Saída: 4
```
{% endtab %}
{% endtabs %}

