Antes de tudo, só gostaria de mostrar de como uma rota _index_ para listar usuários paginados ou não pode se parecer:

```ts
public async index({request, response}: HttpContextContract) {
    const {page, perPage, noPaginate} = request.qs()

    if(noPaginate){
      return await User.query()
        .preload('addresses')
        .preload('roles', (roleTable) => {
        roleTable.select('id', 'name')
      })
    }

    try{
      const users = await User.query()
        .preload('addresses')
        .preload('roles', (roleTable) => {
        roleTable.select('id', 'name')
      }).paginate(page || 1, perPage || 10)

      return response.ok(users)
    } catch(error){
      return response.badRequest({message: 'error in list users', originalError: error.message})
    }
  }
```

# Filters
### Instalação e configuração do Adonis Lucid filter

```bash
yarn add adonis-lucid-filter
node ace configure adonis-lucid-filter
```

### Criando um novo filter

```bash
node ace make:filter UserFilter
```

Antes de usarmos esse filter no User, devemos informar que a classe User vai extender o nosso filter:

```ts
import {compose} from '@ioc:Adonis/Core/Helpers'
import {Filterable} from '@ioc:Adonis/Addons/LucidFilter'
import {UserFilter} from '../Models/Filter/UserFilter'
```

e na classe de user:

```ts
export default class User extends compose(BaseModel, Filterable) {
  public static $filter = () => UserFilter
  
  ...// códigos e métodos
}
```



