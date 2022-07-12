Agora vamos ver os dois casos: como montar uma distribuição praticamente do zero utilizando somente instruções através do _dockerfile_ e outra realizando modificações em uma imagem já existente e salvando em uma imagem nova.

## Vamos começar do começo então, *dockerfile*!
Vamos montar a nossa primeira imagem utilizando como roteiro de criação um _dockerfile_
Para começar, vamos criar um diretório chamado "/root/Dockerfiles".

```bash
# mkdir /root/Dockerfiles
```

Agora começaremos a criação do nosso _dockerfile_, nosso mapa de criação da imagem. Para que possamos organizá-lo melhor, vamos criar um diretório chamado "apache", onde guardaremos esse nosso primeiro exemplo:

```bash
# cd /root/Dockerfiles/
# mkdir apache
```

Por enquanto, vamos apenas criar um arquivo chamado "Dockerfile"

```bash
FROM debian:10

RUN apt-get update && apt-get install -y apache2 && apt-get clean

ENV APACHE_LOCK_DIR="/var/lock"

ENV APACHE_PID_FILE="/var/run/apache2.pid"

ENV APACHE_RUN_USER="www-data"

ENV APACHE_RUN_GROUP="www-data"

ENV APACHE_LOG_DIR="/var/log/apache2"

LABEL description="Webserver"

VOLUME /var/www/html/

EXPOSE 80
```

Muito bom! Agora que você já adicionou as informações conforme o exemplo, vamos entender cada seção utilizada nesse nosso primeiro _dockerfile_:

-   **FROM** -- Indica a imagem a servir como base.
    
-   **RUN** -- Lista de comandos que deseja executar na criação da imagem.
    
-   **ENV** -- Define variáveis de ambiente.
    
-   **LABEL** -- Adiciona _metadata_ à imagem, como descrição, versão, etc.
    
-   **VOLUME** -- Define um volume a ser montado no _container._
    

Após a criação do arquivo, vamos _buildar_ (construir a nossa imagem) da seguinte forma:

```bash
# docker build .
```

A nossa imagem foi criada! Porém, temos um problema. :/

A imagem foi criada e está totalmente funcional, mas, quando a _buildamos_, não passamos o parâmetro "-t", que é o responsável por adicionar uma _tag_ ("nome:versão") à imagem.

Vamos executar novamente o _build_, porém passando o parâmetro '-t', conforme o exemplo a seguir:

```bash
# docker build -t linuxtips/apache:1.0 .
```

Vamos executar um _container_ utilizando nossa imagem como base:

```bash
# docker run -ti linuxtips/apache:1.0
```

# Exemplo com imagem
criar um arquivo Dockerfile, e dentro dele escrever assim
```bash
FROM nginx:latest

WORKDIR /app

RUN apt-get update && apt-get install vim -y

COPY html/ /usr/share/nginx/html
```

Onde tem COPY estamos definindo o volume, onde tem _html/_ estamos dizendo onde iremos apontar no nosso host, referente a pasta html de dentro do container. Nesse exemplo, o arquivo Dockerfile já estava na mesma pasta do _html/_

após isso, buildamos a imagem com o seguinte comando. **atente de usar esse comando no mesmo diretório de onde está o arquivo Dockerfile, para que o build seja efetuado corretamente**

```bash
docker build -t issac/nginx-vim:latest .
```
após isso, criamos um container e utilizamos essa imagem:
```bash
docker run -it issac/nginx-vim bash
```