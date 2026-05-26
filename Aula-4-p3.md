> **Curso:** Engenharia de Software / Tecnologia em Análise e Desenvolvimento de Sistemas  
> **Disciplina:** Análise e Projeto Orientado a Objetos    
> **Tema:**  Diagrama de Classes e POO    
> **Professor:** José Carlos Flores  
---
# Criando um Diagrama de Classes e Convertendo para Código Java

Uma estrutura organizada de projeto Java para o exemplo da biblioteca pode ficar assim:

```text
SistemaBiblioteca/
│
├── src/
│   ├── model/
│   │   ├── Autor.java
│   │   ├── Livro.java
│   │   └── Biblioteca.java
│   │
│   └── app/
│       └── Main.java
│
├── bin/
│
└── README.md
```

---

# 1. Explicação da estrutura

| Pasta       | Função                       |
| ----------- | ---------------------------- |
| `src`       | Código-fonte Java            |
| `model`     | Classes do sistema           |
| `app`       | Classe principal             |
| `bin`       | Arquivos compilados `.class` |
| `README.md` | Documentação do projeto      |

---

# 2. Criando o Projeto

## Passo 1 — Criar pasta principal

```text
SistemaBiblioteca
```

---

## Passo 2 — Criar subpastas

```text
src/model
src/app
bin
```

---

# 3. Classe Autor.java

Local:

```text
src/model/Autor.java
```

Código:

```java
package model;

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

# 4. Classe Livro.java

Local:

```text
src/model/Livro.java
```

Código:

```java
package model;

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

# 5. Classe Biblioteca.java

Local:

```text
src/model/Biblioteca.java
```

Código:

```java
package model;

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

# 6. Classe Main.java

Local:

```text
src/app/Main.java
```

Código:

```java
package app;

import model.Autor;
import model.Biblioteca;
import model.Livro;

public class Main {

    public static void main(String[] args) {

        Autor autor1 = new Autor(
            "Machado de Assis",
            "Brasileiro"
        );

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

        Biblioteca biblioteca = new Biblioteca(
            "Biblioteca Central"
        );

        biblioteca.adicionarLivro(livro1);
        biblioteca.adicionarLivro(livro2);

        biblioteca.listarLivros();
    }
}
```

---

# 7. Como Compilar

Entre na pasta do projeto:

```bash
cd SistemaBiblioteca
```

---

## Compilar tudo

Linux/Mac:

```bash
javac -d bin src/model/*.java src/app/*.java
```

Windows CMD:

```cmd
javac -d bin src\model\*.java src\app\*.java
```

---

# 8. Como Executar

Linux/Mac:

```bash
java -cp bin app.Main
```

Windows:

```cmd
java -cp bin app.Main
```

---

# 9. Estrutura Final Completa

```text
SistemaBiblioteca/
│
├── src/
│   ├── model/
│   │   ├── Autor.java
│   │   ├── Livro.java
│   │   └── Biblioteca.java
│   │
│   └── app/
│       └── Main.java
│
├── bin/
│   ├── model/
│   └── app/
│
└── README.md
```

---

## 👤 GitHub

[![Foto de Perfil](https://github.com/floresjcd.png?size=50)](https://github.com/floresjcd) 
**[@floresjcd](https://github.com/floresjcd)**
