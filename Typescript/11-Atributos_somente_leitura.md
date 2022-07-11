# Atributos somente leitura (readonly)
Podemos criar atributos que servem apenas para leitura.

Nesse exemplo, declaramos a variável *name* como apenas leitura, e que é atribuído um valor a ela, apenas no momento de instância da classe

```ts
class Teste{

    readonly name: string

    constructor(name: string){
        this.name = name
    }
}

const nova = new Teste('Maria')

nova.name = 'João' // Erro!

console.log(nova.name) // Maria
```

