# Módulos \(em ES6\)

Em projetos grandes, os módulos, que foram adicionados no ES6, são essenciais. Ajudam na organização do sistema, no reuso de código e na diminuição da complexidade das funcionalidades do sistema.

#### Import/Export

Para exportar módulos em JS, deve se fazer o seguinte:

```javascript
export default func1(x, y){
    console.log(x*y)

}
```

Assim, ele poderá ser importado dessa maneira:

```javascript
import { func1 } from 'functions'

func1(7,9) //63
```

#### Classes

Para importar ou exportar classes não se difere muito:

```javascript
export class C1{
    constructor(arg1)
    this._arg1 = arg1
    
    get arg1(){
        return this._arg1
    }

}
```

Assim, podendo importar dessa maneira:

```javascript
import { C1 } from 'classes'

const c1 = new C1('arg2')
dev.arg1 //arg2
```

#### Default

Também é comum ter a necessidade de exportar apenas uma função ou classe por arquivo. Dessa forma, a diferença na exportação fica:

```javascript
//func2

export default function (x){
    console.log(x)
}
```

E na importação:

```javascript
import func2 from 'func2'

func2(a)
```

