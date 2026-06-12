> **Curso:** Engenharia de Software / Tecnologia em Análise e Desenvolvimento de Sistemas  
> **Disciplina:** Programação Front-End    
> **Tema:**  Debugando Código TypeScript com Visual Studio Code    
> **Professor:** José Carlos Flores  
---

# Atividade Prática

## Debugando Código TypeScript com Visual Studio Code

### 🎯 Objetivos de Aprendizagem

Ao final desta atividade, o aluno será capaz de:

* Configurar um ambiente de desenvolvimento TypeScript no VS Code
* Entender o fluxo de compilação TypeScript → JavaScript
* Configurar o debugger do VS Code
* Utilizar breakpoints, step over, step into, watch e call stack
* Identificar e corrigir erros lógicos no código

***

## 🧰 Pré-requisitos

* Noções básicas de lógica de programação
* Conhecimento introdutório de JavaScript
* Computador com acesso à internet

***

## 1️⃣ Preparação do Ambiente

### 1.1 Instalação do Node.js

O TypeScript depende do Node.js.

* Acesse: <https://nodejs.org>
* Instale a versão **LTS**
* Verifique a instalação no terminal:

```bash
node -v
npm -v
```

***

### 1.2 Instalação do Visual Studio Code

* Acesse: <https://code.visualstudio.com>
* Instale conforme seu sistema operacional

#### Extensões recomendadas:

* **TypeScript and JavaScript Language Features** (já vem instalada)
* **Debugger for JavaScript** (geralmente já integrada)

***

### 1.3 Instalação do TypeScript

No terminal:

```bash
npm install -g typescript
```

Verificação:

```bash
tsc -v
```

***

## 2️⃣ Criação do Projeto TypeScript

### 2.1 Estrutura do Projeto

Crie uma pasta para o projeto:

```bash
mkdir debug-typescript
cd debug-typescript
```

Inicialize o projeto:

```bash
npm init -y
```

Crie a estrutura:

```text
debug-typescript/
│
├── src/
│   └── app.ts
│
├── dist/
│
├── tsconfig.json
└── package.json
```

***

### 2.2 Configuração do TypeScript (`tsconfig.json`)

Crie o arquivo `tsconfig.json` com o conteúdo:

```json
{
  "compilerOptions": {
    "target": "ES6",
    "module": "commonjs",
    "outDir": "./dist",
    "rootDir": "./src",
    "sourceMap": true,
    "strict": true
  }
}
```

🔎 **Importante:**  
A opção `"sourceMap": true` é essencial para o debug funcionar corretamente.

***

## 3️⃣ Código para a Prática

### 3.1 Código com Erro Lógico (`src/app.ts`)

```typescript
function calcularMedia(notas: number[]): number {
    let soma = 0;

    for (let i = 0; i <= notas.length; i++) {
        soma += notas[i];
    }

    return soma / notas.length;
}

const notasAluno = [7, 8, 6, 9];
const media = calcularMedia(notasAluno);

console.log("Média do aluno:", media);
```

⚠️ **Observação:**  
O código compila, mas gera um erro lógico em tempo de execução.

***

### 3.2 Compilação do Código

No terminal:

```bash
tsc
```

Será gerado o arquivo:

```text
dist/app.js
dist/app.js.map
```

***

## 4️⃣ Configuração do Debug no VS Code

### 4.1 Arquivo `launch.json`

No VS Code:

* Clique em **Run and Debug**
* Clique em **create a launch.json**
* Escolha **Node.js**

Substitua o conteúdo por:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Debug TypeScript",
      "program": "${workspaceFolder}/dist/app.js",
      "preLaunchTask": "tsc",
      "outFiles": ["${workspaceFolder}/dist/**/*.js"]
    }
  ]
}
```

***


## 5️⃣ Processo de Debug (Passo a Passo)

### 5.1 Inserindo Breakpoints

* Clique à esquerda da linha dentro do `for`
* Adicione um breakpoint em:

```typescript
soma += notas[i];
```

***

### 5.2 Iniciando o Debug

* Pressione **F5**
* Observe a execução pausada no breakpoint

***

### 5.3 Ferramentas do Debugger

Durante a execução, explore:

* **Variables** → valores de `i`, `soma`, `notas`
* **Watch** → adicione `notas[i]`
* **Call Stack** → fluxo de chamadas
* **Step Over (F10)** → linha a linha
* **Step Into (F11)** → entra em funções

***

### 5.4 Identificação do Erro

Observe que:

* O laço usa `i <= notas.length`
* Na última iteração, `notas[i]` é `undefined`
* Isso gera comportamento inesperado no cálculo

***

## 6️⃣ Correção do Código

Código corrigido:

```typescript
function calcularMedia(notas: number[]): number {
    let soma = 0;

    for (let i = 0; i < notas.length; i++) {
        soma += notas[i];
    }

    return soma / notas.length;
}
```

Execute novamente o debug e observe o resultado correto.

***

## 7️⃣  Roteiro de Laboratório

***

## 🎯 Objetivo da Aula Prática

Capacitar o aluno a **utilizar o debugger do Visual Studio Code** para identificar e corrigir erros lógicos em aplicações TypeScript, compreendendo o fluxo de execução do código.

***

## 📌 Competências Desenvolvidas

* Configuração de ambiente TypeScript
* Uso de breakpoints
* Análise de variáveis em tempo de execução
* Identificação de erros lógicos
* Correção orientada por debug

***

## 🧰 Materiais Necessários

* Computador com acesso à internet
* Visual Studio Code
* Node.js (LTS)
* Terminal (PowerShell, Bash ou similar)

***

## ⏱️ Organização do Tempo (Sugestão)

| Etapa                    | Tempo  |
| ------------------------ | ------ |
| Configuração do ambiente | 25 min |
| Implementação do código  | 15 min |
| Configuração do debug    | 15 min |
| Debug guiado             | 25 min |
| Exercícios com debug     | 20 min |

***

## 🧪 Parte 1 – Configuração do Ambiente

### 1.1 Verificação das Ferramentas

No terminal, execute:

```bash
node -v
npm -v
tsc -v
```

📌 **Se algum comando falhar**, o aluno deve solicitar auxílio ao professor.

***

### 1.2 Criação do Projeto

```bash
mkdir lab-debug-typescript
cd lab-debug-typescript
npm init -y
```

Estrutura esperada:

```text
lab-debug-typescript/
├── src/
├── dist/
├── tsconfig.json
└── package.json
```

***

### 1.3 Configuração do TypeScript

Crie `tsconfig.json`:

```json
{
  "compilerOptions": {
    "target": "ES6",
    "module": "commonjs",
    "rootDir": "src",
    "outDir": "dist",
    "sourceMap": true,
    "strict": true
  }
}
```

📌 **Atenção do professor:** enfatizar a importância do `sourceMap`.

***

## 🧪 Parte 2 – Implementação do Código

### 2.1 Código Base com Erro (`src/app.ts`)

```typescript
function calcularMedia(notas: number[]): number {
    let soma = 0;

    for (let i = 0; i <= notas.length; i++) {
        soma += notas[i];
    }

    return soma / notas.length;
}

const notasAluno = [7, 8, 6, 9];
const media = calcularMedia(notasAluno);

console.log("Média do aluno:", media);
```

***

### 2.2 Compilação

```bash
tsc
node dist/app.js
```

📌 O resultado **não é o esperado**, mas o código compila sem erro.

***

## 🧪 Parte 3 – Configuração do Debug

### 3.1 Arquivo `launch.json` (Verifique se está dessa forma)

No VS Code:

* Run and Debug → Create launch.json → Node.js

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Debug TypeScript",
      "program": "${workspaceFolder}/dist/app.js",
      "preLaunchTask": "tsc",
      "outFiles": ["${workspaceFolder}/dist/**/*.js"]
    }
  ]
}
```

***

## 🧪 Parte 4 – Debug Guiado

### 4.1 Inserção de Breakpoint

Inserir breakpoint na linha:

```typescript
soma += notas[i];
```

***

### 4.2 Execução do Debug

* Pressione **F5**
* Observe:
  * Valor de `i`
  * Conteúdo de `notas[i]`
  * Variável `soma`

***

### 4.3 Análise Orientada

O aluno deve perceber que:

* O índice ultrapassa o tamanho do vetor
* `notas[i]` torna-se `undefined`
* O erro ocorre **em tempo de execução**

***

## 🧪 Parte 5 – Correção

Código corrigido:

```typescript
for (let i = 0; i < notas.length; i++) {
    soma += notas[i];
}
```

Executar novamente o debug.

***

# ✅ Lista de Exercícios – Debug em TypeScript

## Exercício 1 – Soma Incorreta

Analise o código abaixo usando o debugger:

```typescript
function somar(valores: number[]): number {
    let total = 1;

    for (let i = 0; i < valores.length; i++) {
        total += valores[i];
    }

    return total;
}

console.log(somar([2, 3, 4]));
```

🔎 **Tarefa:**

* Identificar o erro lógico
* Explicar por que o resultado está incorreto
* Corrigir usando debug

***

## Exercício 2 – Condicional com Erro

```typescript
function aprovado(media: number): boolean {
    if (media > 7) {
        return true;
    } else if (media > 5) {
        return true;
    } else {
        return false;
    }
}

console.log(aprovado(6));
```

🔎 **Tarefa:**

* Usar breakpoints para analisar o fluxo
* Corrigir a regra de negócio

***

## Exercício 3 – Laço Infinito

```typescript
let contador = 0;

while (contador < 5) {
    console.log(contador);
}
```

🔎 **Tarefa:**

* Executar em modo debug
* Identificar por que o laço não termina
* Corrigir o problema

***

## Exercício 4 – Função com Retorno Incorreto

```typescript
function buscarNome(nomes: string[], indice: number): string {
    nomes.forEach((n, i) => {
        if (i === indice) {
            return n;
        }
    });
    return "Não encontrado";
}

console.log(buscarNome(["Ana", "João", "Maria"], 1));
```

🔎 **Tarefa:**

* Usar Step Into e Call Stack
* Entender por que o retorno não funciona
* Propor uma solução

***

## 🧾 Forma de Entrega

* Capturas de tela do debug
* Código corrigido
* Respostas descritivas (1–2 parágrafos por exercício)

***

## 📊 Avaliação

* Execução correta do debug: 40%
* Identificação do erro: 30%
* Correção e explicação: 30%

---

## 👤 GitHub

[![Foto de Perfil](https://github.com/floresjcd.png?size=50)](https://github.com/floresjcd) 
**[@floresjcd](https://github.com/floresjcd)**