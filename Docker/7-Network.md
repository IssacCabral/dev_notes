# Networks
network dentro do docker, nada mais é do que uma rede interna. O docker tem uma rede interna para comunicação entre os containers. Um exemplo: você pode ter um container rodando uma aplicação Node e outro container rodando o seu banco de dados Mysql. Pois é interessante cada container executar uma coisa só

### Listar os networks
```bash
docker network ls
```

- Sempre que você subir um container, a network dele será padrão bridge