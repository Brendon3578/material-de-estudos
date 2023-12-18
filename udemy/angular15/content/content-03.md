<h1> Services e Dependency Injection no Angular </h1>

<h2> Sumário </h2>

- [Serviços](#serviços)
- [Injeção de dependência](#injeção-de-dependência)
- [Angular HTTP Client](#angular-http-client)
- [Observable RXJS](#observable-rxjs)
  - [Promise e Observable](#promise-e-observable)

## Serviços

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

## Injeção de dependência

O decorator `@Injectable` indica ao Angular que essa classe é injetável e pode ser utilizada em outras classes. O `provideIn` é um metadado que é responsável por fornecer uma instância da respectiva classe através da Injeção de Dependência. No contexto acima, o `'root'` significa que o Angular fornecerá o serviço no injetor raiz, ou seja, para toda a aplicação

## Angular HTTP Client

É um módulo usado para fazer requisições HTTP dentro de uma aplicação Angular. É utilizado com os métodos HTTP GET, POST, PUT, DELETE, sendo possível também tratar os status de resposta da requisição HTTP, respostas comuns como os códigos 200, 201, 404, 500, etc.

Para utilizar o HTTP Client, o Angular utiliza de **Observables** da biblioteca RXJS para trabalhar de maneira **reativa**

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

---

Exemplo de uma requisição HTTP do tipo `GET` utilizando o HTTP Client, sendo a resposta dessa requisição, um **Observable:**

- Primeiro cria-se um serviço de Users para abstrair a lógica de trabalhar com requisições HTTP

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

- Depois, usa-se esse serviço no arquivo `.ts` do componente.
- É necessário usar o método `.subscribe` para capturar o dado que é retornado do método `getUsers`, que retorna um Observable

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
