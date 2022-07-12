### Executando um container
Para que possamos executar um _container_, utilizamos o parâmetro "run" do comando "docker". Simples, não? :D

```bash
docker run hello-world
```

Apesar de ser uma tarefa simples, quando você executou o comando "docker run hello-world" foram necessárias quatro etapas para sua conclusão, vamos ver quais:

1.  O comando "docker" se comunica com o _daemon_ do Docker informando a ação desejada.
    
2.  O _daemon_ do Docker verifica se a imagem "hello-world" existe em seu _host_; caso ainda não, o Docker faz o _download_ da imagem diretamente do Docker Hub.
    
3.  O _daemon_ do Docker cria um novo _container_ utilizando a imagem que você acabou de baixar.
    
4.  O _daemon_ do Docker envia a saída para o comando "docker", que imprime a mensagem em seu terminal.

Muito bem, agora que nós já temos uma imagem em nosso _host_, como eu faço para visualizá-la?

Muito simples, basta digitar o seguinte comando:

```bash
root@linuxtips:~# docker image ls
REPOSITORY  TAG    IMAGE ID     CREATED  SIZE
hello-world latest 690ed74de00f 5 months 960 B

root@linuxtips:~#
```

Como você pode notar no código, a saída traz cinco colunas:

-   **REPOSITORY** -- O nome da imagem.
    
-   **TAG** -- A versão da imagem.
    
-   **IMAGE ID** -- Identificação da imagem.
    
-   **CREATED** -- Quando ela foi criada.
    
-   **SIZE** -- Tamanho da imagem.


Quando executamos o comando "docker run hello-world", ele criou o _container_, imprimiu a mensagem na tela e depois o _container_ foi finalizado automaticamente, ou seja, ele executou sua tarefa, que era exibir a mensagem, e depois foi finalizado.

Para ter certeza de que ele realmente foi finalizado, digite:

```bash
root@linuxtips:~# docker ps

CONTAINER ID IMAGE COMMAND CREATED STATUS PORT NAMES

root@linuxtips:~#
```

Com o "docker ps", você consegue visualizar todos os _containers_ em execução e ainda obter os detalhes sobre eles. A saída do "docker ps" é dividida em sete colunas; vamos conhecer o que elas nos dizem:

-   **CONTAINER ID** -- Identificação única do _container._
    
-   **IMAGE** -- A imagem que foi utilizada para a execução do _container._
    
-   **COMMAND** -- O comando em execução.
    
-   **CREATED** -- Quando ele foi criado.
    
-   **STATUS** -- O seu status atual.
    
-   **PORTS** -- A porta do _container_ e do _host_ que esse _container_ utiliza.
    
-   **NAMES** -- O nome do _container._
    

Uma opção interessante do "docker ps" é o parâmetro "-a".

```bash
root@linuxtips:~# docker ps -a

CONTAINER ID  IMAGE        COMMAND   CREATED    STATUS     PORTS      NAMES
6e45cf509282  hello-world  "/hello"  4 seconds  Exited(0)             tracted_ardinghelli

root@linuxtips:~#
```

Com a opção "-a" você consegue visualizar não somente os _containers_ em execução, como também _containers_ que estão parados ou que foram finalizados.

### Legal, quero mais!
Agora que vimos como criar um simples _container_, bem como visualizar as imagens e _containers_ que estão em nosso _host_, vamos criar um novo, porém conhecendo três parâmetros que irão trazer maior flexibilidade no uso e na administração de nossos _containers_. 

-   **-t** -- Disponibiliza um TTY (console) para o nosso _container_.
    
-   **-i** -- Mantém o STDIN aberto mesmo que você não esteja conectado no _container._
    
-   **-d** -- Faz com que o _container_ rode como um _daemon_, ou seja, sem a interatividade que os outros dois parâmetros nos fornecem.

```bash
docker run -it ubuntu bash
```

### Posso voltar ao _container_?
Sim! Após deixar o nosso container em execução, e querermos acessá-lo novamente, basta utilizar o seguinte comando:

Para que o nosso container recém-criado seja executado, basta utilizar o  "docker start [CONTAINER ID]" e em seguida "docker attach [CONTAINER ID"]

```bash
docker start [CONTAINER ID] // deixando o container em execução
docker attach [CONTAINER ID] // acessando novamente o container
```



### Rodando o nginx
- O que é nginx?
nginx nada mais é que um proxy reverso, que é bastante utilizado nos servidores para você disponibilizar a porta de acesso da sua aplicação,Onde vai bater uma porta do nginx, e ele vai fazer direcionamento para determinada pasta do seu projeto e onde tá rodando determinada porta. 

- Para passar a porta para o nginx
```bash
docker run -d -p 80:80 nginx
```

Para executar um comando dentro de um container que já está em execução, é necessário recorrer à ajuda do comando Docker exec. Apenas ele pode iniciar qualquer comando nessas condições.

```bash
docker exec -it [CONTAINER ID] bash
```



