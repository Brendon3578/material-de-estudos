<h1> Módulos, Lazy Loading e Angular Material </h1>

<h2>Sumário</h2>

- [Módulos](#módulos)
- [Lazy Loading nas Rotas](#lazy-loading-nas-rotas)
- [Angular Material](#angular-material)

## Módulos

São uma forma de organizar e encapsular (separar) funcionalidades e da aplicação em blocos (agrupamento) coesos e independentes.

- Utilizado para dividir a aplicação em partes menores, para a manutenção mais rápida e escalabilidade do código

Há 2 tipos de módulos:

- **Feature Modules**: encapsula uma funcionalidade da aplicação, ex: módulo de login ou módulo de carrinho de compras.
  - Contêm components, directives, services e pipes necessário para implementar a funcionalidade
- **Root Module**: módulo principal da aplicação, carregado quando a aplicação é inicializado

```bash
ng generate module ./features/product --routing
# or
ng g m ./features/product --routing

```

Usa-se a flag `--routing` para criar um arquivo de rotas para gerenciar as rotas dos componentes

## Lazy Loading nas Rotas

Por padrão, *ngModules* são *eagerly loaded* (carregamento ansioso), quando a aplicação é carregada, todos os módulos também serão.

O **Lazy Loading** (carregamento preguiçoso ou tardio) é utilizado para melhorar o desempenho da aplicação, e não abrir a rota instantaneamente, ou seja, apenas quando solicitado e não no primeiro acesso.

Implementa-se, utilizando o `loadChildren` (um módulo) em vez de o `component` no arquivo de rotas da aplicação

```ts
const routes: Routes = [
  //... other routes
  { path: 'home', component: HomeComponent },
  {
    path: 'product',
    loadChildren: () =>
      import('./features/product/product.module').then((m) => m.ProductModule),
  },
];
```

Dentro do arquivo de rotas do módulo de products:

```ts
const routes: Routes = [
  { path: '', redirectTo: 'list', pathMatch: 'full' },
  { path: 'list', component: ListingComponent },
  { path: 'new', component: RegisterComponent },
];
```

## Angular Material

É uma biblioteca usado pra construir interfaces criado pela própria equipe de desenvolvedores do Angular. Ajuda no desenvolvimento e manutenção do código utilizando temas já pré-criados pelo Angular Material

```bash
# para adicionar na aplicação angular:
ng add @angular/material
```
