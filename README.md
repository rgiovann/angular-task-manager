# Easy Task — Gerenciador de Tarefas com Angular

Aplicação web de gerenciamento de tarefas construída com **Angular 18** e foco em uma experiência simples: selecionar usuário, visualizar tarefas, criar novas tarefas e marcar tarefas como concluídas.

> Este projeto usa recursos modernos do Angular (como **Standalone Components** e o novo controle de fluxo com `@if`/`@for`) para manter o código enxuto, modular e fácil de evoluir.

---

## 📌 Visão geral

O sistema apresenta uma lista de usuários e, para cada usuário selecionado, exibe suas tarefas. As tarefas são persistidas em `localStorage`, permitindo manter os dados entre recarregamentos da página.

### Fluxo principal

1. Selecionar um usuário.
2. Ver tarefas associadas ao usuário.
3. Abrir formulário de criação de tarefa.
4. Salvar tarefa.
5. Concluir (remover) tarefa.

---

## ✨ Features da aplicação

- Seleção de usuário com destaque visual do item ativo.
- Listagem de tarefas por usuário.
- Criação de novas tarefas por formulário.
- Remoção de tarefas concluídas.
- Persistência de tarefas em `localStorage`.
- Formatação de data em português (`pt-BR`).
- Interface com componentes reutilizáveis (`CardComponent`).

---

## 🅰️ Recursos do Angular usados (destaque)

Aqui estão os principais recursos que você utilizou no projeto:

### 1) Standalone Components

O projeto foi estruturado com componentes standalone, sem necessidade de `NgModule` tradicional para composição da UI.

- `AppComponent`, `UserComponent`, `TasksComponent`, `TaskComponent`, `NewTaskComponent`, `HeaderComponent` e `CardComponent` usam `standalone: true`.
- Cada componente declara explicitamente seus `imports`, melhorando legibilidade e isolamento.

### 2) Bootstrap moderno com `bootstrapApplication`

A aplicação inicia via API moderna:

- `bootstrapApplication(AppComponent, { providers: [...] })`
- Registro de locale (`registerLocaleData`) e injeção de `LOCALE_ID` diretamente no bootstrap.

### 3) Novo controle de fluxo de template (`@if` e `@for`)

Você utiliza a sintaxe moderna do Angular para renderização condicional e repetição:

- `@if` para exibir fallback ou modal de nova tarefa.
- `@for (...; track ...)` para listar usuários e tarefas com `track` por id.

Isso melhora clareza do template e performance no diff de listas.

### 4) Comunicação entre componentes (`@Input` / `@Output`)

- `@Input` para passagem de dados (usuário selecionado, lista de tarefas, ids, etc.).
- `@Output` com `EventEmitter` para emitir ações (ex.: seleção de usuário, fechar modal).

### 5) Injeção de dependência (DI)

- Serviço `TasksService` com `@Injectable({ providedIn: 'root' })`.
- Uso de DI por construtor e também via função `inject(...)` em componentes.

### 6) Forms com `FormsModule` e `ngModel`

No componente de criação de tarefa:

- Import de `FormsModule` no componente standalone.
- Two-way data binding com `[(ngModel)]` para campos do formulário.
- Submissão tratada por `(ngSubmit)`.

### 7) Pipes nativos e internacionalização básica

- Uso de `DatePipe` para formatar data de entrega.
- Padrão de formatação em português (`d 'de' MMMM 'de' yyyy`) com `LOCALE_ID = 'pt-BR'`.

### 8) Data binding e event binding

- Interpolação `{{ ... }}` para renderizar dados dinâmicos.
- Property binding (`[src]`, `[alt]`, `[class.active]`, etc.).
- Event binding (`(click)`, `(ngSubmit)`).

### 9) Content projection com `<ng-content>`

`CardComponent` funciona como wrapper visual reutilizável usando projeção de conteúdo.

---

## 🧱 Estrutura do projeto

```text
src/
  app/
    header/                # Cabeçalho da aplicação
    shared/card/           # Componente visual reutilizável
    user/                  # Item de usuário e seleção
    tasks/                 # Feature de tarefas
      task/                # Item individual de tarefa
      new-task/            # Formulário de criação
    app.component.*        # Componente raiz
    dummy-users.ts         # Dados mockados de usuários
  assets/                  # Imagens e avatares
  main.ts                  # Bootstrap + locale pt-BR
```

---

## ⚙️ Pré-requisitos

- **Node.js** (recomendado: versão LTS)
- **npm**
- **Angular CLI** (opcional, pode usar via `npx`)

---

## 🚀 Como executar

### 1) Instalar dependências

```bash
npm install
```

### 2) Rodar em desenvolvimento

```bash
npm start
```

A aplicação ficará disponível em:

- `http://localhost:4200/`

### 3) Build de produção

```bash
npm run build
```

Os artefatos serão gerados em `dist/`.

### 4) Executar testes

```bash
npm test
```

---

## 🧠 Regras de negócio implementadas

- Cada tarefa pertence a um `userId`.
- Apenas tarefas do usuário selecionado são exibidas.
- Ao criar tarefa, ela entra no início da lista (`unshift`).
- Ao concluir tarefa, ela é removida da coleção.
- Toda alteração na lista de tarefas é persistida em `localStorage`.

---

## 💾 Persistência

A persistência usa API nativa do navegador:

- Leitura inicial: `localStorage.getItem('tasks')`.
- Escrita após criar/remover: `localStorage.setItem('tasks', JSON.stringify(tasks))`.

> Observação: como é persistência local no navegador, os dados não são compartilhados entre dispositivos/usuários e podem ser limpos manualmente pelo usuário.

---

## 📈 Possíveis evoluções

- Validação de formulário (campos obrigatórios, datas válidas, mensagens de erro).
- Separar tipos/interfaces em pasta de domínio.
- Adicionar camada de API real (HTTP) no lugar de `localStorage`.
- Adicionar estado reativo com Signals.
- Testes unitários para componentes e serviço de tarefas.
- Filtros e ordenação de tarefas (por data, status, prioridade).

---

## 📜 Scripts disponíveis

- `npm start` → inicia servidor de desenvolvimento (`ng serve`)
- `npm run build` → gera build de produção (`ng build`)
- `npm test` → executa testes (`ng test`)
- `npm run watch` → build em modo watch

---

## 🏁 Conclusão

Este projeto é um ótimo exemplo de aplicação Angular moderna e enxuta, explorando **componentização**, **DI**, **templates reativos**, **forms**, **pipes** e **persistência local** com uma base preparada para evolução.
