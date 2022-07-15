Assim como no express, no Adonis podemos utilizar variáveis de ambiente. Mas o Adonis tem um suporte bem legal para trabalhar com elas.

Pra começar, um projeto Adonis tem um arquivo chamado env.ts que lá podemos definir as as nossas variáveis de ambiente que inserirmos no arquivo .env e podemos validar as variáveis lá mesmo:

```ts
// no arquivo env.ts
import Env from '@ioc:Adonis/Core/Env'

export default Env.rules({
  HOST: Env.schema.string({ format: 'host' }),
  PORT: Env.schema.number(),
  APP_KEY: Env.schema.string(),
  APP_NAME: Env.schema.string(),
  DRIVE_DISK: Env.schema.enum(['local'] as const),
  NODE_ENV: Env.schema.enum(['development', 'production', 'test'] as const),
  E_MAIL: Env.schema.string({format: 'email'})
})
```

E em algum arquivo/controller qualquer podemos trabalhar com as nossas variáveis de ambiente:

```ts
import Env from '@ioc:Adonis/Core/Env'

export default class UsersController {
  public async index({response}: HttpContextContract) {
    const email = Env.get('E_MAIL')
    response.ok({message: email})
  }
}
```

### Reutilizando variáveis de ambiente
```ts
PORT=3333
HOST-A=0.0.0.0
NODE_ENV=development
APP_KEY=8XRXnm1F30g_L-RzCMkSjE4S2MAdTZhP
DRIVE_DISK=local
E_MAIL=clidenorissac@gmail.com
```

```ts
PORT=3333
HOST=0.0.0.0
URL=${HOST-A}:$PORT
NODE_ENV=development
APP_KEY=8XRXnm1F30g_L-RzCMkSjE4S2MAdTZhP
DRIVE_DISK=local

E_MAIL=clidenorissac@gmail.com
```