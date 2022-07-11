```ts
type Teste = {

    altura?: number

    largura?: number

    profundidade?: number

    x?: number

    y?: number

    z?: number
}


class Paralelepipedo{

    altura: number

    largura: number

    profundidade: number

    x: number

    y: number

    z: number

    constructor({altura = 10, largura = 20, profundidade = 30, x = 1, y = 2, z = 3}: Teste){

        this.altura = altura

        this.largura = largura

        this.profundidade = profundidade

        this.x = x

        this.y = y

        this.z = z
    }
}

const instancia = new Paralelepipedo({profundidade: 100})

console.log(instancia.profundidade)

// getters e setters

class X{

    private _idade: number = 0

    get idade(){
        return this._idade
    }

    set idade(value: number){
        this._idade = value
    }
}

let inst = new X()

console.log(inst.idade)

inst.idade = 2

console.log(inst.idade)
```
[[10-Classe Abstrata]]