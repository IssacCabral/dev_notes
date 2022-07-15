- No arquivo de rotas, podemos criar um grupo de rotas e definir um prefixo:
```typescript
import Route from '@ioc:Adonis/Core/Route'

Route.where('id', Route.matchers.number())

Route.group(() => {
  Route.get('/users', 'UsersController.index')
  Route.get('/users/:id', 'UsersController.show')
  Route.put('/users/:id', 'UsersController.update')
  Route.post('/users', 'UsersController.store')
  Route.delete('/users/:id', 'UsersController.destroy')
}).prefix('v1/api')
```

Mas também podemos resumir isso tudo assim:
- Como criamos os controladores com o comando _node ace make:controller [Controller_name] -r_ , os métodos estão obedecendo a nomenclatura correta para podermos usar o _Route.resource_
```typescript
import Route from '@ioc:Adonis/Core/Route'

Route.where('id', Route.matchers.number())

Route.group(() => {
  Route.resource('/users', 'UsersController')
}).prefix('v1/api')
```

Como estamos trabalhando com API's e os métodos create e edit não estão sendo usados, podemos passar o método _apiOnly_ para que o Adonis não gaste recurso procurando por esses métodos.

```ts
Route.resource('/users', 'UsersController').apiOnly()
```

Outra coisa que também podemos fazer é, filtrar as rotas:
passamos o método _only_ falando as únicas rotas que o controlador tem.

```ts
Route.resource('/users', 'UsersController').only(['index', 'store', 'show', 'update', 'destroy'])
```

E se tivermos todos os métodos, exceto... 

```ts
Route.resource('/users', 'UsersController').except(['create', 'edit'])
```