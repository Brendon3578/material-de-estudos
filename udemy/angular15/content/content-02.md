<h1> Conteúdo 02 </h1>

# Módulos

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

# Lazy Loading nas Rotas

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

# Angular Material

É uma biblioteca usado pra construir interfaces criado pela própria equipe de desenvolvedores do Angular. Ajuda no desenvolvimento e manutenção do código utilizando temas já pré-criados pelo Angular Material

```bash
# para adicionar na aplicação angular:
ng add @angular/material
```

# Services e Dependency Injection no Angular

São serviços, objetos, funções ou um valor que uma classe necessita para desempenhar sua função

Um **Service** é um arquivo que guarda a lógica de negócios, sendo responsável pela comunicação com o servidor. Ele nos auxiliar a separar dos componentes algumas informações importantes e o modo como vamos obtê-las, além de dados de requisições do servidor

```bash
ng generate service features/product/services/product
# or
ng g s features/product/services/product
```

No arquivo:

```ts
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class ProductService {
  constructor() { }
}
```

O decorator `@Injectable` indica ao Angular que essa classe é injetável e pode ser utilizada em outras classes. O `provideIn` é um metadado que é responsável por fornecer uma instância da respectiva classe através da Injeção de Dependência. No contexto acima, o `'root'` significa que o Angular fornecerá o serviço no injetor raiz, ou seja, para toda a aplicação

## Angular HTTP Client

É um módulo usado para fazer requisições HTTP dentro da aplicação angular, utilizando seus métodos HTTP (GET, POST, PUT, DELETE) e tratando das respostas comuns (200, 201, 404, 500) etc.

Angular usa o **Observable** do RXJS

## Observable RXJS

RxJs **(Reactive Extensions Library for JavaScript)** é uma biblioteca que facilita o uso de manipulação de dados de forma **assíncrona**, sem utilizar Promises nativas do javascript (método fetch, async, await, then, etc).

O **Observable** abre um canal de stream (transferência) de dados, como se fosse a ideia de um cano, que pode ser "observado" por 1 ou n assinantes (subscribers ou observadores), que quando um source (fonte) de dados é modificada, todos os observadores serão notificados para responder sobre essa mudança

- São dados que respondam a mudanças em **tempo real** para os subscribers (destino)
- Não há a necessidade de mudar a interface manualmente

### Promise e Observable

Ambos são utilizados para lidar com programação assíncrona em JavaScript

- Promises pode ter os estados pending (inicial), fulfilled (concluído), rejected (rejeitado/falha/erro).
- Observable pode emitir vários valores ao longo do tempo

- Resolução Única vs Múltiplas Atualizações
- Tipos de Dados
- Gerenciamento de Erro (try catch) x (catchError)
- Cancelamento (não pode cancelada) x (pode ser cancelada)

Exemplo utilizando uma API

```ts
import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root',
})
export class UserService {
  private apiUrl = 'https://api.example.com/users';

  constructor(private http: HttpClient) {}

  getUsers(): Observable<any> {
    return this.http.get<any>(this.apiUrl);
  }
}
```

No componente:

```ts
import { Component, OnInit } from '@angular/core';
import { UserService } from '../user.service';

@Component({
  selector: 'app-user-list',
  templateUrl: './user-list.component.html',
  styleUrls: ['./user-list.component.scss'],
})
export class UserListComponent implements OnInit {
  users: any[]

  constructor(private userService: UserService) {}

  ngOnInit(): void {
    this.userService.getUsers().subscribe((data) => {
      this.users = data;
    });
  }
}
```
