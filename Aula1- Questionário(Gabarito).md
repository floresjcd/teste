> **Curso:** Engenharia de Software  
> **Disciplina:** Análise e Projeto Orientado a Objetos    
> **Professor:** José Carlos Flores  
> **Assunto:** Gabarito Questionário Aula-1  

---

1. **O que define uma linguagem de programação em termos de sua estrutura e finalidade?**
   Uma linguagem de programação é uma forma estruturada de comunicar instruções a um computador, permitindo que o programador descreva tarefas a serem executadas pela máquina.

2. **Explique a diferença entre um programa e uma linguagem de programação.**
   Uma linguagem de programação é a ferramenta/sistema de comunicação, enquanto um programa representa uma sequência específica de instruções ou ordens escritas nessa linguagem para resolver um problema ou desempenhar uma função.

3. **Como são classificadas as linguagens de programação quanto ao seu nível de abstração?**
   São classificadas em linguagens de Alto Nível (mais próximas da linguagem humana) e linguagens de Baixo Nível (mais próximas do hardware).

4. **Quais são as principais características das linguagens de alto nível?**
   São linguagens mais intuitivas, fáceis de ler e escrever, como Python, Java, JavaScript e Ruby. Elas abstraem a complexidade do hardware.

5. **Cite duas vantagens e duas desvantagens das linguagens de alto nível.**
   Vantagens: Facilidade de aprendizado e alta produtividade; manutenção simplificada. Desvantagens: Exigem maior tempo de processamento e ocupam mais memória em comparação com as de baixo nível.

6. **O que caracteriza uma linguagem de baixo nível e qual sua proximidade com o hardware?**
   São linguagens que operam muito próximas da arquitetura física do computador (C, Assembly), exigindo conhecimento profundo do hardware.

7. **Quais são as vantagens de se utilizar uma linguagem de baixo nível, como C ou Assembly?**
   O tempo de processamento é mais rápido e a arquitetura do dispositivo é melhor aproveitada, resultando em maior eficiência.

8. **Por que o tempo de aprendizado de linguagens de baixo nível costuma ser maior?**
   Devido à complexidade da sintaxe e à necessidade de compreender detalhadamente o funcionamento interno da máquina e seu hardware.

9. **Defina o conceito de "Sintaxe" no contexto da programação.**
   Sintaxe refere-se ao conjunto de regras que determinam como o código deve ser estruturado corretamente para ser compreendido pelo computador.

10. **O que é a "Semântica" de um código e como ela se diferencia da sintaxe?**
    A semântica é o significado do código escrito. Enquanto a sintaxe foca na "forma" (escrita correta), a semântica foca no "conteúdo" (o que o comando realmente faz).

11. **O que é um paradigma de programação e qual sua importância para a solução de problemas?**
    Um paradigma é um estilo, modelo ou metodologia de programação. Ele define as regras e a forma como os problemas serão solucionados usando determinado código.

12. **Descreva o funcionamento do Paradigma Imperativo (ou Procedural).**
    Baseia-se na execução sequencial de instruções passadas ao computador, onde o programador descreve um passo a passo detalhado do que deve ser cumprido.

13. **No Paradigma Orientado a Objetos, qual é a menor entidade básica e como as operações são realizadas?**
    A menor entidade básica é o objeto, e todo tipo de operação é realizado diretamente sobre esses objetos.

14. **Qual a principal vantagem da Orientação a Objetos em relação à portabilidade entre sistemas operacionais?**
    Permite que softwares sejam desenvolvidos uma única vez e interpretados por diferentes plataformas sem obstáculos, pois o programa é estruturado como uma coleção de classes e objetos.

15. **Explique a diferença fundamental entre os paradigmas imperativos e os declarativos.**
    O paradigma imperativo foca no "como" fazer (passo a passo), enquanto o declarativo foca no "o quê" se deseja obter, sem detalhar o processo para chegar ao resultado.

16. **O que caracteriza o Paradigma Funcional e em que tipo de problemas ele é mais indicado?**
    Destaca o uso de funções e cálculos matemáticos, dividindo o problema em blocos. É altamente indicado para problemas que envolvem matemática direta.

17. **Como funciona o Paradigma Lógico e qual sua principal aplicação prática mencionada?**
    Baseia-se em fatos e cláusulas verdadeiras para realizar inferências e produzir resultados. É muito popular na área de Inteligência Artificial.

18. **O que é uma variável e o que ela representa fisicamente no computador?**
    Uma variável corresponde a uma posição física na memória do computador, onde dados podem ser armazenados e acessados.

19. **Quais elementos compõem a declaração de uma variável em Java?**
    Uma declaração define o tipo da variável, seu identificador (nome) e pode incluir outros atributos.

20. **Diferencie a "declaração" da "inicialização" de uma variável.**
    Declarar é apenas definir o tipo e o nome da variável (`int x;`). Inicializar é atribuir um valor inicial a ela no momento da criação (`int x = 10;`).

21. **Explique o conceito de Tipagem Estática e cite um exemplo de linguagem que a utiliza.**
    Em linguagens de tipagem estática, o tipo de uma variável não pode ser alterado após ser declarado. Exemplos: Java e C++.

22. **O que permite a Tipagem Dinâmica ao programador e em que momento o tipo é definido?**
    Permite alterar o tipo de uma variável anteriormente declarada ou definir o tipo apenas em tempo de execução. Exemplos: Python e JavaScript.

23. **Qual a diferença entre Tipagem Forte e Tipagem Fraca?**
    Tipagem forte não permite conversões implícitas entre tipos diferentes (ex: somar número com texto causa erro). Tipagem fraca permite essas conversões automaticamente.

24. **O que ocorre quando tentamos somar um inteiro e uma string em uma linguagem de tipagem forte como Python?**
    Ocorrerá um erro, pois a linguagem não permite a operação entre tipos incompatíveis sem uma conversão explícita.

25. **Como funciona o processo de execução em uma linguagem compilada?**
    O código-fonte é convertido integralmente por um compilador em código de máquina, que o processador executa diretamente.

26. **Por que linguagens compiladas tendem a ser mais rápidas que as interpretadas?**
    Porque o código já está em formato nativo de máquina, sendo mais eficiente para o processador, sem a necessidade de tradução durante a execução.

27. **Descreva o funcionamento de um interpretador em linguagens interpretadas.**
    O interpretador lê e executa o programa linha por linha, processando cada comando sequencialmente em tempo de execução.

28. **Cite três exemplos de linguagens interpretadas mencionadas no material.**
    PHP, Ruby, Python e JavaScript.

29. **O que são Linguagens Híbridas e como elas combinam os conceitos de compilação e interpretação?**
    Representam um meio-termo: o código de alto nível é primeiro compilado para uma linguagem intermediária e, posteriormente, essa linguagem é interpretada por uma máquina virtual.

30. **No contexto de linguagens híbridas (como Java), o que é a "linguagem intermediária" e qual sua função?**
    É um código projetado para facilitar a interpretação em diferentes plataformas (como o bytecode em Java), garantindo portabilidade e eficiência no processo final de execução.
