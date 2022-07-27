**Instalação**
```bash
yarn create adonis-ts-app hello-world
```

uma nova linha está sendo adicionada
outra linha adicionada
xxx
**Execução**
```bash
node ace serve --watch
```

## Criar um controlador
```bash
node ace make:controller [Controller_name]
```

## Criar um controlador com todos os recursos

```bash
node ace make:controller [Controller_name] -r
```
Dessa maneira, o Adonis cria um controller com todos os métodos de CRUD.
- index
- create
- store
- show
- edit
- update
- destroy

`Diferença entre create e store`

Diferença => Create serve quando você usa o MVC no adonisjs, ou seja, ele abre um formulário html para o usuário preencher os dados, como estamos codando uma API, vamos utilizar o store
    
    O mesmo para edit e update
    
    update é da API, edit é do front-end

    API's nós não usamos o corpo da requisição para passar os valores do formulário de um User por exemplo???
    
    => Com certeza, não só usamos, como devemos usar!

## Listar as rotas cadastradas no sistema
```bash
node ace list:routes --json
```