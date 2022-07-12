## Para que serve o Volume?
O volume vai fazer uma conexão de um diretório da nossa máquina, para um diretório dentro do container que está em execução

A principal função do volume é persistir os dados. Diferentemente do _filesystem_ do _container,_ que é volátil e toda informação escrita nele é perdida quando o _container_ morre, quando você escreve em um volume aquele dado continua lá, independentemente do estado do _container_.

Existem algumas particularidades entre os volumes e _containers_ que valem a pena ser mencionadas:

-   O volume é inicializado quando o _container_ é criado.    
-   Caso ocorra de já haver dados no diretório em que você está montando como volume, ou seja, se o diretório já existe e está "populado" na imagem base, aqueles dados serão copiados para o volume.    
-   Um volume pode ser reusado e compartilhado entre _containers_.    
-   Alterações em um volume são feitas diretamente no volume.
-   Alterações em um volume não irão com a imagem quando você fizer uma cópia ou _snapshot_ de um _container_.
-   Volumes continuam a existir mesmo se você deletar o _container_.

## Volumes nomeados
Temos duas Opções:
- Criar o volume antes de criar e iniciar o container
- Criar o volume no momento da criação e inibialização do container

Mas em ambas as situações devemos utilizar duas flags:
- -v ou --volume
- --mount

Se você precisa passar informações sobre driver de volume, deve utilizar --mount

### Entendendo Melhor Volumes
A ideia aqui é a seguinte: Subir um container nginx, e na pasta onde deveriam ficar os arquivos HTML, eu vou apontar para um pasta que está no meu computador localmente.

![img](/Docker/images/1.png)

```bash
docker run -d -p 80:80 -v [host_local]:[path_da_pasta_no_container] nginx
```

**Exemplo Real**
```bash
docker run -d -p 80:80 -v C:\Users\PICHAU\desktop\volume\html:/usr/share/nginx/html nginx
```

**Usando o mount**
```bash
docker run -d -p 80:80 --mount type=bind,source=C:\Users\PICHAU\desktop\volume\html,target=/usr/share/nginx/html nginx
```
**Nesse primeiro caso:** Escrevemos dentro do container. Ou seja, peguei meu código e escrevi algo para dentro do container. E o contrário é possível? ou seja, o container pode escrever dentro do meu computador?

A resposta é sim! vamos usar o exemplo do mySql.

```bash
docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -v C:\Users\PICHAU\desktop\mysql-data:/var/lib/mysql mysql
```

Com isso aprendemos que tanto podemos escrever em um container, como um container pode escrever no nosso computador







