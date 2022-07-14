## Parâmetros Obrigatórios
```ts
import Route from '@ioc:Adonis/Core/Route'

Route.get('/hello_world/:id', 'HelloWorldsController.hello')
```

## Parâmetros opcionais
```ts
import Route from '@ioc:Adonis/Core/Route'

Route.get('/hello_world/:id?', 'HelloWorldsController.hello')
```

## Parâmetro coringa
Esse é um parâmetro coringa e podemos passar qualquer coisa para ele
```ts
import Route from '@ioc:Adonis/Core/Route'

Route.get('/hello_world/*', 'HelloWorldsController.hello')
```
Podemos retornar um array com os parâmetros passados a partir de um parâmetro coringa dessa maneira:
```ts
import type { HttpContextContract } from '@ioc:Adonis/Core/HttpContext'

export default class HelloWorldsController {
    public async hello({params}: HttpContextContract){

        const paramsReturn = params['*']
        
        return {message: paramsReturn}
    }
}
```

## Validação de parâmetros
Através desse Regex, pegamos o id, somente quando o id for no formato numérico 
```ts
import Route from '@ioc:Adonis/Core/Route'

Route.get('/hello_world/:id', 'HelloWorldsController.hello').where('id', /^[0-9]+$/)
```

Podemos definir essa condição de maneira global também:
```ts
import Route from '@ioc:Adonis/Core/Route'

Route.where('id', /^[0-9]+$/)

Route.get('/hello_world/:id', 'HelloWorldsController.hello')
```

#### Olha que legal!
- validar esses parâmetros e convertê-lo para um valor numérico:
para isso precisamos definir dois parâmetros dentro do global:
o _match_ que indica qual a validação que deve ser feita, e o _cast_ indica a conversão do valor, **Antes de chegar no controller**

```ts
import Route from '@ioc:Adonis/Core/Route'

Route.where('id', {
  match: /^[0-9]+$/,
  cast: (id) => Number(id)
})

Route.get('/hello_world/:id', 'HelloWorldsController.hello')
```

Dessa forma todos os ids informados no parâmetro da requisição, chegarão no _controller_ como _numbers_

- Podemos resumir isso tudo em:

```ts
import Route from '@ioc:Adonis/Core/Route'

Route.where('id', Route.matchers.number())

Route.get('/hello_world/:id', 'HelloWorldsController.hello')
```