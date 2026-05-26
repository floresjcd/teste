
> **Curso:** Engenharia de Software / Tecnologia em Análise e Desenvolvimento de Sistemas  
> **Disciplina:** Análise e Projeto Orientado a Objetos    
> **Tema:**  Diagrama de Classes e POO    
> **Professor:** José Carlos Flores  
---


# Criando um Diagrama de Classes e Convertendo para Código Java

## 1. Objetivo

Neste exemplo, vamos:

1. Criar um problema real simples
2. Modelar o sistema usando UML
3. Criar o diagrama de classes
4. Identificar atributos, métodos e relacionamentos
5. Converter o diagrama para código Java
6. Explicar cada parte do código

---

# 2. Cenário do Sistema

Vamos criar um sistema simples de biblioteca.

O sistema possui:

* Uma classe `Livro`
* Uma classe `Autor`
* Uma classe `Biblioteca`

Regras:

* Um autor pode escrever vários livros
* Uma biblioteca possui vários livros
* Cada livro possui título, ano e autor

---

# 3. Entendendo UML (Unified Modeling Language)

Um diagrama de classes representa:

| Elemento       | Significado                        |
| -------------- | ---------------------------------- |
| Classe         | Estrutura do objeto                |
| Atributo       | Característica da classe           |
| Método         | Comportamento da classe            |
| Associação     | Relacionamento entre classes       |
| Herança        | Especialização de classe           |
| Multiplicidade | Quantidade de objetos relacionados |

---

# 4. Diagrama de Classes UML

```text
+------------------------+
|         Autor          |
+------------------------+
| - nome:String          |
| - nacionalidade:String |
+------------------------+
| + exibirDados():void   |
+------------------------+
            |
            | 1
            |
            | escreve
            |
            | *
+------------------------+
|         Livro          |
+------------------------+
| - titulo:String        |
| - ano:int              |
+------------------------+
| + exibirLivro():void   |
+------------------------+


+------------------------+
|     Biblioteca         |
+------------------------+
| - nome:String          |
| - livros:List<Livro>   |
+------------------------+
| + adicionarLivro()     |
| + listarLivros()       |
+------------------------+

```

---

# 5. Interpretando o Diagrama

## Classe Autor

Possui:

### Atributos

* nome
* nacionalidade

### Método

* exibirDados()

---

## Classe Livro

Possui:

### Atributos

* titulo
* ano

### Método

* exibirLivro()

### Relacionamento

Um livro possui um autor.

---

## Classe Biblioteca

Possui:

### Atributos

* nome
* lista de livros

### Métodos

* adicionarLivro()
* listarLivros()

---

# 6. Conversão UML → Java

Agora vamos transformar cada classe do diagrama em código Java.

---

# 7. Classe Autor

## Passo 1 — Criar a classe

```java
public class Autor {

}
```

---

## Passo 2 — Adicionar atributos

```java
private String nome;
private String nacionalidade;
```

* `private` protege os dados
* `String` representa texto

---

## Passo 3 — Criar construtor

```java
public Autor(String nome, String nacionalidade) {
    this.nome = nome;
    this.nacionalidade = nacionalidade;
}
```

O construtor inicializa o objeto.

---

## Passo 4 — Criar método

```java
public void exibirDados() {
    System.out.println("Autor: " + nome);
    System.out.println("Nacionalidade: " + nacionalidade);
}
```

---

## Código completo da classe Autor

```java
public class Autor {

    private String nome;
    private String nacionalidade;

    public Autor(String nome, String nacionalidade) {
        this.nome = nome;
        this.nacionalidade = nacionalidade;
    }

    public void exibirDados() {
        System.out.println("Autor: " + nome);
        System.out.println("Nacionalidade: " + nacionalidade);
    }
}
```

---

# 8. Classe Livro

## Passo 1 — Criar atributos

```java
private String titulo;
private int ano;
private Autor autor;
```

Observe:

```java
private Autor autor;
```

Isso representa o relacionamento entre Livro e Autor.

---

## Passo 2 — Criar construtor

```java
public Livro(String titulo, int ano, Autor autor) {
    this.titulo = titulo;
    this.ano = ano;
    this.autor = autor;
}
```

---

## Passo 3 — Criar método

```java
public void exibirLivro() {
    System.out.println("Título: " + titulo);
    System.out.println("Ano: " + ano);
    autor.exibirDados();
}
```

---

## Código completo da classe Livro

```java
public class Livro {

    private String titulo;
    private int ano;
    private Autor autor;

    public Livro(String titulo, int ano, Autor autor) {
        this.titulo = titulo;
        this.ano = ano;
        this.autor = autor;
    }

    public void exibirLivro() {
        System.out.println("Título: " + titulo);
        System.out.println("Ano: " + ano);
        autor.exibirDados();
    }
}
```

---

# 9. Classe Biblioteca

Agora teremos uma coleção de livros.

Para isso usamos:

```java
List<Livro>
```

---

## Passo 1 — Importar biblioteca

```java
import java.util.ArrayList;
import java.util.List;
```

---

## Passo 2 — Criar atributos

```java
private String nome;
private List<Livro> livros;
```

---

## Passo 3 — Inicializar lista

```java
this.livros = new ArrayList<>();
```

---

## Passo 4 — Adicionar métodos

### Adicionar livro

```java
public void adicionarLivro(Livro livro) {
    livros.add(livro);
}
```

### Listar livros

```java
public void listarLivros() {
    for (Livro livro : livros) {
        livro.exibirLivro();
        System.out.println("----------------");
    }
}
```

---

## Código completo da classe Biblioteca

```java
import java.util.ArrayList;
import java.util.List;

public class Biblioteca {

    private String nome;
    private List<Livro> livros;

    public Biblioteca(String nome) {
        this.nome = nome;
        this.livros = new ArrayList<>();
    }

    public void adicionarLivro(Livro livro) {
        livros.add(livro);
    }

    public void listarLivros() {
        for (Livro livro : livros) {
            livro.exibirLivro();
            System.out.println("----------------");
        }
    }
}
```

---

# 10. Classe Principal (Main)

Agora vamos usar todas as classes.

```java
public class Main {

    public static void main(String[] args) {

        Autor autor1 = new Autor("Machado de Assis", "Brasileiro");

        Livro livro1 = new Livro(
            "Dom Casmurro",
            1899,
            autor1
        );

        Livro livro2 = new Livro(
            "Memórias Póstumas",
            1881,
            autor1
        );

        Biblioteca biblioteca = new Biblioteca("Biblioteca Central");

        biblioteca.adicionarLivro(livro1);
        biblioteca.adicionarLivro(livro2);

        biblioteca.listarLivros();
    }
}
```

---

# 11. Resultado Esperado

```text
Título: Dom Casmurro
Ano: 1899
Autor: Machado de Assis
Nacionalidade: Brasileiro
----------------
Título: Memórias Póstumas
Ano: 1881
Autor: Machado de Assis
Nacionalidade: Brasileiro
----------------
```

---

# 12. Mapeamento UML → Java

| UML                      | Java                    |
| ------------------------ | ----------------------- |
| Classe                   | class                   |
| Atributo                 | variável                |
| Método                   | Método                  |
| Associação               | objeto dentro da classe |
| Multiplicidade *         | List<>                  |
| Visibilidade privada (-) | private                 |
| Visibilidade pública (+) | public                  |

---

# 13. Tipos de Relacionamento UML

## Associação

Uma classe usa outra.

Exemplo:

```java
private Autor autor;
```

---

## Agregação

Uma classe possui outra, mas ambas podem existir separadamente.

Exemplo:

```java
private List<Livro> livros;
```

---

## Herança

Exemplo:

```java
public class Pessoa {
}

public class Aluno extends Pessoa {
}
```

---

## Interface

Exemplo:

```java
public interface Imprimivel {
    void imprimir();
}
```

```java
public class Relatorio implements Imprimivel {

    @Override
    public void imprimir() {
        System.out.println("Imprimindo...");
    }
}
```

---

# 14. Passo a Passo Geral para Converter UML em Java

## Passo 1

Identifique as classes.

---

## Passo 2

Identifique atributos.

---

## Passo 3

Identifique métodos.

---

## Passo 4

Analise relacionamentos.

---

## Passo 5

Defina:

* private
* public
* protected

---

## Passo 6

Implemente construtores.

---

## Passo 7

Implemente listas e relacionamentos.

---

## Passo 8

Crie a classe Main para testar.

---

# 15. Conclusão

Converter um diagrama UML para Java consiste em:

1. Transformar cada classe UML em uma classe Java
2. Transformar atributos UML em variáveis
3. Transformar operações UML em métodos
4. Representar relacionamentos usando objetos e coleções
5. Implementar o comportamento no código

A UML funciona como um projeto arquitetônico do software, enquanto o Java é a implementação prática desse projeto.

---

## 👤 GitHub

[![Foto de Perfil](https://github.com/floresjcd.png?size=50)](https://github.com/floresjcd) 
**[@floresjcd](https://github.com/floresjcd)**