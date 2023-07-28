<h1> Conteúdo 05 </h1>

## Inversão de Dependência (DIP)

Dependency Inversion Principle consiste em depender de abstrações (uma camada a mais na aplicação, **interfaces**) para fazer a conexão entre classes, com ela ocorre um desacoplamento na implementação de classes

## Compartilhar dados entre componente pai e filho

### Compartilhar de pai para filho

- Utiliza-se o decorator `@Input`
- Permite passar dados do componente pai para o componente filho
- Usado para criar uma propriedade em um componente filho
- Podendo ser vinculado a uma propriedade no componente pai, permitindo a comunicação de dados entre componentes

### Compartilhar de filho para pai

- Utiliza-se o decorator `@Output`
- Permite que um componente filho emita eventos para o componente pai
- Criar eventos personalizados no componente filho  que podem ser capturados e processados pelo componente pai. Permitindo a comunicação de eventos de filho para pai.
