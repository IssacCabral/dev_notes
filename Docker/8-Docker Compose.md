# O que é?
O Docker Compose nada mais é do que uma forma de você conseguir escrever em um único arquivo todos os detalhes do ambiente de sua aplicação. Antes nós usávamos o _dockerfile_ apenas para criar imagens, seja da minha aplicação, do meu BD ou do meu _webserver_, mas sempre de forma unitária, pois tenho um _dockerfile_ para cada "tipo" de _container_: um para a minha _app_, outro para o meu BD e assim por diante.

Com o Docker Compose nós falamos sobre o ambiente inteiro. Por exemplo, no Docker Compose nós definimos quais os _services_ que desejamos criar e quais as características de cada _service_ (quantidade de _containers_ debaixo daquele _service_, volumes, _network_, _secrets_, etc.).

 


