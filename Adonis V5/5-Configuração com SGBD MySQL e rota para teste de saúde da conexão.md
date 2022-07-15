Configurações:
```bash
yarn add @adonisjs/lucid
node ace configure @adonisjs/lucid
```

```ts
import Database from '@ioc:Adonis/Lucid/Database'

// rota para testar a conexão com o banco
Route.get('/test_db_connections', async ({response}: HttpContextContract) => {
  await Database.report().then(({health}) => {
    const {healthy, message} = health

    if(healthy) return response.ok({message})

    return response.status(500).json({message})
  })
})
```