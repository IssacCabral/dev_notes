## Criar um validator
```bash
node ace make:validator User/store
```

## Regex
```bash
// REGEX PARA NOMES regex(/^[ a-zA-ZÀ-ÿ\u00f1\u00d1]*$/g)

// REGEX PARA CPF /^\d{3}.\d{3}.\d{3}-\d{2}$/

// REGEX PARA CEP /^[0-9]{5}-[0-9]{3}$/
```

## Custom validators
```ts
export default class MessagesCustom {
2  public messages = {
3    //Pattern message for Types
4    'string': '{{ field }} field is invalid string',
5    'boolean': '{{ field }} field is invalid boolean',
6    'number': '{{ field }} field is invalid number',
7    'date': '{{ field }} field is invalid date',
8    'enum': 'the value must be one of {{ options.choices }}',
9    'enumSet': 'the value must be one of {{ options.choices }}',
10    'file': '{{ field }} field is invalid file',
11    'file.size': 'The file size must be under {{ options.size }}',
12    'file.extname': 'The file must have one of {{ options.extnames }} extension names',
13
14    'array': '{{ field }} field is invalid array',
15    'object': '{{ field }} field is invalid object',
16
17    //Pattern message for rules
18    'required': '{{ field }} field is required',
19    'requiredIfExists': '{{ options.otherField }} requires {{ field }}',
20    'requiredIfExistsAll': '{{ options.otherFields }} requires {{ field }}',
21    'requiredWhen': '{{ field }} is required when {{ otherField }}{{ operator }}{{ values }}',
22
23    'alpha': '{{ field }} field only accepts letters',
24    'confirmed': '{{ field }} field must be the same as the confirmation field',
25    'email': '{{ field }} field should be a valid email',
26    'exists': '{{ field }} not found in us database',
27    'unique': '{{ field }} already exists',
28    'maxLength': '{{ field }} field must be up to {{ options.maxLength }}',
29    'minLength': '{{ field }} field must be at least {{ options.minLength }}',
30    'regex': '{{ field }} field with invalid format',
31  }
32}
```

No validator de produto foi feito algo diferente:

Nós podemos falar qual é o mínimo que esse array tem que ter. Ou seja, eu quero que todo produto contenha no mínimo 1 categoria. E dentro de members, eu sei que dentro desse array eu vou receber um arrray de strings, e verifico se existe esse name especificado em categories dentro do array, lá na tabela de categorias. 

Então se eu especificar um name como: 'Alimentícios' e não tiver essa categoria cadastrada, será acusado um erro informando que não encontrou esse parâmetro dentro dessa tabela. 

```ts
public schema = schema.create({
    name: schema.string({ trim: true }, [
      rules.maxLength(50),
      rules.minLength(3),
      rules.regex(/^[ a-zA-ZÀ-ÿ\u00f1\u00d1]*$/g),
    ]),

    code: schema.string({ trim: true }, [
      rules.unique({ table: 'products', column: 'code' }),
      rules.maxLength(250)
    ]),

    categories: schema
      .array([rules.minLength(1)])
      .members(
        schema.string({trim: true}, [rules.exists({table: 'categories', column: 'name'})])
      )

  })
```

