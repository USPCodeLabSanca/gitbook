---
description: Que horas são?
---

# Datas

### Introdução

Datas fazem parte do nosso dia a dia e, portanto, são frequentemente usadas em desenvolvimento de software. Em Javascript, você pode ter que criar um site com um calendário ou uma agenda, entre outras coisas. Essas aplicações podem precisar de controle de dias, horas, fuso horário e fazer cálculos com base nesses dados.

Para isso vamos usar o objeto padrão do Javascript para lidar com datas e horários: o `Date`!

### O Objeto Date

O objeto `Date` é padrão do Javascript, ou seja, não é preciso baixar nenhuma biblioteca/dependência para usá-lo. Ele possui vários métodos para manipular e formatar datas.

Ao criar um objeto do tipo `Date`, sem argumentos, é instanciado um objeto representando o momento atual \(data e horário\) de acordo com os dados fornecidos pelo seu sistema local.

```javascript
// Atribua a uma varivael o momento atual
const agora = new Date();

// Veja o resultado
console.log(agora); // Sun Oct 04 2020 15:31:43 GMT-0300 (Brasilia Standard Time)
```

O formato do print acima é:

| Dia da semana | Mês | Dia | Ano | Hora | Minuto | Segundo | Fuso Horário |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Sun | Oct | 04 | 2020 | 15 | 31 | 43 | GMT-0300 \(Brasilia Standard Time\) |

A data \(dia + mês + ano\) e o horário \(hora + minuto + segundo\) são dividos em partes para um fácil entendimento humano.

Para o Javascript, a data e o horário são armazenados em um `timestamp` \(traduz-se para algo como "marca no tempo"\), que é o tempo, em milissegundos, que se passou desde 1 de Janeiro de 1970 \(01/01/1970\), seguindo o [padrão Unix](https://pt.wikipedia.org/wiki/Era_Unix).

```javascript
// Pega o timestamp de um Date
const timestamp = agora.getTime(); // 1601836303000
```

O timestamp 1601836303000 representa a mesma data do primeiro trecho de código.

### Construtor

Ha diferentes forma de criar um objeto de `Date` em Javascript, dependendo de quais valores são passados no construtor:

| Construtor | Resultado |
| :--- | :--- |
| new Date\(\) | Data e horário atual |
| new Date\(timestamp\) | Data baseada no timestamp |
| new Date\(date string\) | Data baseada na string |
| new Date\(ano, mes, dia, horas, minutos, segundos, milissegundos\) | Data baseada nos parâmetros |

### Lendo dados de um `Date` com `get`

Você pode precisar de partes especificas da um `Date`, como o dia ou o ano, e para isso temos vários métodos. Os métodos abaixo retornam seus correspondentes valores em relação ao **fuso horário local** do seu sistema.

| Data/Horário | Método | Intervalo | Exemplo |
| :--- | :--- | :--- | :--- |
| Ano | getFullYear\(\) | YYYY | 1992 |
| Mês | getMonth\(\) | 0-11 | 0 \(Janeiro\) |
| Dia \(do mês\) | getDate\(\) | 1-31 | 1 \(primeiro dia do mês\) |
| Dia \(da semana\) | getDay\(\) | 0-6 | 0 \(domingo\) |
| Hora | getHours\(\) | 0-23 | 0 \(meia-noite\) |
| Minuto | getMinutes\(\) | 0-59 | 30 |
| Segundo | getSeconds\(\) | 0-59 | 50 |
| Milissegundo | getMilliseconds\(\) | 0-999 | 200 |
| Timestamp | getTime\(\) | Milissegundos após o 1970 | 1601836303000 |

Note que a maioria dos valores começam do 0, exceto o dia do mês.

Saber qual o intervalo que o método retorna é muito importante

```javascript
// Para checar se um Date se refere a Dezembro, use o mes 11 e não o 12
// Esses pequenos detalhes pode ser dificeis de debugar
const data = new Date(timestamp);

if (data.getMonth === 11) {
    console.log('É Dezembro');
}
else {
    console.log('Não é Dezembro');
}
```

### Modificando um `Date` com `set`

Para cada método `get` acima existe um `set` correspondente que modifica aquela parte da informação do `Date`.

**Importante:** Os objetos `Date` são mutáveis, portanto seus métodos _set_ modificam o objeto original. Passar um `Date` como parâmetro de uma função pode acabar modificando o objeto original; quando este não é o comportamento desejado, basta fazer uma cópia dele \(usando `new Date(minhaData)`\)

| Data/Horário | Método | Intervalo | Exemplo |
| :--- | :--- | :--- | :--- |
| Ano | setFullYear\(\) | YYYY | 1992 |
| Mês | setMonth\(\) | 0-11 | 0 \(Janeiro\) |
| Dia \(do mês\) | setDate\(\) | 1-31 | 1 \(primeiro dia do mês\) |
| Dia \(da semana\) | setDay\(\) | 0-6 | 0 \(domingo\) |
| Hora | setHours\(\) | 0-23 | 0 \(meia-noite\) |
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

Note que as funções `set` mudam o valor absoluto, ou seja, com elas não se pode aumentar o dia ou a hora em relação ao valor atual. Para fazer isso, temos que usar o `set` junto com o `get` respectivo. Exemplo \(incrementando em um o ano\):

```javascript
const agora = new Date();
const ano = agora.getFullYear();
agora.setFullYear(ano + 1);
```

### UTC

UTC é uma sigla para Coordinated Universal Time \(Tempo Universal Coordenado\), que é um padrão de fusos.

Aqui no Brasil estamos \(em maioria\) 3 horas atrasados em relação ao fuso de referência, e essa informação está disponível no print do objeto Date: `GMT-0300`.

Problemas de sincronização podem surgir por conta do fuso horário. Imagine que você esta desenvolvendo um sistema que depende de datas pra funcionar, e que ele precisa de precisão. Durante o desenvolvimento, as datas vão ser referentes a de sua maquina \(se estiver no Brasil, vão estar com 3 horas de atraso no padrão UTC\). Se seu sistema for rodar em nuvem, é provável que a maquina esteja hospedada em outro país, causando variações de horário que podem quebrar seu sistema.

Para resolver esse tipo de problema, todos os métodos _get_ e _set_ tem um respectivo para o UTC \(fuso horário 0\).

* getUTCHours
* getUTCDate
* setUTCFullYear
* ...

Usando os métodos UTC, o resultado da execução é sempre o mesmo,  independente da região da máquina que está executando o código.

### Formas de exibir/formatar um `Date`

Existem várias formas diferentes para exibir um `Date`, dependendo para quem ou onde a informação será exibida:

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

Os métodos com `Locale` são referentes à região da máquina e, portanto, podem variar em seus resultados.

### Conclusão

Vimos como inicializar um `Date`, como ler \(_get_\) e modificar \(_set_\) suas informações e como exibí-lo.

Para mais informações, cheque a [documentação do Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) 

