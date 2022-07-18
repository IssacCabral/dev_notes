### Hooks
Hooks são ciclos de vida na aplicação

- beforeSave
- beforeCreate
- beforeUpdate
- beforeDelete
- beforePaginate
- beforeFetch
- beforeFind

Para todo _before_ tem um _after_

- Definindo um uuid antes de criar um registro na tabela de Users

```ts
@beforeCreate()
public static assignUuid(user: User){
  user.secure_id = uuidv4()
}
```
- Hasheando a senha antes de salvar um registro na tabela de Users

```ts
@beforeSave()
public static async hashPassword(user: User){
  if(user.$dirty.password){
    user.password = await Hash.make(user.password)
  }
}
```

**Diferença entre _beforeCreate_ e _beforeSave_ **

O _beforeSave_ sempre vai executar essa função antes de salvar. Já o _beforeCreate_ só é executada uma vez, apenas na hora da criação. Ou seja, o _beforeSave_ pode ser executado tanto em caso de _update_ como em caso de _create_ 

#### Entendendo a propriedade $dirty

O _Hook_ é chamado toda vez que um novo usuário é **criado** ou **atualizado** usando a instância do modelo.`beforeSave`

Durante a atualização, você pode ter atualizado outras propriedades, mas NÃO a senha de usuário. Portanto, não há necessidade de re-hash o hash existente, e é por isso que usando o objeto.`$dirty`

O objeto contém apenas os valores alterados. Assim, você pode verificar se a senha foi alterada e, em seguida, hash o novo valor.`$dirty`

#### Executando Seeders apenas em um ambiente específico
dentro de sua classe _seeder_, passe um dos seguintes atributos como true:
- 
```ts
public static developmentOnly = true
```