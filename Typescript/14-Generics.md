# Introdução ao Generics
Generics são para tipos o que valores são para argumentos de função — eles são uma maneira de dizer aos nossos componentes (funções, classes ou interfaces) o tipo que queremos usar quando executarmos esse pedaço de código, da mesma forma como dizemos a uma função quais valores usar como argumentos quando nós a executamos.

```ts
class IdentityClass{

    identity<T>(arg: T): T{
        return arg
    }

    identity2<T, U>(value: T, message: U): T{
        console.log(message)

        return value
    }
}

const foo = new IdentityClass()

console.log(foo.identity<number>(1)) // 1
console.log(foo.identity2<number, string>(2, "Olá")) // "Olá" 2
```


### Genéricos para Classes e Interfaces funcionam exatamente como em Funções


```ts
interface GenericInterface<U>{
    value: U
    getIdentity(): U
}

class IdentityClass<T> implements GenericInterface<T>{
    value: T

    constructor(value: T){
        this.value = value
    }

    getIdentity(): T {
        return this.value
    }
}

const myNumberClass = new IdentityClass<number>(1)
console.log(myNumberClass.getIdentity())

const myStringClass = new IdentityClass<string>('Hello!')
console.log(myStringClass.getIdentity())
````

Funciona assim:

- Instanciamos uma nova instância de `IdentityClass`, passando `Number` e `1`
- Na classe de identidade, `T` torna-se `Number`
- `IdentityClass` implementa `GenericInterface<T>` e sabemos que `T` é `Number`, por isso é como se estivéssemos implementando `GenericInterface<Number>`
- Em `GenericInterface`, `U` torna-se `Number`. Eu propositadamente usei nomes de variáveis ​​diferentes aqui para mostrar que o valor do tipo se propaga pela cadeia e o nome da variável não importa

### Caso de uso prático: indo além dos tipos primitivos
Considere o exemplo clássico de herança de um carro. Nós temos uma classe base `Car` que é usada como base para `Truck` e `Vespa`. Em seguida, escrevemos uma função de utilidade `washCar` que recebe uma instância genérica `Car` e depois a retorna.

```ts
class Car{
    label: string  = 'Generic Car'
    numWheels: number = 4
	
    horn(){
        return "beep beep"
    }
}

class Truck extends Car{
    label = 'Truck';
    numWheels = 18;
}

class Vespa extends Car{
    label = 'Vespa'
    numWheels = 2
}

function washCar<T extends Car>(car: T): T{
    console.log(`Received a ${car.label} in the car wash.`)
    console.log(`Cleaning all ${car.numWheels} tires.`)
    console.log('Beeping horn -', car.horn())
    console.log('Returning your car now')

    return car
}

const myVespa = new Vespa()
washCar<Vespa>(myVespa)

const myTruck = new Truck()
washCar<Truck>(myTruck)
```

Ao dizer à nossa função `washCar` que `T` deve estender `Car`, sabemos quais funções e propriedades podemos chamar dentro da função. Usar um tipo genérico também nos permite retornar o tipo específico que passamos, ao invés de apenas um não específico tipo de `Car`.

### Generics com Array
```ts
// Nesse caso recebemos como argumento
// um Array do tipo T
function verify<T>(arg: T[]): T[]{
    return arg
}

console.log(verify<number>([1, 2, 3]))
console.log(verify<string>(['eu', 'tu', 'ele']))
```
