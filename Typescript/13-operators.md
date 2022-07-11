# Optional Chaining
- Utilizamos o Optional Chaining quando estamos trabalhando com um objeto que existe a possibilidade do mesmo ser *null* ou *undefined*.

```ts
let x = foo?.bar.baz()
```

- Mais claramente, esse trecho de código é o mesmo que escrever o seguinte.

```ts
let x = foo === null || foo === undefined ? undefined : foo.bar.baz()
```

# Operador de Coalescência Nula
- O **operador de coalescência nula (`??`)** é um operador lógico que retorna o seu operando do lado direito quando o seu operador do lado esquerdo é `null` ou `undefined`. Caso contrário, ele retorna o seu operando do lado esquerdo.

```ts
const foo = null ?? 'default string';
console.log(foo);
// expected output: "default string"

const baz = 0 ?? 42;
console.log(baz);
// expected output: 0
```

- Endereçando um valor padrão à variável

Inicialmente, quando se deseja endereçar um valor padrão à variável, um padrão comum é utilizar o operador lógico OR ||
```ts
let foo;

//  foo nunca é endereçado a nenhum valor, portanto, ainda está indefinido
let someDummyText = foo || 'Hello!';
```

Entretanto, devido ao `||` ser um operador lógico booleano, o operando do lado esquerdo é coagido para um valor booleano para sua avaliação e qualquer valor _falseável_ (`0`, `''`, `NaN`, `null`, `undefined`) não é retornado. Este comportamento pode causar consequencias inesperadas se você considerar `0`, `''`, ou `NaN` como valores válidos.

# Non-Null Assertion
- Um novo operador de expressão pós-correção pode ser usado para afirmar que seu operando é não-nulo e não indefinido em contextos onde o verificador de tipo é incapaz de concluir esse fato.

```ts
// Nesse caso eu tenho certeza de que o meu obj possui a propriedade address

function addAddress(obj: IUser){

    obj.address = {

        address: "Rua do pó",

        city: "Cidade do pó"
    }  
}

addAddress(obj)

const cityNonNull = obj.address!.city
```