### O que são Seeders?
Seeder é um semeador, seeds são sementes
- Popular o banco de maneira prévia
- Criar dados através de um comando

#### Criando seeders
```bash
node ace make:seeder [seeder_name]
```
#### Executando uma seed
```bash
node ace db:seed
```
E agora, supondo que tenhamos várias seeds e queiramos executar apenas uma em específico. Devemos utilizar o seguinte comando: e entre aspas devemos passar o path em que se encontra nossa seed dentro do projeto
```bash
node ace db:seed --files "database/seeders/Role.ts"
```
E se eu quiser executar algumas seeders? mais de uma, mas não todas
```bash
node ace db:seed -i
```
- através da CLI nós escolhemos quais seeds queremos executar

#### Método updateOrCreateMany

Na definição de uma seeder, usamos o método updateOrCreateMany para atualizar ou criar muitos. Então, para fazer uma operação idempotente, primeiramente, devemos identificar qual é a chave única dentro da nossa tabela. No caso da _Roles_, o campo único é o _name_

Tendo essa chave única, passamos ela para o método _updateOrCreateMany_ como primeiro parâmetro. Ou seja, quero criar registro se essa chave não for encontrada. Caso ela seja encontrada, será feito um update

```ts
export default class extends BaseSeeder {
  public async run () {
    const uniqueKey = 'name'

    await Role.updateOrCreateMany(uniqueKey, [
      {
        name: 'admin',
        description: 'Access all resource of the system'
      },
      {
        name: 'client',
        description: 'Access to shopping and product features only'
      },
      {
        name: 'employee',
        description: 'Access to sales resources only'
      }
    ])
  }
}
```

#### Método updateOrCreate
Quando eu vou fazer apenas um _updateOrCreate_, eu preciso especificar tanto a chave que quero mudar, quanto o valor a ser alterado. Então, vai ser dado um update sempre que o email for igual ao o que eu estou tentando registrar novamente.

```ts
export default class extends BaseSeeder {
  public async run () {
    // -------------- USER ADMIN ----------- //
    const searchKeyAdmin = {email: 'admin@email.com'}
    const userAdmin = await User.updateOrCreate(searchKeyAdmin, {
      secure_id: uuidv4(),
      name: 'Admin',
      cpf: '000.000.000-00',
      email: 'admin@email.com',
      password: 'secret'
    })

    const roleAdmin = await Role.findBy('name', 'admin')
    if(roleAdmin) await userAdmin.related('roles').attach([roleAdmin.id])

    // -------------- USER CLIENT ----------- //
    const searchKeyClient = {email: 'client@email.com'}
    const userClient = await User.updateOrCreate(searchKeyClient, {
      secure_id: uuidv4(),
      name: 'Client',
      cpf: '000.000.000-01',
      email: 'client@email.com',
      password: 'secret'
    })

    const roleClient = await Role.findBy('name', 'client')
    if(roleClient) await userClient.related('roles').attach([roleClient.id])

    // -------------- USER EMPLOYEE ----------- //
    const searchKeyEmployee = {email: 'employee@email.com'}
    const userEmployee = await User.updateOrCreate(searchKeyEmployee, {
      secure_id: uuidv4(),
      name: 'Employee',
      cpf: '000.000.000-02',
      email: 'employee@email.com',
      password: 'secret'
    })

    const roleEmployee = await Role.findBy('name', 'employee')
    if(roleEmployee) await userEmployee.related('roles').attach([roleEmployee.id])
  }
  
}
```