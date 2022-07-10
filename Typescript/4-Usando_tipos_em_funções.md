# Tipar a assinatura da função
```ts
function sum(param1: number, param2: number): number{

    return param1 + param2

}

const exemplo: () => string = () => {

    return 'Olá'

}

const exemplo2: (param1: number, param2: number) => number = sum
```

### Criar uma função que recebe um objeto de parâmetro e retorna true or false

```ts
type User = {

    name: string,

    age: number

}

const issac: User = {

    name: 'Issac',

    age: 24

}

const exemplo3: (objParam: User) => boolean = (objParam) => {

    return objParam.age >= 18

}
```

### Criando um tipo de função e atribuindo essa assinatura à uma variável
```ts
type sumFunctionType = (param1: number, param2: number) => number

function sumFunction(x1: number, x2: number): number{

    return x1 + x2

}

let x: sumFunctionType = sumFunction
```

### Criando uma função cujo argumentos recebem um tipo genérico
```ts
function loucura<T>(param1: T, param2: T): boolean{

    return param1 === param2

}

console.log(loucura("1", "1"))
console.log(loucura<number>(1, 1))
```