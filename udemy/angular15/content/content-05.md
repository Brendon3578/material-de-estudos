<h1> Capturando dados de um Formulário utilizando Template Driven </h1>

<h2> Sumário </h2>

- [Capturar e Preencher os campos de um Formulário](#capturar-e-preencher-os-campos-de-um-formulário)
  - [Utilizando Template Driven (forma antiga)](#utilizando-template-driven-forma-antiga)

## Capturar e Preencher os campos de um Formulário

Existe duas formas para capturar e manipular dados providos de um formulário no Angular, através do **Template Driven**(maneira antiga) e **Reactive Forms**

### Utilizando Template Driven (forma antiga)

O Template-Driven é uma das formas de se obter dados de um formulários e manipulá-los no Angular. Dessa forma é utilizado:

- O **ngModel** para se fazer o two-way data-binding de cada input do formulário
- Utilização do módulo **FormsModule** (para utilizar **ngModel**)

- Importando o `FormsModule` no `app.module.ts` (módulo root) para a utilização do `ngModel`:

```ts
import { FormsModule } from '@angular/forms';

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

- Criação do serviço do produto (CRUD) utilizando o `HttpClient`

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

- Utilizando um componente register (responsável por criar o produto) para os métodos HTTP: **POST** e **PUT**, no `register.component.ts`

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
      this.router.navigate(['product', 'list']);
    });
  }
}
```

- Template do componente Register `register.component.html`

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
    <!-- outros componentes do product... -->

    <button mat-raised-button color="primary" (click)="saveProduct()">
      Salvar
    </button>
  </form>
</main>
```
