# Estudo do Angular 15

Anotações feitas a partir do Curso de Angular 15 do Alexandre Ribeiro. [Link do curso na Udemy](https://www.udemy.com/course/curso-angular-15/)

## Componentes no Angular

- Criando um componente
- Ciclo de vida dos componentes
  - Métodos `OnInit`, `OnChanges`, `DoCheck`, `OnDestroy`
- Data Binding - capturando dados nos componentes
- Diretivas estruturais `ngIf`, `ngSwitch` e `ngFor`
- **Pipes** para formatação de dados antes de serem exibidos na view (template)
  - Criando uma Pipe customizada de avaliações de um produto (estrelas)

[Link de acesso para o guia](./content/content-01.md)

## Módulos, Lazy Loading e Angular Material

- O que são módulos no Angular
- Lazy Loadings nas rotas para melhorar o desempenho da aplicação
- Angular Material para estilização "nativa" do Angular
  - Como criar um módulo para centralizar importações do Angular Material - [Acesse o guia](./content/extra/angular-material-module.md)
  - Como Implementar o Componente de DatePicker traduzido para PT-BR - [Acesse o guia](./content/extra/angular-material-datepicker.md)
  - Como utilizar o Componente de SnackBar sendo um serviço reutilizável - [Acesse o guia](./content/extra/angular-material-snackbar-as-service.md)

[Link de acesso para o guia](./content/content-02.md)

## Serviços e Injeção de Dependência

- O que são **serviços** e como ocorre a **injeção de dependência** nos módulos do Angular
- Como usar o Angular **HTTP Client** para trabalhar com requisições HTTP
  - Utilização de Observables do RXJS para uma programação reativa
  - Diferença entre Promise nativa do JS e o Observable do RXJS
- Exemplo de uma requisição HTTP Client e como usar com os serviços

[Link de acesso para o guia](./content/content-03.md)

## Pipe do RXJS e Resgatando dados através de parâmetros de rota

- Pipe do RXJS para transformação de dados do Observable
  - Métodos como `pipe()`, `tap()`, `filter()`
  - Boa prática para nomear Observables
- Resgatar informações através de parâmetros de rota

[Link de acesso para o guia](./content/content-04.md)

## Capturando e Manipulando dados de um Formulário no Angular

### Utilizando Template Driven

- Formas de capturar e manipular dados providos de um formulário html
- Captura de dados do formulário através de Template Driven, utilizando **ngModel** e **FormsModule**

[Link de acesso para o guia](./content/content-05.md)

### Utilizando Reactive Forms

- Captura de dados do formulário através de Reactive Forms Driven, utilizando **ReactiveFormsModule**, **FormBuilder** e **FormGroup**
- Validações reativas
  - Criando validações customizadas usando **ValidatorFn**

[Link de acesso para o guia](./content/content-06.md)

## Inversão de Dependência Compartilhamento de dados entre componente pai e filho

- Inversão de Dependência (DIP)
- Compartilhamento de dados entre componente pai e filho utilizando os decorators **@Input** e **@Output**

[Link de acesso para o guia](./content/content-07.md)

## Autorização e Autenticação no Angular

- Autenticação do usuário no Angular
- Utilização de Subject e Behavior Subject para armazenar o estado do usuário e direcionar para vários Observers
- Guardas de rotas para negar ou permitir o acesso do usuário à rotas criadas
- Implementando o Interceptor para adicionar ao Header o token de autorização nas requisições HTTP  

[Link de acesso para o guia](./content/content-08.md)
