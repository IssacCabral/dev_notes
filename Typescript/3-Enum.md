- Em enum, as propriedades listadas seguem uma ordem numérica crescente.
Logo, Cima = 0, Baixo = 1, ... e por aí vai

- É possível alterar esse valor, atribuindo-o diretamente no elemento, como no enum de Valores.

- Também é possível usar operações matemáticas para atribuir valores aos elementos 

- Outra coisa que também podemos fazer, é tipar uma variável com um tipo enum

```ts
enum Direcoes{

    Cima, // Direcoes.Cima = 0

    Baixo, // Direcoes.Baixo = 1

    Esquerda, // Direcoes.Esquerda = 2

    Direita // Direcoes.Direita = 3

}

enum Valores{

    Dois = 2,

    Tres,

    Quatro,

    Sete = 7,

    Oito,

    Nove
}

enum Textos{

    Titulo = "TÍTULO",

    Descricao = "DESCRICAO",

    Um = 1,

    Dois,

    Tres
}

const maximo: number = 50

  
enum Valores2{

    Um = 1,

    Dois,

    Tres,

    Quatro,

    Cinco,

    Maximo = maximo

}

enum Valores3{

    Minimo = 10,

    Segundo = Minimo * 2,

    Terceiro

}

  

const temp: Valores3 = Valores3.Minimo
```