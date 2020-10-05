# Datas

### Introdução

Datas fazem parte do nosso dia a dia e portanto é frequentemente usada em desenvolvimento de software. Em Javascript você pode ter que criar um site com um calendário ou uma agenda entre outras cosias. Essas aplicações podem precisar de controle de dias, horas, fuso horário e fazer cálculos com base nesses dados.

Para isso vamos usar o objeto padrão do Javascript para lidar com data e horários o `Date`!

### O Objeto Date

O objeto `Date` é padrão do Javascript, ou seja, não é preciso baixar nenhuma biblioteca/dependência para usa-lo. Ele possui vários métodos para manipular e formatar datas.

Ao criar um objeto  do tipo `Date` sem argumentos é instanciado um objeto representando o momento atual \(data e hora\) de acordo com os dados fornecidos pelo sistema local.

```javascript
// Atribua a uma varivael o momento atual
const agora = new Date();

// Veja o resultado
console.log(agora); // Sun Oct 04 2020 15:31:43 GMT-0300 (Brasilia Standard Time)
```

O Formato do print acima é:

| Dia da semana | Mes | Dia | Ano | Hora | Minuto | Segundo | Fuso Horatio |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Sun | Oct | 04 | 2020 | 15 | 31 | 43 | GMT-0300 \(Brasilia Standard Time\) |

O dia e hora é divido em parte para fácil entendimento humano

Para o Javascript a data e hora são armazenadas em um `timestamp` \(traduz para algo como marca no tempo\) que é o tempo em milissegundos que se passaram desde primeiro de Janeiro de 1970 \(01/01/1970\)

```javascript
// Pegar o timestamp de um Date
const timestamp = agora.getTime(); // 1601836303000
```

O timestamp 1601836303000 representa a mesma data do primeiro trecho de código 

### Construtor

Ha diferentes forma de criar um objeto de `Data` em Javascript dependendo de quais valores são passados no construtor

| Construtor | Resultado |
| :--- | :--- |
| new Date\(\) | Data e hora atual |
| new Date\(timestamp\) | Data baseada no timestamp |
| new Date\(date string\) | Data baseada na string |
| new Date\(ano, mes, dia, horas, minutos, segundos, milissegundos\) | Data baseada nos parâmetros |

### Lendo dados de um `Date` com `get`

Você pode precisar de partes especificas da um `Date` como o dia, ou o ano e para isso temos vários métodos.  Os métodos abaixo retornam o valor correspondente em relação ao **fuso horário local** do seu sistema.

| Data/Hora | Método | Intervalo | Exemplo |
| :--- | :--- | :--- | :--- |
| Ano | getFullYear\(\) | YYYY | 1992 |
| Mes | getMonth\(\) | 0-11 | 0 \(Janeiro\) |
| Dia \(do mes\) | getDate\(\) | 1-31 | 1 \(primeiro dia do mes\) |
| Dia \(da semana\) | getDay\(\) | 0-6 | 0 \(domingo\) |
| Hora | getHours\(\) | 0-23 | 0 \(meia noite\) |
| Minuto | getMinutes\(\) | 0-59 | 30 |
| Segundo | getSeconds\(\) | 0-59 | 50 |
| Milissegundo | getMilliseconds\(\) | 0-999 | 200 |
| Timestamp | getTime\(\) | Milissegundos apos o 1970 | 1601836303000 |

Note que a maioria dos valores começam com 0, exceto o dia do mes.

Saber qual o intervalo que o método retorna é muito importante

```javascript
// Para checar se um Date se refere a dezembro use o mes 11 e não o 12
// Esses pequenos detalhes pode ser dificil de debugar
const data = new Date(timestamp);
if (data.getMonth === 11) {
    //
    console.log('É dezembro');
}
else {
    console.log('Não é dezembro');
}
```

### Modificando um `Date` com `set`

Para cada método `get` acima existe um `set` correspondente que modifica aquela parte da informação do `Date`

**Importante:** Os objetos `Date` são mutáveis, seus métodos set modificam o objeto original. Passar um `Date` como parâmetro de uma função pode acabar modificando o objeto, quando este não é o comportamento desejado basta fazer uma copia dele

| Data/Hora | Método | Intervalo | Exemplo |
| :--- | :--- | :--- | :--- |
| Ano | setFullYear\(\) | YYYY | 1992 |
| Mes | setMonth\(\) | 0-11 | 0 \(Janeiro\) |
| Dia \(do mes\) | setDate\(\) | 1-31 | 1 \(primeiro dia do mes\) |
| Dia \(da semana\) | setDay\(\) | 0-6 | 0 \(domingo\) |
| Hora | setHours\(\) | 0-23 | 0 \(meia noite\) |
| Minuto | setMinutes\(\) | 0-59 | 30 |
| Segundo | setSeconds\(\) | 0-59 | 50 |
| Milissegundo | setMilliseconds\(\) | 0-999 | 200 |
| Timestamp | setTime\(\) | Milissegundos apos o 1970 | 1601836303000 |

```javascript
const agora = new Date();

console.log(agora); // Sun Oct 04 2020 16:26:56 GMT-0300 (Brasilia Standard Time)

// Modificando o objeto
agora.setDate(11);
agora.setMonth(3);

console.log(agora); // Sat Apr 11 2020 16:26:56 GMT-0300 (Brasilia Standard Time)
```

Note que as funções `set` mudam o valor absoluto, ou seja, com elas não podem aumentar o dia ou a hora em relação ao valor atual, para fazer isso temos que usar o `set` junto com o `get` respectivo

```javascript
const agora = new Date();
const ano = agora.getFullYear();
agora.setFullYear(ano+1);
```

### UTC

UTC é uma sigla para Coordinated Universal Time \(Tempo Universal Coordenado\) que é um padrão de fusos

Aqui no Brasil estamos \(em maioria\) 3 horas atrasados  no fuso, e essa informação esta disponível no print `GMT-0300`

Problemas de sincronização podem surgir por conta de fuso horário, imagine que você esta desenvolvendo um sistema que depende de datas pra funcionar, e que ele precisa de precisão. Durante o desenvolvimento as datas vão ser referentes a de sua maquina \(se estiver no Brasil vão estar com 3 horas de atraso no padrão UTC\). Se seu sistema for rodar em nuvem, é provável que a maquina esteja hospedada em outro pais, causando variações de horário que podem quebrar seu sistema.

Para resolver esse tipo de problema, todos os métodos get e set tem um respectivo para o UTC \(fuso horário 0\)

* getUTCHours
* getUTCDate
* setUTCFullYear
* ...

Usando os métodos UTC o resultado da execução é sempre o mesmo independente da região da maquina que esta executando o código

### Formas de exibir/formatar um `Date`

Existem varias formas diferentes para exibir um `Date` dependendo para quem ou onde a informação sera exibida

| Método | Exemplo |
| :--- | :--- |
| toString\(\) | Sun Oct 04 2020 16:42:05 GMT-0300 \(Brasilia Standard Time\) |
| toDateString\(\) | Sun Oct 04 2020 |
| toTimeString\(\) | 16:42:05 GMT-0300 \(Brasilia Standard Time\) |
| toGMTString\(\) | Sun, 04 Oct 2020 19:42:05 GMT |
| toISOString\(\) | 2020-10-04T19:42:05.970Z |
| toLocaleString\(\) | 10/4/2020, 4:42:05 PM |
| toLocaleDateString\(\) | 10/4/2020 |
| toLocaleTimeString\(\) | 4:42:05 PM |

Os métodos com`Locale` são referentes a região da maquina portanto podem variar.

### Conclusão

Vimos como inicializar um `Date`, como ler \(get\) e modificar \(set\) suas informações e como exibi-lo

Para mais informações cheque a [documentação do Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) 

