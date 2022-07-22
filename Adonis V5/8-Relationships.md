### HasOne
Aqui estamos relacionando um _User_ com um _Profile_
Dentro do model de _User_ importamos o model de Profile, e criamos o seguinte relacionamento:
```ts
@hasOne(() => Profile)
public profile: HasOne<typeof Profile>
```
assim, estamos inserindo o id de _User_ dentro de _Profile_

--> 1 usuário tem 1 perfil e apenas 1 perfil
- Usando o facebook de exemplo, vamos entender que quando você loga, você só tem 1 perfil e somente 1 perfil. Para que você crie outro perfil, é necessário que você crie outra conta. Então, 1 usuário em específico só pode ter 1 perfil

### BelongsTo
E se a gente quiser fazer um crud um relacionamento com os perfis? 
Se a gente quiser retornar o usuário à qual um perfil pertence? Nesse caso utilizamos o `belongsTo`
Dentro do model de _Profile_:
```ts
@belongsTo(() => User)
public user: BelongsTo<typeof User>
```

--> 1 perfil pertence à 1 usuário

### HasMany
1 _User_ possui vários _Post_
_user_id_ dentro de _Post_

```ts
@hasMany(() => Post)
public posts: HasMany<typeof Post>
```

E quando quisermos falar que um Post pertence à um _User_ , se precisarmos pegar isso em algum retorno, devemos identificar que esse _Post_ pertence à um _User_

```ts
@belongsTo(() => User)
public user: BelongsTo<typeof User>
```

### ManyToMany
1 skill pode ser de vários devs e 1 dev pode ter várias skills
```ts
@manyToMany(() => Skill, {
	pivotTable: 'user_skills',
})
public skills: ManyToMany<typeof Skill>
```

##  Preload relationship

O pré-carregamento permite que você busque os dados de relacionamento ao lado da consulta principal. Por exemplo: Selecione todos os usuários e seus perfis ao mesmo tempo.`preload`

O valor da propriedade de relacionamento é uma matriz da instância de modelo relacionada para todos os outros tipos de relacionamento.

```ts
const users = await User
  .query()
  .preload('profile')

users.forEach((user) => {
  console.log(user.profile)
})
```

Você pode modificar a consulta de relacionamento passando um retorno de chamada opcional para o método.`preload`

```ts
const users = await User
  .query()
  .preload('profile', (profileQuery) => {
    profileQuery.where('isActive', true)
  })
```

### Pré-carregar vários relacionamentos

Você pode múltiplos relacionamentos juntos chamando o método para várias vezes. Por exemplo:`preload` `preload`

```ts
const users = await User
  .query()
  .preload('profile')
  .preload('posts')
```

### Lazy load relationships

Juntamente com o pré-carregamento, você também pode carregar relacionamentos diretamente de uma instância de modelo.

```ts
const user = await User.find(1)

// Lazy load the profile
await user.load('profile')
console.log(user.profile) // Profile | null

// Lazy load the posts
await user.load('posts')
console.log(user.posts) // Post[]
```

Assim como o método, o método também aceita um retorno de chamada opcional para modificar a consulta de relacionamento.`preload` `load`

```ts
await user.load('profile', (profileQuery) => {
  profileQuery.where('isActive', true)
})
```

Você pode carregar vários relacionamentos ligando para o método várias vezes ou pegando uma instância do carregador de relacionamento subjacente.`load`

```ts
// Calling "load" method multiple times
await user.load('profile')
await user.load('posts')
```

## Relationship query builder

Você também pode acessar o construtor de consultas para um relacionamento usando o método. As consultas de relacionamento são sempre escopo para uma determinada instância de modelo pai.`related`

Lucid adicionará automaticamente a cláusula para limitar as postagens ao usuário dado no exemplo a seguir.`where` 

```ts
const user = await User.find(1)
const posts = await user.related('posts').query()
```

O método retorna uma instância padrão de construtor de consulta, e você pode acorrentar quaisquer métodos a ele para adicionar restrições adicionais.`query`

```ts
const posts = await user
  .related('posts')
  .query()
  .where('isPublished', true)
  .paginate(1)
```

## Criar relacionamentos

Você pode criar relações entre dois modelos usando a API de persistência de relacionamentos. Certifique-se também de verificar os [documentos da API](https://docs.adonisjs.com/reference/orm/relations/has-one#query-client) para visualizar todos os métodos disponíveis.

### create
No exemplo a seguir, criamos um novo comentário e o vinculamos ao post ao mesmo tempo. O método aceita que um objeto JavaScript simples persista. O valor da chave estrangeira é definido automaticamente.`create`

```ts
const post = await Post.findOrFail(1)
const comment = await post.related('comments').create({
  body: 'This is a great post'
})

console.log(comment.postId === post.id) // true
```

### save

A seguir, um exemplo usando o método. O método precisa de uma instância do modelo relacionado. O valor da chave estrangeira é definido automaticamente.`save``save`

```ts
const post = await Post.findOrFail(1)

const comment = new Comment()
comment.body = 'This is a great post'

await post.related('comments').save(comment)

console.log(comment.postId === post.id) // true
```

### attach

O método é exclusivo para um relacionamento. Ele permite criar uma relação entre dois modelos persistentes dentro da mesa de pivô.`attach` `manyToMany`

O método só precisa do modelo relacionado para formar a relação dentro da tabela de pivô.`attach` `id`

```ts
const user = await User.find(1)
const skill = await Skill.find(1)

// Performs insert query inside the pivot table
await user.related('skills').attach([skill.id])
```

