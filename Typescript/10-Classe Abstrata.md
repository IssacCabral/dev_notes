# Classes Abstratas
Classes abstratas são classes em que não podem ser instanciadas diretamente, mas que, na verdade, devem ser herdadas. 

Elas possuem métodos abstratos que podem ser implementados de diferentes maneiras, dependendo da classe que está herdando-a,  contanto que essa implementação respeite a assinatura do método abstrato

```ts
abstract class Base{

    nome: string
    sobrenome: string

    constructor(nome: string, sobrenome: string){

        this.nome = nome

        this.sobrenome = sobrenome

    }

    abstract getNomeCompleto(): string
}

class Tronco extends Base{

    altura: number

    constructor(nome: string, sobrenome: string, altura: number){

        super(nome, sobrenome)

        this.altura = altura

    }

    getNomeCompleto(): string {

        return this.nome + ' ' + this.sobrenome

    }

}

let x = new Tronco('issac', 'cabral', 1.77)
```
[[11-Atributos_somente_leitura]]