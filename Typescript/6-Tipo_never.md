# Conhecendo o tipo never
Esse **_type_** indica que algo nunca deve ocorrer. É isso mesmo, nós temos um **_type_** no TypeScript chamado _never_, que indica que uma função **_nunca_** deve retornar algo e que é diferente do **_type_** **void**.
- Nós podemos utilizar o type never em funções sem retorno ou que retornam algum erro

```ts
function carregandoGame(): never {
    while (true) {
        console.log("Carregando todos processos de um game!");
    }
}
```

- Outro exemplo:
```ts
function teste(): never {

    throw new Error()

}

function Erro(mensagem: string): never {

    throw new Error(mensagem)

}

function exemplo(arg1: any, arg2: any): boolean {

    if (typeof arg1 === typeof arg2) {

        return true

    }

    else if (typeof arg1 !== 'object') {

        return false

    }

    Erro('Os argumentos são diferntes e arg1 é do tipo objeto')

}
```
[[7-Spread_destructuring]]