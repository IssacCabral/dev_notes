### Comando para criar uma nova migration
```bash
node ace make:migration [migration_name]
```

### Comando para rodar as migrations
```bash
node ace migration: run
```

### Desfazendo migrations para um lote
```bash
node ace migration:rollback
```
Quando executamos o código acima, estamos avisando ao Adonis para desfazer todas as migrations criadas para um lote(o número do lote pode ser verificado no DBeaver). Então se executarmos esse comando, todas as migrations dentro de um mesmo lote serão excluídas

- Se quisermos reverter um lote específico, basta passar a flag batch

```bash
node ace migration:rollback --batch=[lote_number]
```
**Cuidado** ao executar um rollback, ele executa o comando down dentro de cada migration. E isso consequentemente exclui os dados! Pode ser muito perigoso em ambiente de produção

Por isso o pessoal do Adonis criou um comando para desabilitar o rollback quando o seu código estiver em produção

Então, dentro das configurações do seu banco no projeto Adonis, você pode passar esse parâmetro:
```ts
migrations: {
        disableRollbacksInProduction: true
}
```

Essa condição é para quando o .env estiver configurado assim:

```bash
NODE_ENV=production
```

### Alterando migrations
```bash
node ace make:migration alter_cpf_in_[table_name] --table=[table_name]
```

### Renomear uma tabela
```bash
node ace make:migration alterName_Product_Categories
```

###  Apenas testar a migration sem alterar o banco de dados
```bash
node ace migration:run --dry-run
```