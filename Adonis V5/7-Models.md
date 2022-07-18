### Criando um Model
Podemos passar o nome do modelo do singular que o Adonis já procura lá no banco, no plural
- Se for passado a flag -m, ja é criado o _model_ e a _migration_
```bash
node ace make:model [tabela_que_o_model_se_relaciona]
```

As classes de modelo trabalham com _snake_case_ então ,se eu informo:
```ts
@column()
public secureId: uuidv4
```

o Adonis já procura lá na tabela, como se fosse assim:
```ts
@column()
public secure_id: uuidv4
```

### Definindo manualmente o nome da tabela lá no banco
Se ficarmos com medo do nome do _Model_ não seja encontrado lá no banco, podemos explicitar o nome da tabela lá no banco com uma variável estática no model:
```ts
public static table = 'table_name'
```

Se tivéssemos um outro banco de dados para determinada tabela, podemos definir o nome do banco em uma variável estática no model:
```ts
public static connection = 'pg'
```

