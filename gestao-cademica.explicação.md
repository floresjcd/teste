
---

## 🎓 Explicação Completa: Sistema de Gestão Acadêmica

### **O que é esta aplicação?**

É um **sistema web para gerenciar uma instituição acadêmica** - permite cadastrar cursos, alunos e vincular alunos aos cursos (matrículas). Tudo funciona no navegador, sem precisar de um banco de dados externo. Os dados são armazenados localmente no navegador.

---

### **Como a aplicação começa? (O Ponto de Entrada)**

Quando você abre a aplicação, o fluxo é assim:

```
1. Navegador carrega → main.ts (primeiro arquivo executado)
   ↓
2. main.ts inicia a aplicação → app.ts (componente raiz)
   ↓
3. app.ts carrega as rotas → app.routes.ts
   ↓
4. Você vê a tela de Login
```

```typescript name=src/main.ts url=https://github.com/floresjcd/gestao-academica/blob/ef3a7b3cdfc68066bf994c7aadbdbafd0258832f/src/main.ts
import { bootstrapApplication } from '@angular/platform-browser';
import { appConfig } from './app/app.config';
import { App } from './app/app';

bootstrapApplication(App, appConfig)  // ← Aqui começa tudo!
  .catch((err) => console.error(err));
```

**O que isso significa?** É como ligar o computador - você precisa de um ponto de partida. Este arquivo é esse ponto.

---

### **Como está estruturada a aplicação?**

#### **A Pasta do Projeto:**

```
gestao-academica/
├── src/
│   ├── app/
│   │   ├── pages/              ← Onde está a INTERFACE (o que vê na tela)
│   │   │   ├── login/          - Tela de entrada
│   │   │   ├── dashboard/      - Menu principal
│   │   │   ├── cursos/         - Gerenciar cursos
│   │   │   ├── alunos/         - Gerenciar alunos
│   │   │   └── matriculas/     - Vincular alunos aos cursos
│   │   ├── services/           ← Onde está a LÓGICA (operações nos dados)
│   │   │   ├── auth.service    - Controla login/logout
│   │   │   └── storage.service - Salva/recupera dados no navegador
│   │   ├── app.ts             ← Componente raiz
│   │   ├── app.routes.ts      ← Mapa das páginas
│   │   └── app.config.ts      ← Configurações
│   └── main.ts                ← Ponto de entrada
```

---

### **Entendendo a Arquitetura MVC**

O projeto segue o padrão **MVC (Model-View-Controller)**. Pense assim:

| Parte | O que é | Onde está |
|-------|---------|-----------|
| **Model** | Os dados e estruturas (tipos de dados) | `services/storage.service.ts` |
| **View** | O que você vê na tela (HTML/interface) | `pages/login/`, `pages/cursos/`, etc |
| **Controller** | A lógica que conecta View + Model | `services/auth.service.ts`, `services/storage.service.ts` |

**Exemplo prático:**
- **View:** Botão "Adicionar Curso" na tela
- **Controller:** Função `salvar()` que pega os dados do formulário
- **Model:** Dados do curso armazenados no `localStorage`

---

### **O Fluxo Completo da Aplicação**

#### **Passo 1: Você abre a aplicação**
```
Browser → localhost:4200
↓
Carrega main.ts → Executa bootstrapApplication(App, appConfig)
↓
Mostra a tela de Login (LOGIN COMPONENT)
```

#### **Passo 2: Você clica em "Entrar"**
```
Clica no botão → Chama entrar() do LoginComponent
↓
entrar() chama → this.authService.login()
↓
login() → Salva "session: active" no localStorage
↓
Redireciona para /dashboard → Mostra DASHBOARD
```

```typescript name=src/app/pages/login/login.component.ts url=https://github.com/floresjcd/gestao-academica/blob/ef3a7b3cdfc68066bf994c7aadbdbafd0258832f/src/app/pages/login/login.component.ts#L19-L23
export class LoginComponent {
  private authService = inject(AuthService);
  entrar() {
    this.authService.login();  // ← Vai para aqui
  }
}
```

#### **Passo 3: No Dashboard, você clica em "Cursos"**
```
Clica no link "Cursos" → Navega para /cursos
↓
Carrega CURSOS COMPONENT
↓
No constructor, chama this.atualizar()
↓
atualizar() → Pega os cursos do localStorage via StorageService
↓
Mostra a lista de cursos na tela
```

---

### **Entendendo os Conceitos-Chave do Angular**

#### **1. Componentes (Components)**
Um componente é um "bloco" reutilizável que combina:
- **Lógica TypeScript** (o comportamento)
- **Template HTML** (o visual)
- **Estilos CSS** (a aparência)

```typescript
@Component({
  selector: 'app-cursos',      // ← Nome para usar em HTML
  standalone: true,             // ← Componente independente (novo Angular)
  imports: [CommonModule, FormsModule, RouterModule],  // ← Funcionalidades que usa
  template: `...`,             // ← HTML da tela
  styleUrl: './cursos.css'     // ← Estilos
})
export class CursosComponent {
  // TypeScript aqui
}
```

#### **2. Serviços (Services)**
Um serviço é um "assistente" que executa tarefas comuns. Por exemplo:

- **AuthService:** Gerencia login/logout
- **StorageService:** Salva e recupera dados do navegador

```typescript name=src/app/services/auth.service.ts url=https://github.com/floresjcd/gestao-academica/blob/ef3a7b3cdfc68066bf994c7aadbdbafd0258832f/src/app/services/auth.service.ts#L1-L29
@Injectable({ providedIn: 'root' })  // ← Disponível em toda a app
export class AuthService {
  estaAutenticado(): boolean {
    return localStorage.getItem('session') === 'active';
  }
  
  login() {
    localStorage.setItem('session', 'active');
    this.router.navigate(['/dashboard']);
  }
  
  logout() {
    localStorage.removeItem('session');
    this.router.navigate(['/login']);
  }
}
```

#### **3. Rotas (Routes)**
Define quais componentes aparecem em cada URL:

```typescript name=src/app/app.routes.ts url=https://github.com/floresjcd/gestao-academica/blob/ef3a7b3cdfc68066bf994c7aadbdbafd0258832f/src/app/app.routes.ts
export const routes: Routes = [
  { path: 'login', component: LoginComponent },      // URL: /login
  { path: 'dashboard', component: DashboardComponent }, // URL: /dashboard
  { path: 'cursos', component: CursosComponent },    // URL: /cursos
  { path: 'alunos', component: AlunosComponent },    // URL: /alunos
  { path: 'matriculas', component: MatriculasComponent }, // URL: /matriculas
  { path: '', redirectTo: 'login', pathMatch: 'full' }   // URL raiz vai para /login
];
```

#### **4. Two-Way Binding (Ligação nos Dois Sentidos)**
Quando você digita em um input, o valor é atualizado na variável TypeScript automaticamente:

```html
<!-- No template do componente -->
<input [(ngModel)]="novo.nome" placeholder="Nome do Curso">
<!-- [(ngModel)] = quando digita aqui, atualiza novo.nome no TypeScript
                    quando novo.nome muda no TypeScript, atualiza aqui -->
```

---

### **Como Funciona o CRUD (Create, Read, Update, Delete)**

#### **Exemplo: Cadastro de Cursos**

**1. CREATE (Criar)**
```typescript
salvar() {
  if (!this.novo.nome || !this.novo.cargaHoraria) return;
  
  // Chama o serviço para salvar
  this.storage.save('cursos', this.novo);
  
  // Limpa o formulário
  this.cancelar();
  
  // Atualiza a lista na tela
  this.atualizar();
}
```

**2. READ (Ler)**
```typescript
atualizar() {
  // Recupera todos os cursos do localStorage
  this.lista = this.storage.getList('cursos');
}
```

**3. UPDATE (Atualizar)**
```typescript
editar(item: any) {
  // Copia o curso para edição
  this.novo = { ...item };
}
// Quando salva, o StorageService detecta o ID e atualiza no lugar de criar novo
```

**4. DELETE (Deletar)**
```typescript
excluir(id: number) {
  if (confirm("Deseja realmente excluir?")) {
    // Remove do localStorage
    this.storage.delete('cursos', id);
    // Recarrega a lista
    this.atualizar();
  }
}
```

---

### **Como os Dados são Armazenados**

A aplicação usa **localStorage do navegador** - é como um bloco de notas do seu navegador:

```javascript
// No StorageService:
getList(key: string): any[] {
  const data = localStorage.getItem(key);  // ← Recupera
  return data ? JSON.parse(data) : [];
}

save(key: string, item: any) {
  const list = this.getList(key);
  if (item.id) {
    // Editar existente
    const index = list.findIndex(i => i.id === item.id);
    if (index !== -1) list[index] = item;
  } else {
    // Criar novo
    item.id = Date.now();  // Gera ID único
    list.push(item);
  }
  localStorage.setItem(key, JSON.stringify(list));  // ← Salva
}
```

**Exemplo de dado armazenado:**
```json
localStorage.cursos = [
  { id: 1717923748392, nome: "Engenharia", cargaHoraria: 40 },
  { id: 1717923759401, nome: "Administração", cargaHoraria: 30 }
]

localStorage.alunos = [
  { id: 1717923764821, nome: "João Silva", email: "joao@email.com" }
]

localStorage.matriculas = [
  { id: 1717923769000, idAluno: 1717923764821, idCurso: 1717923748392, data: "08/06/2024" }
]
```

---

### **Fluxo Visual Completo**

```
┌─────────────────────────────────────────────────────────┐
│           NAVEGADOR - localhost:4200                    │
├─────────────────────────────────────────────────────────┤
│  ↓ main.ts executa bootstrapApplication(App, appConfig) │
│  ↓                                                        │
│  ↓ App carrega as rotas de app.routes.ts                │
│  ↓                                                        │
│  ↓ URL = /login → Mostra LoginComponent                 │
│    ┌────────────────────────────────────┐               │
│    │  Clique em "Entrar"               │               │
│    │  ↓                                  │               │
│    │  Chama authService.login()         │               │
│    │  ↓                                  │               │
│    │  Salva session no localStorage     │               │
│    │  ↓                                  │               │
│    │  Navega para /dashboard            │               │
│    └────────────────────────────────────┘               │
│  ↓                                                        │
│  URL = /dashboard → Mostra DashboardComponent           │
│    ┌────────────────────────────────────┐               │
│    │  Clique em "Cursos"               │               │
│    │  ↓                                  │               │
│    │  Navega para /cursos               │               │
│    └────────────────────────────────────┘               │
│  ↓                                                        │
│  URL = /cursos → Mostra CursosComponent                 │
│    ┌────────────────────────────────────┐               │
│    │  No constructor, chama atualizar() │               │
│    │  ↓                                  │               │
│    │  Carrega cursos do localStorage    │               │
│    │  ↓                                  │               │
│    │  Mostra tabela com cursos          │               │
│    │                                      │               │
│    │  Pode: Adicionar, Editar, Excluir  │               │
│    └────────────────────────────────────┘               │
└─────────────────────────────────────────────────────────┘
```

---

### **Resumo: Como Tudo se Conecta**

| Componente | Função | Exemplo |
|-----------|--------|---------|
| **main.ts** | Inicia a app | Carrega App e appConfig |
| **App** | Componente raiz | Exibe o conteúdo das rotas |
| **app.routes.ts** | Define URLs | /login, /dashboard, /cursos, etc |
| **LoginComponent** | Tela de login | Botão "Entrar" |
| **DashboardComponent** | Menu principal | Links para Cursos, Alunos, Matrículas |
| **CursosComponent** | CRUD de cursos | Formulário + tabela |
| **AlunosComponent** | CRUD de alunos | Formulário + tabela |
| **MatriculasComponent** | CRUD de matrículas | Vincula alunos aos cursos |
| **AuthService** | Gerencia login | estaAutenticado(), login(), logout() |
| **StorageService** | Acessa dados | getList(), save(), delete() |
| **localStorage** | Banco de dados | Armazena cursos, alunos, matrículas |

---

### **Para Rodar a Aplicação**

```bash
# 1. Instalar dependências
npm install

# 2. Iniciar servidor de desenvolvimento
ng serve

# 3. Abrir no navegador
# localhost:4200
```

