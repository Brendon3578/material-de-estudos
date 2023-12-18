<h1> Componentes no Angular</h1>

<h2>Sumário</h2>

- [Criando um novo Componente](#criando-um-novo-componente)
- [Ciclo de vida dos componentes](#ciclo-de-vida-dos-componentes)
  - [Boas práticas](#boas-práticas)
- [Data Binding](#data-binding)
- [Directive ngIf e ngSwitch](#directive-ngif-e-ngswitch)
  - [Utilizando ngSwitch](#utilizando-ngswitch)
- [Diretivas Estrutural ngFor](#diretivas-estrutural-ngfor)
- [Pipe](#pipe)
  - [Criando uma Pipe Customizada](#criando-uma-pipe-customizada)

## Criando um novo Componente

Usa-se a CLI do Angular, com o seguinte comando `ng generate componente <meuCoomponente>`

```bash
ng generate component ./components/toolbar
# or
ng g component ./components/toolbar
# or
ng g c ./components/home
```

## Ciclo de vida dos componentes

São métodos hooks de lifecycle, ou seja, o Angular oferece os **Hooks** para lidar de situações durante o ciclo de vida do componente, de sua inicialização (init) até sua finalização (destroy)

É utilizado para garantir o melhor desempenho da aplicação e evitar vazamento de memória

São interfaces (contratos que podem ser implementados):

```ts
import { Component, OnInit } from '@angular/core';
// ...
export class AppComponent implements OnInit {

  // ...
  ngOnInit(): void {
    throw new Error('Method not implemented.');
  }
}
```

- **ngOnInit:** é executado uma vez quando o componente é **inicializado**.
  - Usado quando precisa fazer muitas coisas antes de inicializar o componente, podendo ser algum tipo de configuração, por exemplo: pegara parâmetros de rotas (url)
- **ngOnChanges:** executado uma vez na criação do componente e toda vez que ele sofrer alguma mudança;
- **ngDoCheck:** executado a cada mudança que o ngOnChange não detecta;
- **ngOnDestroy:** executado na destruição do componente.

<img src="./assets/angular-component-lifecycle.png" alt="Ciclo de vida dos componentes" width="240px">

### Boas práticas

- **ngDoCheck** e **ngOnChanges** não devem ser implementados juntos no mesmo componente.

## Data Binding

O Angular provê 3 categorias de bind (ligação) de dados de acordo com **direção do fluxo de dados**

- Da source (component) para à view (HTML)
- Da view (HTML) para o source (component)
- Two-way data binding (bind bidirecional) entre a view o source

- Se utiliza o `[ ]` para o bind do source para a view
- Se utiliza o `( )` para o bind do view para o source
- Se utiliza o `[( )]` para o two-way binds

Há 4 tipos de data binding

- Interporlation {{ title }}
- Property Binding `<input [placeholder]="myPlaceholder">`
- Event Bind (click)="evento"
- Two Way Data Binding - `<input [(ngModel)]="title">` junto com a importação de `FormsModule` dentro do componente

## Directive ngIf e ngSwitch

Utiliza-se a diretiva `ngIf` para renderizar de forma condicional (se uma condição for satisfeita, se o valor da condição for True)

```html
<p *ngIf="message == 'banana'">É uma banana!</p>
```

Também é possível renderizar utilizando o `else` para renderizar "*caso contrários*" da condição anterior

```html
<p *ngIf="message == 'Banana'; else messagePadrao">É uma banana!</p>

<ng-template #messagePadrao>
  <p>Não é uma banana!</p>
</ng-template>
```

### Utilizando ngSwitch

É utilizado para renderizar com Valores Idênticos, usa-se com o `ngSwitchCase` e o `ngSwitchDefault`

```html
<span [ngSwitch]="message">
  <p *ngSwitchCase="'banana'">É uma banana</p>
  <p *ngSwitchCase="'maçã'">Não é uma maçã</p>
  <p *ngSwitchDefault>Não é nada!</p>
</span>
```

## Diretivas Estrutural ngFor

Usa-se para renderizar um template de cada item de uma lista.

```html
<tr *ngFor="let product of products">
  <td>{{ product.name }}</td>
  <td>{{ product.price | currency }}</td>
</tr>
```

## Pipe

É utilizado para formatar (transformar) dados antes de serem exibidos (visualizados) no template.

Para usar o Pipe, usa-se o pipe-operator `|`

```jsx
<td>{{ product | json }}</td>
<td>{{ product.name | uppercase }}</td>
<td>{{ product.price | currency : "BRL" }}</td>

```

Outros exemplos

- **DatePipe** para formatações de datas
- **UpperCasePipe** para tornar letras maiúsculas
- **LowerCasePipe** para tornar letras minúsculas
- **CurrencyPipe** para formatações de moedas do tipo ISO 4217

### Criando uma Pipe Customizada

Exemplo: criar uma pipe para pegar a quantidade de reviews e quantidade de estrelas totais de um produto e mostrar em tela as estrelas correspondentes da avaliação do produto:

```bash
ng g pipe /pipes/stars
# or
ng generate /pipe/
```

```ts
// ./src/pipes/stars.pipe.ts
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'stars',
})
export class StarsPipe implements PipeTransform {
  transform(stars: number, reviews: number): string {
    let starString = '⭐';

    let maxStarsValue = reviews * 5;
    let starsStruck = (stars / maxStarsValue / 2) * 10;

    return `${starString.repeat(starsStruck)}`;
  }
}
```

```ts
// componente
products = [
  {
    name: 'Monitor Gamer Curvo',
    price: 8599.9,
    stars: 22,
    reviews: 5,
  },
  {
    name: 'Cadeira Gamer  RGB',
    price: 959.9,
    stars: 20,
    reviews: 8,
  },
  // outros products..
];
```

```jsx
// template:
<tbody>
  <tr * ngFor="let product of products">
    <td>{{ product.name | uppercase }}</td>
    <td>{{ product.price | currency : "BRL" }}</td>
    <td>{{ product.stars }}</td>
    <td>{{ product.reviews }}</td>
    <td>{{ product.stars | stars : product.reviews }}</td>
  </tr>
</tbody>
```

Resultado final:

![Tabela de star rating](./assets/star-pipe.PNG)
