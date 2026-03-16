# Apostila de Programação Front-End: Design Responsivo, Media Queries e Unidades de Medida

**Disciplina:** Programação Front-End  
**Professor:** José Carlos Flores  
**Curso:** Engenharia de Software  
**Carga Horária Estimada:** 360 minutos (6 horas)

---

## Índice

1. [Introdução ao Design Responsivo](#1-introdução-ao-design-responsivo)
2. [Unidades de Medida CSS](#2-unidades-de-medida-css)
3. [Media Queries: Sintaxe e Aplicação](#3-media-queries-sintaxe-e-aplicação)
4. [Breakpoints e Estratégias de Layout](#4-breakpoints-e-estratégias-de-layout)
5. [Exemplos Práticos Detalhados](#5-exemplos-práticos-detalhados)
6. [Boas Práticas e Armadilhas Comuns](#6-boas-práticas-e-armadilhas-comuns)

---

## 1. Introdução ao Design Responsivo

### 1.1 Contexto Histórico e Importância

Até o ano de 2010, o desenvolvimento web era predominantemente focado em desktops. Os desenvolvedores criavam sites com larguras fixas (frequentemente 960 pixels) e simplesmente ignoravam dispositivos móveis. Essa abordagem tornou-se insustentável com a explosão do mercado de smartphones. O termo **Design Responsivo** foi cunhado por **Ethan Marcotte** em um artigo seminal publicado em maio de 2010, no qual ele propôs uma abordagem fundamentalmente diferente: em vez de criar versões separadas de um site para cada dispositivo, por que não criar um único site que se **adapta** automaticamente?

A filosofia por trás do Design Responsivo é elegantemente simples: a web deve ser fluida, flexível e acessível a todos, independentemente do dispositivo utilizado. Essa mudança de paradigma não foi apenas uma melhoria técnica; representou uma transformação na forma como pensamos sobre a experiência do usuário.

### 1.2 Os Três Pilares do Design Responsivo

Marcotte estabeleceu que o Design Responsivo repousa sobre três pilares técnicos fundamentais:

#### 1.2.1 Grilles Fluídas (Fluid Grids)
Em vez de definir larguras fixas em pixels, utilizamos **porcentagens** e unidades relativas. Isso permite que os elementos se redimensionem proporcionalmente conforme a largura da tela muda. Por exemplo, uma coluna que ocupa 50% da largura do seu container sempre ocupará exatamente metade do espaço disponível, independentemente de esse container ter 320 pixels (mobile) ou 1920 pixels (desktop).

#### 1.2.2 Imagens Flexíveis (Flexible Images)
As imagens devem se redimensionar dentro de seus elementos pai sem transbordar. Historicamente, uma imagem de 800 pixels de largura quebraria o layout em uma tela de 480 pixels. A solução é simples: `max-width: 100%` garante que a imagem nunca ultrapasse a largura do seu container.

#### 1.2.3 Media Queries
Finalmente, precisamos de um mecanismo para aplicar regras de CSS diferentes conforme as características do dispositivo mudam. As **Media Queries** permitem exatamente isso: elas testam condições (como largura da viewport) e aplicam estilos CSS apenas quando essas condições são verdadeiras.

### 1.3 Por Que a Responsividade é Crítica

Consideremos alguns dados práticos:

* **Fragmentação de Dispositivos:** Não existem apenas iPhones e Androids. Existem smartwatches (280 pixels), tablets (768 pixels), laptops (1366 pixels) e monitores 4K (3840 pixels). É impossível criar uma versão específica para cada um.

* **Impacto no SEO:** Desde 2015, o Google prioriza sites responsivos em seus resultados de busca. Um site que não se adapta a dispositivos móveis será penalizado no ranking.

* **Experiência do Usuário:** Um site que força o usuário a fazer zoom ou scroll horizontal em um smartphone é frustrante e resulta em altas taxas de rejeição.

* **Custo de Manutenção:** Manter múltiplas versões de um site (desktop, tablet, mobile) multiplica os custos de desenvolvimento e manutenção.

---

## 2. Unidades de Medida CSS

O domínio das unidades de medida é fundamental para criar layouts verdadeiramente responsivos. Não é suficiente saber que `width: 50%` existe; é necessário entender *quando* utilizá-la, *por quê* e *quais são as implicações*.

### 2.1 Unidades Absolutas

As unidades absolutas possuem um tamanho fixo e não mudam conforme o contexto. Elas são úteis em cenários muito específicos, mas devem ser evitadas na maioria dos casos em design responsivo.

#### 2.1.1 Pixels (px)
O pixel é a unidade mais comum e intuitiva. Um `width: 100px` significa "exatamente 100 pixels de largura". No entanto, é importante notar que em telas de alta densidade (como a Retina do iPhone), um "pixel CSS" pode corresponder a múltiplos "pixels físicos". Isso é transparente para o desenvolvedor, mas explica por que a mesma largura em pixels pode parecer diferente em dispositivos diferentes.

**Quando usar pixels:**
* Bordas muito finas (1px, 2px)
* Ícones de tamanho fixo
* Elementos que devem ter um tamanho absoluto (como um logo)

**Quando evitar pixels:**
* Larguras de containers principais
* Tamanhos de fonte (prejudica acessibilidade)
* Padding e margin de elementos responsivos

```css
/* ✓ Bom: Ícone com tamanho fixo */
.icon { width: 24px; height: 24px; }

/* ✗ Ruim: Fonte com tamanho fixo */
body { font-size: 12px; } /* Não respeita preferências de acessibilidade */
```

### 2.2 Unidades Relativas

As unidades relativas são a base do design responsivo. Seu tamanho depende de outro valor de referência, o que as torna flexíveis e adaptáveis.

#### 2.2.1 Porcentagem (%)
A porcentagem é relativa ao tamanho do elemento pai imediato. Se um container tem 800 pixels de largura e um elemento filho tem `width: 50%`, esse elemento terá 400 pixels.

**Características:**
* Sempre relativa ao elemento pai
* Ideal para layouts fluídos
* Funciona bem com flexbox e grid

```css
.container { width: 100%; max-width: 1200px; margin: 0 auto; }
.column { width: 50%; float: left; } /* Ocupa metade do container */
```

**Exemplo Prático:**
```html
<div class="container" style="width: 800px;">
  <div class="column" style="width: 50%;">
    <!-- Este div terá 400px de largura -->
  </div>
</div>
```

#### 2.2.2 Em (Relative to Element)
A unidade `em` é relativa ao tamanho da fonte do elemento ou de seu pai. Se um elemento tem `font-size: 16px` e você define `padding: 1em`, o padding será 16 pixels.

**Características:**
* Relativa à fonte do próprio elemento ou do pai
* Herança cascata: em elementos aninhados, `em` se multiplica
* Excelente para espaçamentos proporcionais

```css
.button {
  font-size: 16px;
  padding: 0.5em 1em; /* 8px 16px */
}

.button.large {
  font-size: 20px;
  padding: 0.5em 1em; /* 10px 20px - escala automaticamente! */
}
```

**Armadilha Comum - Herança em Cascata:**
```css
.container { font-size: 16px; }
.container .child { font-size: 1.5em; } /* 24px */
.container .child .grandchild { font-size: 1.5em; } /* 36px - multiplicou! */
```

#### 2.2.3 Rem (Relative to Root Element)
A unidade `rem` é relativa ao tamanho da fonte do elemento raiz (`<html>`). Diferentemente de `em`, `rem` não herda em cascata, o que a torna muito mais previsível.

**Características:**
* Sempre relativa ao `<html>`
* Sem herança em cascata
* **Recomendada para tipografia moderna**
* Respeita preferências de acessibilidade do navegador

```css
html { font-size: 16px; } /* Tamanho base */

body { font-size: 1rem; } /* 16px */
h1 { font-size: 2rem; } /* 32px */
h2 { font-size: 1.5rem; } /* 24px */
p { font-size: 1rem; } /* 16px */
small { font-size: 0.875rem; } /* 14px */
```

**Por Que Usar rem para Tipografia:**
Se um usuário aumentar o tamanho da fonte no navegador (por necessidade de acessibilidade), todas as fontes definidas em `rem` aumentarão proporcionalmente. Isso não acontece com pixels fixos.

```css
/* ✗ Ruim: Não respeita preferências de acessibilidade */
body { font-size: 14px; }

/* ✓ Bom: Escala com as preferências do usuário */
body { font-size: 0.875rem; }
```

#### 2.2.4 Viewport Width (vw) e Viewport Height (vh)
Essas unidades são relativas ao tamanho da viewport (a janela do navegador).

* **1vw** = 1% da largura da viewport
* **1vh** = 1% da altura da viewport

**Características:**
* Muito úteis para seções de "hero" que ocupam a tela cheia
* Podem criar efeitos visuais interessantes
* Cuidado: em dispositivos móveis, a viewport pode incluir a barra de endereço

```css
/* Seção hero que ocupa a tela cheia */
.hero { height: 100vh; display: flex; align-items: center; }

/* Fonte que escala com a largura da tela */
h1 { font-size: 5vw; } /* 5% da largura da viewport */
```

**Armadilha - Viewport em Dispositivos Móveis:**
Em alguns navegadores móveis, a altura da viewport (`vh`) inclui a barra de endereço, que pode desaparecer durante o scroll. Isso pode causar comportamentos inesperados.

```css
/* Pode causar problemas em mobile */
.section { height: 100vh; }

/* Mais seguro: usar min-height */
.section { min-height: 100vh; }
```

### 2.3 Tabela Comparativa de Unidades

| Unidade | Referência | Herança | Acessibilidade | Uso Recomendado |
| :--- | :--- | :--- | :--- | :--- |
| **px** | Tamanho físico | Não | Não | Bordas, ícones |
| **%** | Elemento pai | Sim | Sim | Larguras, layouts |
| **em** | Fonte do elemento/pai | Sim | Sim | Espaçamentos proporcionais |
| **rem** | Fonte da raiz | Não | Sim | **Tipografia (recomendado)** |
| **vw** | Largura da viewport | Não | Sim | Seções hero, efeitos |
| **vh** | Altura da viewport | Não | Sim | Seções hero |

---

## 3. Media Queries: Sintaxe e Aplicação

As **Media Queries** são o mecanismo central que permite que um site se adapte a diferentes dispositivos. Elas funcionam testando características do dispositivo (como largura da tela) e aplicando estilos CSS apenas quando essas condições são verdadeiras.

### 3.1 Sintaxe Básica

```css
@media media-type and (condition) {
  /* Regras CSS aqui */
}
```

**Componentes:**
* **@media:** Palavra-chave que inicia uma media query
* **media-type:** O tipo de mídia (geralmente `screen`, `print`, `all`)
* **condition:** A condição a ser testada (ex: `max-width: 768px`)

### 3.2 Media Types

Os tipos de mídia indicam para qual tipo de dispositivo as regras se aplicam:

| Tipo | Descrição |
| :--- | :--- |
| **screen** | Telas (computadores, tablets, smartphones) |
| **print** | Impressoras e visualização de impressão |
| **all** | Todos os dispositivos (padrão) |

```css
/* Estilos para telas */
@media screen { body { font-size: 16px; } }

/* Estilos para impressão */
@media print { body { font-size: 12px; } }
```

### 3.3 Condições de Media Query

As condições mais comuns testam a largura da viewport:

#### 3.3.1 max-width
Aplica estilos quando a viewport tem **no máximo** a largura especificada.

```css
/* Aplica quando a tela tem 768px ou menos */
@media screen and (max-width: 768px) {
  .container { width: 100%; }
}
```

#### 3.3.2 min-width
Aplica estilos quando a viewport tem **no mínimo** a largura especificada.

```css
/* Aplica quando a tela tem 769px ou mais */
@media screen and (min-width: 769px) {
  .container { width: 960px; }
}
```

#### 3.3.3 Combinações com and
Você pode combinar múltiplas condições com `and`:

```css
/* Aplica apenas em telas entre 480px e 768px */
@media screen and (min-width: 480px) and (max-width: 768px) {
  .container { width: 90%; }
}
```

#### 3.3.4 Outras Condições Úteis

```css
/* Orientação */
@media (orientation: portrait) { /* Tela vertical */ }
@media (orientation: landscape) { /* Tela horizontal */ }

/* Resolução */
@media (min-resolution: 2dppx) { /* Telas Retina */ }

/* Altura */
@media (min-height: 800px) { /* Telas altas */ }
```

### 3.4 Estratégia Mobile-First

A estratégia **Mobile-First** é o padrão recomendado atualmente. Começamos estilizando para a menor tela (mobile) e usamos `min-width` para adicionar complexidade conforme a tela aumenta.

**Vantagens:**
* CSS mais limpo (menos overrides)
* Melhor performance em dispositivos móveis
* Força o foco no conteúdo essencial
* Alinha-se com a realidade: mais usuários acessam via mobile

```css
/* Estilo base para TODOS os dispositivos (mobile-first) */
body {
  font-size: 14px;
  line-height: 1.5;
}

.container {
  width: 100%;
  padding: 0 1rem;
}

.grid {
  display: grid;
  grid-template-columns: 1fr; /* Uma coluna em mobile */
  gap: 1rem;
}

/* Tablets (a partir de 768px) */
@media screen and (min-width: 768px) {
  body { font-size: 16px; }
  
  .grid {
    grid-template-columns: 1fr 1fr; /* Duas colunas */
  }
}

/* Desktops (a partir de 1024px) */
@media screen and (min-width: 1024px) {
  body { font-size: 18px; }
  
  .container { max-width: 1200px; margin: 0 auto; }
  
  .grid {
    grid-template-columns: 1fr 1fr 1fr; /* Três colunas */
  }
}
```

**Comparação: Desktop-First vs Mobile-First**

```css
/* ✗ Desktop-First (evitar) */
body { font-size: 18px; }
@media screen and (max-width: 1024px) { body { font-size: 16px; } }
@media screen and (max-width: 768px) { body { font-size: 14px; } }

/* ✓ Mobile-First (recomendado) */
body { font-size: 14px; }
@media screen and (min-width: 768px) { body { font-size: 16px; } }
@media screen and (min-width: 1024px) { body { font-size: 18px; } }
```

---

## 4. Breakpoints e Estratégias de Layout

Os **Breakpoints** são as larguras específicas onde o layout muda significativamente. A escolha correta de breakpoints é crucial para uma boa experiência responsiva.

### 4.1 Breakpoints Recomendados

Não memorize resoluções de dispositivos específicos. Em vez disso, use breakpoints baseados em como o conteúdo se comporta:

| Categoria | Breakpoint | Dispositivos Típicos |
| :--- | :--- | :--- |
| **Mobile Pequeno** | < 480px | Smartphones antigos, iPhone 5 |
| **Mobile Grande** | 480px - 767px | Smartphones modernos |
| **Tablet** | 768px - 1023px | iPads, tablets |
| **Desktop Pequeno** | 1024px - 1365px | Laptops, monitores pequenos |
| **Desktop Grande** | > 1366px | Monitores grandes, 4K |

```css
/* Mobile-first approach */
/* Base: Mobile Pequeno */

@media screen and (min-width: 480px) {
  /* Mobile Grande */
}

@media screen and (min-width: 768px) {
  /* Tablet */
}

@media screen and (min-width: 1024px) {
  /* Desktop Pequeno */
}

@media screen and (min-width: 1366px) {
  /* Desktop Grande */
}
```

### 4.2 Teste de Conteúdo para Definir Breakpoints

A melhor forma de definir breakpoints é testar o conteúdo real. Abra seu site em um navegador, redimensione a janela lentamente e observe onde o layout começa a parecer ruim. Esse é o seu breakpoint.

```css
/* Exemplo: Quando a navegação fica muito apertada, mude para menu hambúrguer */
@media screen and (max-width: 768px) {
  .nav-menu { display: none; }
  .hamburger-menu { display: block; }
}
```

---

## 5. Exemplos Práticos Detalhados

### 5.1 Layout de Duas Colunas Responsivo

Um padrão muito comum é um layout com uma barra lateral e conteúdo principal.

```html
<div class="layout">
  <aside class="sidebar">Barra Lateral</aside>
  <main class="content">Conteúdo Principal</main>
</div>
```

```css
/* Mobile: Empilhado verticalmente */
.layout {
  display: flex;
  flex-direction: column;
}

.sidebar {
  width: 100%;
  margin-bottom: 2rem;
}

.content {
  width: 100%;
}

/* Tablet e acima: Lado a lado */
@media screen and (min-width: 768px) {
  .layout {
    flex-direction: row;
    gap: 2rem;
  }

  .sidebar {
    width: 25%;
    margin-bottom: 0;
  }

  .content {
    width: 75%;
  }
}
```

### 5.2 Grid Responsivo de Produtos

Um padrão de e-commerce: 1 coluna em mobile, 2 em tablet, 4 em desktop.

```html
<div class="product-grid">
  <div class="product-card">Produto 1</div>
  <div class="product-card">Produto 2</div>
  <div class="product-card">Produto 3</div>
  <!-- ... mais produtos ... -->
</div>
```

```css
/* Mobile: 1 coluna */
.product-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 1rem;
}

/* Tablet: 2 colunas */
@media screen and (min-width: 768px) {
  .product-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

/* Desktop: 4 colunas */
@media screen and (min-width: 1024px) {
  .product-grid {
    grid-template-columns: repeat(4, 1fr);
  }
}
```

### 5.3 Tipografia Responsiva

As fontes devem aumentar gradualmente conforme a tela fica maior.

```css
/* Mobile */
h1 { font-size: 1.5rem; }
h2 { font-size: 1.25rem; }
body { font-size: 0.875rem; }

/* Tablet */
@media screen and (min-width: 768px) {
  h1 { font-size: 2rem; }
  h2 { font-size: 1.5rem; }
  body { font-size: 1rem; }
}

/* Desktop */
@media screen and (min-width: 1024px) {
  h1 { font-size: 2.5rem; }
  h2 { font-size: 1.75rem; }
  body { font-size: 1.125rem; }
}
```

### 5.4 Menu Responsivo com Hambúrguer

Um padrão clássico: navegação horizontal em desktop, menu hambúrguer em mobile.

```html
<nav class="navbar">
  <button class="hamburger">☰</button>
  <ul class="nav-menu">
    <li><a href="#">Home</a></li>
    <li><a href="#">Sobre</a></li>
    <li><a href="#">Serviços</a></li>
    <li><a href="#">Contato</a></li>
  </ul>
</nav>
```

```css
/* Mobile: Menu oculto por padrão */
.nav-menu {
  display: none;
  flex-direction: column;
  position: absolute;
  top: 60px;
  left: 0;
  right: 0;
  background-color: #333;
}

.nav-menu.active {
  display: flex;
}

.hamburger {
  display: block;
  background: none;
  border: none;
  color: white;
  font-size: 1.5rem;
  cursor: pointer;
}

/* Desktop: Menu visível, hamburger oculto */
@media screen and (min-width: 768px) {
  .hamburger {
    display: none;
  }

  .nav-menu {
    display: flex !important;
    flex-direction: row;
    position: static;
    background-color: transparent;
  }

  .nav-menu li {
    margin-left: 2rem;
  }
}
```

---

## 6. Boas Práticas e Armadilhas Comuns

### 6.1 Boas Práticas

#### 6.1.1 Sempre Defina a Viewport Meta Tag
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
Sem essa tag, o navegador mobile pode renderizar a página como se fosse desktop, causando zoom automático.

#### 6.1.2 Use Unidades Relativas
```css
/* ✓ Bom */
.button { padding: 0.5rem 1rem; font-size: 1rem; }

/* ✗ Ruim */
.button { padding: 8px 16px; font-size: 16px; }
```

#### 6.1.3 Teste em Dispositivos Reais
As ferramentas de desenvolvedor do navegador são úteis, mas nada substitui testar em um telefone real.

#### 6.1.4 Priorize o Conteúdo
Em mobile, remova elementos decorativos e foque no essencial.

```css
@media screen and (max-width: 768px) {
  .decorative-image { display: none; }
  .sidebar { display: none; }
}
```

### 6.2 Armadilhas Comuns

#### 6.2.1 Esquecer a Meta Viewport
Sem a meta tag viewport, o site não será responsivo.

#### 6.2.2 Usar Breakpoints Arbitrários
```css
/* ✗ Ruim: Breakpoints aleatórios */
@media (max-width: 500px) { }
@media (max-width: 900px) { }
@media (max-width: 1500px) { }

/* ✓ Bom: Breakpoints consistentes */
@media (max-width: 480px) { }
@media (max-width: 768px) { }
@media (max-width: 1024px) { }
```

#### 6.2.3 Misturar Desktop-First e Mobile-First
```css
/* ✗ Ruim: Inconsistente */
body { font-size: 18px; }
@media (min-width: 768px) { body { font-size: 16px; } }
@media (max-width: 480px) { body { font-size: 14px; } }

/* ✓ Bom: Consistentemente mobile-first */
body { font-size: 14px; }
@media (min-width: 768px) { body { font-size: 16px; } }
@media (min-width: 1024px) { body { font-size: 18px; } }
```

#### 6.2.4 Imagens Não Responsivas
```css
/* ✗ Ruim: Imagem transborda */
img { width: 800px; }

/* ✓ Bom: Imagem se adapta */
img { max-width: 100%; height: auto; }
```

---

## Conclusão

O domínio das Media Queries, das unidades relativas e dos breakpoints é o que diferencia um desenvolvedor amador de um Engenheiro de Software Front-End profissional. A responsividade não é uma "feature adicional"; é a base do desenvolvimento web moderno.

Pratique constantemente, teste em dispositivos reais e mantenha a acessibilidade como prioridade. Lembre-se: você não está desenvolvendo para dispositivos; você está desenvolvendo para **pessoas** que usam dispositivos.

---

## Referências

[1] MARCOTTE, Ethan. *Responsive Web Design*. A Book Apart, 2011.

[2] SILVA, Maurício Samy. *Web Design Responsivo: Aprenda a criar sites que se adaptam automaticamente a qualquer dispositivo*. Novatec, 2014.

[3] W3C. *Media Queries Level 4*. Disponível em: https://www.w3.org/TR/mediaqueries-4/

[4] MDN Web Docs. *Using media queries*. Disponível em: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_media_queries/Using_media_queries

---

## 👤 GitHub

[![Foto de Perfil](https://github.com/floresjcd.png?size=50)](https://github.com/floresjcd) 
**[@floresjcd](https://github.com/floresjcd)**