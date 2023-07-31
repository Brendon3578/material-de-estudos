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

### Decorator ViewChild

O `@ViewChild` é decorator que permite que um componente pai **acesse e interaja** com um componente filho **diretamente no próprio template**. É utilizado para obter uma referência a um componente filho dentro de um componente pai.

Usa-se **template variables** com o ViewChild para essa referência, através do hashtag `#`

### Decorator ViewChildren

O `@ViewChildren` permite que um componente pai acesse uma coleção de componentes filhos que correspondem a um determinado seletor de consulta. Ele permite a comunicação e interação com múltiplos componentes filhos ao mesmo tempo
