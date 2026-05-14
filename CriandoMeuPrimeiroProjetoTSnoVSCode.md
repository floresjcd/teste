
> **Curso:** Engenharia de Software / Tecnologia em Análise e Desenvolvimento de Sistemas  
> **Disciplina:** Programação Front-End    
> **Tema:**  Configuração e Desenvolvimento de Projetos TypeScript no Visual Studio Code    
> **Professor:** José Carlos Flores  
---


## 1. Introdução ao TypeScript no Contexto do desenvolvimento de software

A evolução do desenvolvimento web trouxe consigo a necessidade de ferramentas mais robustas para a construção de aplicações de grande escala. O JavaScript, embora seja a linguagem universal da web, possui tipagem dinâmica, o que pode ocasionar erros em tempo de execução difíceis de rastrear em projetos complexos. Nesse cenário, surge o TypeScript, um superconjunto (superset) tipado do JavaScript desenvolvido pela Microsoft.

O TypeScript adiciona tipagem estática opcional ao JavaScript, permitindo que os desenvolvedores identifiquem erros durante a fase de desenvolvimento (tempo de compilação) em vez de descobri-los apenas quando o código está em execução. Essa característica é fundamental para a Engenharia de Software, pois promove a manutenibilidade, a legibilidade e a escalabilidade do código-fonte. Além disso, o TypeScript oferece suporte a recursos modernos de orientação a objetos, como classes, interfaces e módulos, facilitando a estruturação de componentes robustos.

Nesta aula, exploraremos detalhadamente como configurar um ambiente de desenvolvimento profissional utilizando o Visual Studio Code (VS Code), um dos editores de código mais populares e poderosos da atualidade, que possui suporte nativo excepcional para TypeScript.

---

## 2. Pré-requisitos e Preparação do Ambiente

Antes de iniciarmos a codificação, é imprescindível preparar o ambiente de desenvolvimento. O TypeScript não é executado diretamente pelos navegadores ou pelo Node.js; ele precisa ser transpilado (convertido) para JavaScript puro. Para realizar esse processo, utilizaremos o compilador oficial do TypeScript.

### 2.1. Instalação do Node.js e NPM

O Node.js é um ambiente de execução JavaScript server-side, e o NPM (Node Package Manager) é o seu gerenciador de pacotes padrão. O compilador do TypeScript é distribuído como um pacote NPM.

1. Acesse o site oficial do Node.js (https://nodejs.org) e faça o download da versão LTS (Long Term Support).
2. Execute o instalador e siga as instruções padrão.
3. Reinicie o Computador após a instalação.
4. Para verificar se a instalação foi bem-sucedida, abra o terminal (ou prompt de comando) e execute os seguintes comandos:

```bash
node -v
npm -v
```

Esses comandos devem retornar as versões instaladas do Node.js e do NPM, respectivamente.

### 2.2. Instalação do Visual Studio Code

O Visual Studio Code é um editor de código-fonte leve, porém poderoso, que roda no seu desktop. Ele vem com suporte embutido para JavaScript, TypeScript e Node.js.

1. Acesse o site oficial do VS Code (https://code.visualstudio.com) e faça o download da versão correspondente ao seu sistema operacional.
2. Realize a instalação seguindo os passos recomendados.

---

## 3. Criando o Projeto TypeScript

Vamos criar nosso primeiro projeto. A organização do diretório de trabalho é uma prática essencial.

### 3.1. Estruturação do Diretório

Abra o **Prompt de Comando** e execute os comandos abaixo um por um:


```bash
# 1. Criar a pasta do projeto
mkdir MeuProjetoTS
cd MeuProjetoTS

# 2. Criar a estrutura de pastas
mkdir src
mkdir dist

2. Abra esta pasta no Visual Studio Code. No terminal, você pode utilizar o comando:

```bash
code .
```

## 4. Instalar o TypeScript e configurações

Ainda dentro da pasta `MeuProjetoTS`, no terminal execute:

```powershell
# Instala TypeScript globalmente (para usar tsc)
npm install -g typescript

# Este comando exibirá a versão do compilador TypeScript instalada em sua máquina.
tsc --version

# Instala TypeScript como dependência do projeto
npm install --save-dev typescript @types/node

# Instala ts-node (para executar .ts direto sem compilar)
npm install --save-dev ts-node
```

---

## 5. Criar o tsconfig.json

A compilação manual de arquivos individuais torna-se inviável à medida que o projeto cresce. Para gerenciar projetos complexos, o TypeScript utiliza um arquivo de configuração chamado `tsconfig.json`. Este arquivo define as opções do compilador e os arquivos que devem ser incluídos no processo de compilação.

### 5.1. Inicializando o Arquivo de Configuração

Para criar o arquivo `tsconfig.json` com as configurações padrão, execute o seguinte comando no terminal, na raiz do seu projeto:

```bash
tsc --init
```

Um arquivo `tsconfig.json` será gerado. Ao abri-lo, você verá diversas opções comentadas. Vamos focar nas configurações mais importantes para a estruturação de um projeto front-end moderno.

### 5.2. Opções Essenciais do Compilador

Ajuste o seu `tsconfig.json` para refletir as seguintes configurações:

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "Node16",
    "moduleResolution": "Node16",
    "rootDir": "./src",
    "outDir": "./dist",
    "types": ["node"],
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "sourceMap": true
  },
  "include": ["src/**/*.ts"],
  "exclude": ["node_modules", "dist"]
}
```

Agora, para compilar todo o projeto, basta executar o comando `tsc` sem especificar nenhum arquivo:

```bash
tsc
```

O compilador lerá o `tsconfig.json`, buscará os arquivos na pasta `src` e gerará os arquivos JavaScript correspondentes na pasta `dist`.

---


## 6. Escrevendo o Primeiro Código

No VS Code, crie um novo arquivo chamado `index.ts`. A extensão `.ts` indica que se trata de um arquivo TypeScript. Insira o seguinte código:

```typescript
let saudacao: string = "Olá, acadêmicos de Engenharia de Software e ADS!";
console.log(saudacao);
```

Observe a sintaxe `let saudacao: string`. Esta é a anotação de tipo do TypeScript, que define explicitamente que a variável `saudacao` só pode armazenar valores do tipo texto (string).

### 6.1. Compilação

Como mencionado anteriormente, o TypeScript precisa ser transpilado para JavaScript. Para compilar o arquivo que acabamos de criar, abra o terminal integrado do VS Code (atalho: `` Ctrl + ` ``) e execute:

```bash
tsc 
```

Após a execução deste comando, você notará que um novo arquivo chamado `index.js` foi gerado no diretório src. Este é o código JavaScript resultante, que pode ser executado pelo Node.js:

```bash
node index.js
```

O terminal exibirá a mensagem: `Olá, acadêmicos de Engenharia de Software e ADS!`.


**Ou executar direto sem compilar (mais prático para treino):**

```powershell
npx ts-node src/index.ts
```
---

## 7. Automação e Depuração (Debugging) no VS Code

Para otimizar o fluxo de trabalho, podemos automatizar a compilação e configurar o VS Code para depurar nosso código TypeScript diretamente.

### 7.1. Modo de Observação (Watch Mode)

Durante o desenvolvimento, é produtivo que o código seja compilado automaticamente a cada salvamento. Para ativar o modo de observação, utilize a flag `-w` ou `--watch`:

```bash
tsc --watch
```

O terminal ficará bloqueado, observando as alterações nos arquivos `.ts` e recompilando-os instantaneamente.

### 7.2. Configurando o Debugger

O VS Code possui suporte nativo para depuração de TypeScript, desde que os `source maps` estejam habilitados no `tsconfig.json` (como fizemos no passo 5.2) [1].

1. No VS Code, acesse a aba "Run and Debug" (Executar e Depurar) na barra lateral esquerda (atalho: `Ctrl + Shift + D`).
2. Clique em "create a launch.json file" (criar um arquivo launch.json) e selecione "Node.js".
3. O VS Code criará uma pasta `.vscode` com o arquivo `launch.json`. Modifique-o para a seguinte configuração:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Executar Programa TypeScript",
      "skipFiles": [
        "<node_internals>/**"
      ],
      "program": "${workspaceFolder}/src/index.ts",
      "preLaunchTask": "tsc: build - tsconfig.json",
      "outFiles": [
        "${workspaceFolder}/dist/**/*.js"
      ]
    }
  ]
}
```

Esta configuração instrui o VS Code a compilar o projeto antes de iniciar a depuração (`preLaunchTask`) e mapeia os arquivos de saída corretamente.

Para testar, adicione um *breakpoint* (ponto de interrupção) clicando à esquerda do número da linha no seu arquivo `index.ts`. Em seguida, pressione `F5` para iniciar a depuração. A execução será pausada no breakpoint, permitindo a inspeção de variáveis e o controle do fluxo de execução.

---

## 8. Conclusão

A adoção do TypeScript em projetos de desenvolvimento de software representa um avanço significativo na garantia de qualidade e na prevenção de erros. A configuração adequada do ambiente no Visual Studio Code, compreendendo o papel do compilador, a estruturação de diretórios e a utilização do `tsconfig.json`, é o alicerce para o desenvolvimento de aplicações front-end escaláveis e de fácil manutenção.

Incentivo todos os acadêmicos a explorarem os recursos avançados do TypeScript e a integrarem essas práticas em seus projetos acadêmicos e profissionais.

## **Resumo da estrutura final da pasta do projeto**

```
MeuProjetoTS/
├── src/                  ← Seus arquivos .ts
│   └── index.ts
├── dist/                 ← Arquivos .js compilados
├── node_modules/
├── package.json
├── tsconfig.json
└── package-lock.json
```

---  



## Referências

[1] Visual Studio Code. "TypeScript tutorial in Visual Studio Code". Disponível em: https://code.visualstudio.com/docs/typescript/typescript-tutorial. Acesso em: 22 abr. 2026.


---

## 👤 GitHub

[![Foto de Perfil](https://github.com/floresjcd.png?size=50)](https://github.com/floresjcd) 
**[@floresjcd](https://github.com/floresjcd)**
