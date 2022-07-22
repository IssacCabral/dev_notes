# Operações CRUD

## Create
Você pode criar e persistir novos registros no banco de dados, primeiro atribuindo valores à instância do modelo e, em seguida, chamando o método.`save`

O método realiza a consulta **INSERT** ao persistir a instância do modelo pela primeira vez e realiza a consulta **UPDATE** quando o modelo persistir.`save`

```ts
import User from 'App/Models/User'
const user = new User()

// Assign username and email
user.username = 'virk'
user.email = 'virk@adonisjs.com'

// Insert to the database
await user.save()

console.log(user.$isPersisted) // true
```

O método cria a instância do modelo e persiste no banco de dados de uma só vez.`static create`

```ts
import User from 'App/Models/User'

const user = await User.create({
  username: 'virk',
  email: 'virk@adonisjs.com',
})

console.log(user.$isPersisted) // true
```

## Read

Você pode consultar a tabela do banco de dados usando um dos seguintes métodos estáticos.

### All

Pegue todos os usuários do banco de dados. O método retorna uma série de instâncias de modelo.

```ts
const user = await User.all()
// SQL: SELECT * from "users" ORDER BY "id" DESC;
```

### find

Encontre um registro usando a chave principal. O método retorna uma instância de modelo ou nula (quando não são encontrados registros).

```ts
const user = await User.find(1)
// SQL: SELECT * from "users" WHERE "id" = 1 LIMIT 1;
```

### findBy

Encontre um registro por um nome de coluna e seu valor. Semelhante ao método, este método também retorna uma instância de modelo ou .`find` `null`

```ts
const user = await User.findBy('email', 'virk@adonisjs.com')
// SQL: SELECT * from "users" WHERE "email" = 'virk@adonisjs.com' LIMIT 1;
```

### first

Pegue o primeiro registro do banco de dados. Retorna quando não há registros.`null`

```ts
const user = await User.first()
// SQL: SELECT * from "users" LIMIT 1;
```

### orFail variation

Você também pode usar a variação para os métodos de encontrar. Isso levanta uma exceção quando nenhuma linha é encontrada.`orFail`

```ts
const user = await User.findOrFail(1)
const user = await User.firstOrFail()
const user = await User.findByOrFail('email', 'virk@adonisjs.com')
```

### Using the query builder

Os métodos estáticos acima mencionados abrangem os casos de uso comum para consulta ao banco de dados. No entanto, você não está apenas limitado a esses métodos e também pode aproveitar a API do construtor de consultas para fazer consultas SQL avançadas.

Você pode obter uma instância de um construtor de consultas para o seu modelo usando o método.`.query`

```ts
const users = await User
  .query() // 👈now have access to all query builder methods
  .where('countryCode', 'IN')
  .orWhereNull('countryCode')
```

## Update

A maneira padrão de executar atualizações usando o modelo é procurar o registro e, em seguida, atualizá-lo/persisti-lo para o banco de dados.

```ts
const user = await User.findOrFail(1)
user.lastLoginAt = DateTime.local() // Luxon dateTime is used

await user.save()
```


Além disso, você pode usar o método para definir todos os atributos de uma só vez e, em seguida, chamar o método.`merge` `save`

```ts
await user
  .merge({ lastLoginAt: DateTime.local() })
  .save()
```

#### Por que não usar a consulta de atualização diretamente?

Outra maneira de atualizar os registros é realizar uma atualização usando o construtor de consulta manualmente. Por exemplo

```ts
await User
  .query()
  .where('id', 1)
  .update({ lastLoginAt: new Date() })
```

No entanto, atualizar registros diretamente não aciona nenhum gancho de modelo e nem atualiza automaticamente os horários.

Recomendamos não enfatizar muito na consulta extra, a menos que lidar com milhões de atualizações por segundo e feliz deixando os recursos do modelo.`select`

## Delete

Como a operação, primeiro você o pega no banco de dados e exclui a linha. Por exemplo`update`

```ts
const user = await User.findOrFail(1)
await user.delete()
```

Novamente, para os _Hooks_ funcionarem, Lucid precisa primeiro da instância do modelo. Se você decidir usar o construtor de consulta diretamente, então o modelo não disparará nenhum _Hook_.

No entanto, a abordagem do construtor de consulta direta pode ajudar a realizar exclusões em massa.

```ts
await User.query().where('isVerified', false).delete()
```

# Modelos de serialização

Se você criar um servidor API, deseja converter as instâncias do modelo em objetos JSON simples antes de enviá-los ao cliente em resposta.

O processo de transformação de instâncias de classe para objetos JSON simples é conhecido como serialização.

## Modelos de serialização

Você pode serializar um modelo ligando para o método ou para o método. Por exemplo:`serialize` `toJSON`

```ts
const post = await Post.find(1)
const postJSON = post.serialize()
```

Você pode serializar uma série de instâncias de modelo chamando o método.`Array.map`

```ts
const posts = await Post.all()
const postsJSON = posts.map((post) => post.serialize())
```

## Serializando relacionamentos

Os relacionamentos são serializados automaticamente toda vez que você serializa uma instância de modelo. Por exemplo:`preloaded`

```ts
const posts = await Post
  .query()
  .preload('comments')

const postsJSON = posts.map((post) => post.serialize())
```

No exemplo acima, as postagens serão serializadas para o objeto post. Por exemplo:`comments`

```json
{
  id: 1,
  title: 'Adonis 101',
  comments: [{
    id: 1,
    content: 'Nice article'
  }]
}
```



