# Tipos Primitivos
```script
type Primitive = string | boolean | number | bigint | symbol | null | undefined
```

**Qualquer outro tipo não é primitivo**

- Object (nativo do Javascript, não deve ser usado para tipagem)
- object (pode ser usado para tipagem)
- Class
- qualquer outra modelagem de object

# Tipos implíticos e explícitos

```js
const impl_string = "typescript"

const impl_number = 5.5

const impl_boolean = true

const impl_obj = {name: "typescript"}

  

const expl_string: string = "typescript"

const expl_number: number = 5.5

const expl_boolean: boolean = true

const expl_obj: {name: string} = {name: "typescript"}

  

const num1: number | undefined = undefined

  

const num2: number = num1!
```

## Tipando Arrays

```js
const frutas: Array<string> = []

const frutas1: string[] = []

const frutas2: [] = []

  
// Array de string ou number
const misto: (string | number)[] = []

const misto2: Array<string | number> = []

  

// Array de arrays do tipo string

const inception: Array<Array<string>> = []

const inception2: string[][] = []

const inception3: Array<string[]> = []


// tipo string ou number
const inception4: Array<(string | number)[]> = []

  
const inception5: Array<string[] | string | number[]> = [['test'], 'text', [1,2,3]]
```
[[2-Objetos]]