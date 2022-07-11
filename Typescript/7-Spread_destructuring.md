### O código é auto explicativo
```ts
function chamadaAPI(usr: Usuario){

    const idade = 10

    const {idade: usrIdade, maiorDeIdade, ...resto} = usr

}

const arr: string[] = ['primeiro', 'segundo', 'terceiro']

const [valor1, ...resto] = arr

const [, valor] = arr // arr[1]

let outroArr = [...resto]
```
[[8-Promises]]