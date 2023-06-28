<h1> Conteúdo 03 </h1>

<h2> Sumário </h2>

- [RXJS Pipe](#rxjs-pipe)
  - [Piping](#piping)
- [Resgatando dados pelo URL](#resgatando-dados-pelo-url)
- [Capturar e Preencher os campos de um Formulário](#capturar-e-preencher-os-campos-de-um-formulário)
  - [Utilizando Template Driven (forma antiga)](#utilizando-template-driven-forma-antiga)
  - [Utilizando Reactive Forms](#utilizando-reactive-forms)

# RXJS Pipe

Um Pipe do RXJS é diferente do Pipe do Angular

O RxJs disponibiliza operadores para trabalhar com os Observables dde forma declarativa e clara. Sendo operadores, funções. Há dois tipos de operadores:

- **Pipeable Operators**: Podem ser *piped* (canalizados) ou seja, utilizar a sintaxe `observableInstance.pipe(operator)`, ou `observableInstance.pipe(operatorFactory())`, para manipular um fluxo de informações.
- **Creation Operators**: usadas pra criar novos Obeservables, exemplo `of(1,2,3)`

```ts
import { of, map } from 'rxjs';
of(1, 2, 3)
  .pipe(map((x) => x * x))
  .subscribe((v) => console.log(`value: ${v}`));
```

## Piping

Observables têm o método `.pipe()` para facilitar a clareza na leitura durante a transformação dos dados do Observable. Ele transforma os dados emitidos por um Observable antes de dar ao Observador (`subscribe`)

É possível usar o método `tap` para **side-effects** para notificar e monitorar as mudanças do Observable fonte

Exemplo de uso no Angular:

```ts
constructor() {
  of('banana', 'pitaia', 'pera', 'maçã')
    .pipe(
      map((fruta) => fruta.toUpperCase()),
      filter((fruta) => fruta.startsWith('B') || fruta.startsWith('M')),
      tap(console.log)
    )
    .subscribe((result) => {
      this.frutas.push(result);
    });
}
```

Resultado:

![Resultado do Código do Observable com Piping](../assets/example-pipe-rxjs.PNG)

Uma [boa prática](https://angular.io/guide/rx-library#naming-conventions-for-observables) para os Observables, é sufixar a variável com o símbolo de dólar **($)** para indicar os Observables:

```ts
import { filter, map, of, tap } from 'rxjs';

frutas$ = of('banana', 'pitaia', 'pera', 'maçã');

constructor() {
  this.frutas$
    .pipe(
      map((fruta) => fruta.toUpperCase()),
      filter((fruta) => fruta.startsWith('B') || fruta.startsWith('M')),
      tap(console.log)
    )
    .subscribe((result) => {
      this.frutas.push(result);
    });
}
```

É possível combinar Observables, por exemplo chamar duas APIs concorrentemente, e retornar ao usuário apenas um retorno.

# Resgatando dados pelo URL

- Adicione uma nova rota no module de rotas de produto `product-routing.module.ts`

```ts
const routes: Routes = [
  { path: '', redirectTo: 'list', pathMatch: 'full' },
  { path: 'list', component: ListingComponent },
  { path: 'new', component: RegisterComponent },
  { path: 'edit/:id', component: RegisterComponent },
];
```

- Crie um novo método no **service** de produto para resgatar um único produto pelo ID

```ts
export class ProductService {
  private baseApiUrl = 'http://localhost:3000/';

  constructor(private http: HttpClient) {}

  getProducts(): Observable<ProductList> {
    return this.http.get<ProductList>(`${this.baseApiUrl}products`);
  }

  // novo método para resgatar o produto pelo IDd
  getProductById(id: string): Observable<Product> {
    return this.http.get<Product>(`${this.baseApiUrl}products/${id}`);
  }
}
```

- Resgate o produto no componente que será renderizado o produto, utilizando o serviço injetado de router `ActivatedRoute`

```ts
export class RegisterComponent implements OnInit {
  id!: string;
  product!: Product;

  constructor(
    private ProductService: ProductService,
    private activatedRoute: ActivatedRoute
  ) {}

  ngOnInit(): void {
    // pegar o id do produto em uma url: [//http](http://localhost:4200/product/edit/1)
    // sendo o '/product', o url raiz
    this.id = this.activatedRoute.snapshot.url[1].path;

    this.ProductService.getProductById(this.id).subscribe(
      (product: Product) => (this.product = product)
    );
  }
}
```

# Capturar e Preencher os campos de um Formulário

## Utilizando Template Driven (forma antiga)

O Template-Driven é uma das formas de se utilizar formulários no Angular, nele é utilizado:

- **ngModel** pra fazer o two-way data-binding de cada input do formulário
- Utilização do FormsMoule (para o ngModel funcionar)

Importando o `FormsModule` no `app.module.ts` (módulo root) para a utilização o `ngModel`:

```ts
import { FormsModule }   from '@angular/forms';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule // <-- Forms Module
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

Model do product

```ts
// product/models/product.model.ts
interface Product {
  id?: string;
  name: string;
  description: string;
  imageUrl?: string;
  price: number;
  stars: number;
  reviews: number;
}
interface ProductList extends Array<Product> {}

export { Product, ProductList }
```

Criação do serviço do produto (CRUD) utilizando o `HttpClient`

```ts
// product/services/product.service.ts
import { HttpClient } from '@angular/common/http';
import { Injectable } from '@angular/core';
import { Observable } from 'rxjs';
import { Product, ProductList } from '../models/product.model'; // interfaces (model) do product

@Injectable({
  providedIn: 'root',
})
export class ProductService {
  private baseApiUrl = 'http://localhost:3000/'; // API do json-server

  constructor(private http: HttpClient) {}

  getProducts(): Observable<ProductList> {
    return this.http.get<ProductList>(`${this.baseApiUrl}products`);
  }

  getProductById(id: string): Observable<Product> {
    return this.http.get<Product>(`${this.baseApiUrl}products/${id}`);
  }

  updateProduct(product: Product): Observable<Product> {
    return this.http.put<Product>(
      `${this.baseApiUrl}products/${product.id}`,
      product
    );
  }

  createProduct(product: Product): Observable<Product> {
    return this.http.post<Product>(`${this.baseApiUrl}products`, product);
  }

  deleteProduct(id: string): Observable<Product> {
    return this.http.delete<Product>(`${this.baseApiUrl}products/${id}`);
  }
}
```

Utilizando um componente register (criar) para os métodos HTTP POST e PUT, no `register.component.ts`

```ts
// product/register/register.component.ts
import { Component, OnInit } from '@angular/core';
import { ProductService } from './../services/product.service';
import { ActivatedRoute, Router } from '@angular/router';
import { Product } from '../models/product.model';

@Component({
  selector: 'app-register',
  templateUrl: './register.component.html',
  styleUrls: ['./register.component.scss'],
})
export class RegisterComponent implements OnInit {
  title: string = ''; // <-- title do formulário da pagina
  route: string = '';
  // flag para a captura da ação que é para fazer (se é pra cadastrar - POST - ou alterar - PUT - um prouto)
  isNewProduct: boolean = false;

  id!: string;
  product!: Product;

  name: string = '';
  description: string = '';
  price: number = 0;
  //..outras propriedades

  constructor(
    private productService: ProductService,
    private activatedRoute: ActivatedRoute,
    private router: Router
  ) {}

  ngOnInit(): void {
    this.route = this.activatedRoute.snapshot.url[0].path; // -> pegar o path da url (create ou edidt):
    // na url: http://localhost:4200/product/create
    if (this.route === 'edit') {
      this.id = this.activatedRoute.snapshot.url[1].path; // pegar o id do produto na url http://localhost:4200/product/edit/2
      this.productService
        .getProductById(this.id)
        .subscribe((product: Product) => {
          this.product = product;
          this.name = this.product.name;
          this.description = this.product.description;
          //..outras propriedades

          this.title = `Editar produto ${this.name}`;
        });
    } else {
      // create new product
      this.isNewProduct = true;
      this.title = 'Adicionar novo produto';
    }
  }

  saveProduct() {
    const productData: Product = {
      id: this.id,
      name: this.name,
      description: this.description,
      //..outras propriedades
    };

    if (this.isNewProduct) {
      this.createProduct(productData);
    } else {
      this.updateProduct(productData);
    }
  }

  updateProduct(productData: Product) {
    this.productService.updateProduct(productData).subscribe((res) => {
      this.router.navigate(['product', 'list']);
    });
  }

  createProduct(productData: Product) {
    this.productService.createProduct(productData).subscribe((res) => {
      console.log('Produto criaddo com sucesso');
      this.router.navigate(['product', 'list']);
    });
  }
}
```

Componente do `register.component.html`

```html
<!-- register.component.html -->
<main>
  <form class="example-form mat-elevation-z8">
    <h1 class="title">{{ title }}</h1>
    <mat-form-field class="example-full-width">
      <mat-label>Nome</mat-label>
      <input
        matInput
        placeholder="Nome do produto"
        [(ngModel)]="name"
        [ngModelOptions]="{ standalone: true }"
        name="name"
      />
    </mat-form-field>

    <mat-form-field class="example-full-width">
      <mat-label>Descrição</mat-label>
      <textarea
        matInput
        placeholder="Descrição do produto"
        name="description"
        [(ngModel)]="description"
        [ngModelOptions]="{ standalone: true }"
      ></textarea>
    </mat-form-field>
    <!-- outros componentes do product -->

    <button mat-raised-button color="primary" (click)="saveProduct()">
      Salvar
    </button>
  </form>
</main>
```

## Utilizando Reactive Forms

Ver [conteúdo 04](./content-04.md)
