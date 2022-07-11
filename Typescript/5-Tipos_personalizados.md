# Definir tipos para cada elemento de um array
```ts
type User = {

    name: string,

    age: number,

    height: number,

    peso: number,

    bornDate: string,

    apelido: string,

    password: string,

    ativado: boolean,

    pokeCards: string[]

}

const issac: User = {

    name: "Issac",

    age: 24,

    height: 1.77,

    peso: 76,

    bornDate: "31/07/1997",

    apelido: "Odish",

    password: "123",

    ativado: false,

    pokeCards: ['Pikachu', 'Cyndaquil']

}

type List = [string, number, User]

const test: List = ['string', 2, issac]


type Chaves = keyof User
const example: Chaves = 'bornDate'

console.log(typeof example) // string
```
[[6-Tipo_never]]