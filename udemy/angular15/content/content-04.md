<h1> Conteúdo 04 </h1>

<h2>Sumário</h2>

- [Utilizando Reactive Forms](#utilizando-reactive-forms)
- [Criando validações customizadas](#criando-validações-customizadas)

## Utilizando Reactive Forms

A maior diferença entre o Reactive Forms e o Template Driven  é o modo que os dados são gerenciados dentro da aplicação,  no Reactive Forms o estado do formulário é representado utilizando Observable (paradigma da programação reativa utilizando o RxJs e assincronismo), no qual é possível manipular os dados em tempo real

Com o Reactive Forms é possível ter um controle maior nas validações, sendo possível facilmente criar validação própria customizada da forma que desejar.

É preciso importar o `ReactiveFormsModule` no modulo de routing

Depois agrupar todos os "controls" (inputs etc) do formulário dentro de um FormGroup:

```ts
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

@Component({
  selector: 'app-register',
  //... other properties
})
export class RegisterComponent implements OnInit {
  //... other properties
  product!: Product;

  formRegisterProduct!: FormGroup; // <-- form Group de todos os inputs

  constructor(
    private productService: ProductService,
    private activatedRoute: ActivatedRoute,
    private router: Router,
    // dependency injection do FormBuilder
    private formBuilder: FormBuilder
  ) {}

  ngOnInit(): void {
    this.route = this.activatedRoute.snapshot.url[0].path;
    // utilizar de um método pra criar o formulário 
    this.createForm();

    if (this.route === 'edit') {
      this.id = this.activatedRoute.snapshot.url[1].path;
      this.productService
        .getProductById(this.id)
        .subscribe((product: Product) => {
          this.product = product;

          // setar todos os controles do forms com o product extraído
          // ..do banco de dados
          this.formRegisterProduct.controls['name'].setValue(this.product.name);
          this.formRegisterProduct.controls['description'].setValue(
            this.product.description
          );
          this.formRegisterProduct.controls['price'].setValue(
            this.product.price
          );
          // ..outros controles do Product
        });
    } else {
      // ..comportamento do create new product (formulário vazio)
    }
  }

  createForm() {
    // construindo um formulárioGorup com o formBuilder.group e utilizando validações
    this.formRegisterProduct = this.formBuilder.group({
      name: ['', [Validators.required]],
      description: ['', [Validators.required]],
      price: [0, [Validators.required, Validators.min(1)]],
    });
  }

  // método que vai ser executado através do evento click do botão de cadastrar product/atualizar product
  saveProduct() {
    // verificação se o formulário foi alterado para evitar atualizações desnecessárias no banco de dados (no caso de atualizar produto)
    if (!(this.formRegisterProduct.dirty && this.formRegisterProduct.touched)) {
      return;
    }

    // verificar se o formulário está validado
    if (this.formRegisterProduct.valid) {
      // armazenar os valores do formulário
      const productData = this.formRegisterProduct.value;

      if (this.isNewProduct) {
        this.createProduct(productData);
      } else {
        // atualizar o id do produto
        this.updateProduct({ ...productData, id: this.id });
      }
    }
  }

  updateProduct(productData: Product) {
    this.productService.updateProduct(productData).subscribe((res) => {
      this.router.navigate(['product', 'list']);
      console.log(res);
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

Template do componente do formulário

```html
<main>
  <!-- setando o formGroup -->
  <form class="example-form mat-elevation-z8" [formGroup]="formRegisterProduct">
    <mat-form-field class="example-full-width">
      <mat-label>Nome</mat-label>
      <!-- setando o formControlName do input -->
      <input matInput placeholder="Nome do produto" formControlName="name" />
      <!-- utilização do mat-error (material icons) para feedback de input que não é valida -->
      <mat-error>Insira um nome para o produto</mat-error>
    </mat-form-field>

    <mat-form-field class="example-full-width">
      <mat-label>Descrição</mat-label>
      <textarea
        matInput
        placeholder="Descrição do produto"
        formControlName="description"
      ></textarea>
      <mat-error>Insira uma descrição para o produto</mat-error>
    </mat-form-field>


    <mat-form-field class="example-full-width">
      <mat-label>Preço</mat-label>
      <input
        type="number"
        matInput
        placeholder="Ex: 199.99"
        formControlName="price"
      />

      <mat-error>Insira um número maior que 0 para o preço produto</mat-error>
    </mat-form-field>

    <!-- desabilitar submit se o formulário não é valido -->
    <button
      mat-raised-button
      color="primary"
      (click)="saveProduct()"
      [disabled]="formRegisterProduct.valid == false"
    >
    </button>
  </form>
</main>
```

## Criando validações customizadas

Para criar uma validação customizada, basta criar uma função e usar a interface `ValidatorFn`, veja o exemplo criando uma validação para um input de **password**:

```ts
// ../validators/strongPasswordValidator.ts
import { AbstractControl, ValidationErrors, ValidatorFn } from '@angular/forms';

export function strongPasswordValidator(): ValidatorFn {
  return (control: AbstractControl): ValidationErrors | null => {
    const value = control.value;
    if (!value) {
      return null;
    }
    const hasUppercaseCharacters = /[A-Z]+/.test(value);
    const hasLowercaseCharacters = /[a-z]+/.test(value);
    const hasNumericCharacters = /[0-9]+/.test(value);

    const passwordVality =
      hasUppercaseCharacters && hasLowercaseCharacters && hasNumericCharacters;

    return !passwordVality ? { strongPassword: true } : null;
  };
}
```

Implementação no componente de register:

```ts
import { FormBuilder, FormGroup, Validators } from '@angular/forms';
import { strongPasswordValidator } from '../validators/strongPasswordValidator';

export class RegisterComponent implements OnInit {
  formRegisterProduct!: FormGroup;

  constructor(
    private formBuilder: FormBuilder
  ) {}

  ngOnInit(): void {
    this.createForm();
  }

  createForm() {
    this.formRegisterProduct = this.formBuilder.group({
      password: [
        '',
        [
          Validators.required,
          Validators.minLength(8),
          strongPasswordValidator(),
        ],
      ]
    });
  }

  get password() {
    return this.formRegisterProduct.get('password');
  }
}
```

Implementação no template do componente (html):

```html
<main>
  <form class="example-form mat-elevation-z8" [formGroup]="formRegisterProduct">

    <mat-form-field class="example-full-width">
      <mat-label>Senha</mat-label>
      <input
        type="text"
        matInput
        placeholder="Ex: 199.99"
        formControlName="password"
        id="password"
      />
      <mat-error *ngIf="password?.errors?.['required']">
        Insira uma senha forte
      </mat-error>
      <mat-error *ngIf="password?.errors?.['minlength']">
        A senha tem que ter pelo menos 8 caracteres
      </mat-error>
      <mat-error *ngIf="password?.errors?.['strongPassword']">
        A senha tem que ter pelo menos uma caractere maiúsculo, minusculo e um número
      </mat-error>
    </mat-form-field>
  </form>
</main>
```
