<h1> Pipe do RXJS e Resgatando dados através de parâmetros de rota </h1>

<h2> Sumário </h2>

- [RXJS Pipe](#rxjs-pipe)
  - [Piping](#piping)
- [Resgatando dados pelo URL através do parâmetro de rota](#resgatando-dados-pelo-url-através-do-parâmetro-de-rota)

## RXJS Pipe

Um Pipe do RXJS é diferente do Pipe do Angular

O RxJs disponibiliza operadores para trabalhar com os Observables de forma declarativa e clara. Sendo operadores, funções. Há dois tipos de operadores:

- **Pipeable Operators**: Podem ser *piped* (canalizados) ou seja, utilizar a sintaxe `observableInstance.pipe(operator)`, ou `observableInstance.pipe(operatorFactory())`, para manipular um fluxo de informações.
- **Creation Operators**: usadas pra criar novos Obeservables, exemplo `of(1,2,3)`

```ts
import { of, map } from 'rxjs';
of(1, 2, 3)
  .pipe(map((x) => x * x))
  .subscribe((v) => console.log(`value: ${v}`));
```

### Piping

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

Também é possível combinar Observables, por exemplo quando for chamar duas APIs concorrentemente (ao mesmo tempo), e retornar apenas uma informação ao usuário.

## Resgatando dados pelo URL através do parâmetro de rota

- É adicionado uma nova rota no module de rotas de produto `product-routing.module.ts` para a captura do produto pelo Id
- É utilizado o token `:id` que cria um slot no path para ser um parâmetro de rota

```ts
const routes: Routes = [
  { path: '', redirectTo: 'list', pathMatch: 'full' },
  { path: 'list', component: ListingComponent },
  { path: 'new', component: RegisterComponent },
  { path: 'edit/:id', component: RegisterComponent },
];
```

- É criado um novo método no **service** de produto para resgatar um único produto pelo ID

```ts
export class ProductService {
  private baseApiUrl = 'http://localhost:3000/';

  constructor(private http: HttpClient) {}

  getProducts(): Observable<ProductList> {
    return this.http.get<ProductList>(`${this.baseApiUrl}products`);
  }

  // novo método para resgatar o produto pelo Id
  getProductById(id: string): Observable<Product> {
    return this.http.get<Product>(`${this.baseApiUrl}products/${id}`);
  }
}
```

- É resgatado os dados do produto no componente que será renderizado o produto, pegando o ID, utilizando o serviço `ActivatedRoute` que foi injetado no constructor da classe do componente

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
