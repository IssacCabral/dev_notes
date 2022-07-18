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

