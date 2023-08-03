<h1> Operadores do RXJS </h1>

<h2> Sumário </h2>

- [Piping](#piping)
- [Operadores de utilidade](#operadores-de-utilidade)
  - [`tap` - observar side effects](#tap---observar-side-effects)
- [Operadores para criar Observables](#operadores-para-criar-observables)
  - [`from` - criar observable a partir de uma lista](#from---criar-observable-a-partir-de-uma-lista)
  - [`of` - criar observable a partir de uma informação](#of---criar-observable-a-partir-de-uma-informação)
  - [(FUNÇÃO) `interval` - Emitir números em sequência de um tempo X](#função-interval---emitir-números-em-sequência-de-um-tempo-x)
  - [(FUNÇÃO) `timer` - Usado para criar temporizador](#função-timer---usado-para-criar-temporizador)
- [Operadores para filtrar informações](#operadores-para-filtrar-informações)
  - [`filter` - filtrar as informações passadas](#filter---filtrar-as-informações-passadas)
  - [`map` - Transformar os valores emitidos](#map---transformar-os-valores-emitidos)
  - [`distinctUntilChanged` - Obter resultado apenas se for diferente do anterior](#distinctuntilchanged---obter-resultado-apenas-se-for-diferente-do-anterior)
  - [`switchMap` - Emitir os valores apenas para o Observable mais recente](#switchmap---emitir-os-valores-apenas-para-o-observable-mais-recente)
  - [`debounceTime` - Emitir para o Observable apenas se não hover outra chamada de emissão](#debouncetime---emitir-para-o-observable-apenas-se-não-hover-outra-chamada-de-emissão)
  - [`take` - Controlar a quantidade de valores que são emitidos para o Observable](#take---controlar-a-quantidade-de-valores-que-são-emitidos-para-o-observable)
  - [`takeUntil` - Emitir valores até outro Observable emitir um valor](#takeuntil---emitir-valores-até-outro-observable-emitir-um-valor)
- [Operadores para captura de error](#operadores-para-captura-de-error)
  - [`catchError` - Capturar erros do Observable](#catcherror---capturar-erros-do-observable)
- [Exemplo prático](#exemplo-prático)
- [Operadores de combinações](#operadores-de-combinações)
  - [`forkJoin` combinar a última emissão de 1 ou mais Observables](#forkjoin-combinar-a-última-emissão-de-1-ou-mais-observables)

## Piping

Utilizar o método `.pipe()` dos Observables é útil para combinar operadores de RXJS, sendo executados sequencialmente

## Operadores de utilidade

### `tap` - observar side effects

É utilizado para capturar side-effects (efeito colateral) do Observable e monitorar seus valores

## Operadores para criar Observables

### `from` - criar observable a partir de uma lista

Utilizado para criar um Observable Através de uma lista iterável (array)

### `of` - criar observable a partir de uma informação

Utilizado para criar um Observable a partir da informação que será passada pra frente

### (FUNÇÃO) `interval` - Emitir números em sequência de um tempo X

- Ele é utilizado para criar números em sequência de um determinado timeframe que você define em milissegundos

### (FUNÇÃO) `timer` - Usado para criar temporizador

## Operadores para filtrar informações

### `filter` - filtrar as informações passadas

É usado para filtrar os dados que são passados pelo Observable

Exemplo de utilização do `filter` para verificar números pares

```ts
import { from, tap, filter } from 'rxjs';

numbers$ = from([1, 2, 3, 4, 5, 6, 7, 8]);

ngOnInit(): void {
  this.numbers$
    .pipe(
      // verificar os números pares
      filter((number) => number % 2 == 0),
      tap(console.log)
    )
    .subscribe();
}
```

### `map` - Transformar os valores emitidos

Usado para transformar os valores emitidos em um observable, e retorna os valores retornados como um novo Observable

Exemplo de utilização do `map` para transformar cada valor e retornar se é par (*even*) ou não

```ts
import { from, map, tap } from 'rxjs';

numbers$ = from([1, 2, 3, 4, 5, 6, 7, 8]);
ngOnInit(): void {
  this.numbers$
    .pipe(
      map((number) => {
        return number % 2 == 0
          ? { number: number, isEven: true }
          : { number: number, isEven: false };
      }),
      tap(console.log)
    )
    .subscribe();
}
/* OUTPUT:
{number: 1, isEven: false}
{number: 2, isEven: true}
{number: 3, isEven: false}
{number: 4, isEven: true}...
*/
```

### `distinctUntilChanged` - Obter resultado apenas se for diferente do anterior

Usado para obter o resultado do Observable apenas se não for igual ao resultado anterior

### `switchMap` - Emitir os valores apenas para o Observable mais recente

- É muito utilizado quando um novo valor é projetado para o Observable e pode descartar o valor projetado anteriormente
- Podemos dizer que é o contrário do `mergeMap` que executa vários Observables ao mesmo tempo
- Usado para evitar problemas de **memory leak**, e em cenários cenários como componentes de `TypeAhead` no qual você não precisa focar em dar uma resposta para a requisição anterior quando há uma nova **requisição**.

> Trocar (switch) para um novo Observable

### `debounceTime` - Emitir para o Observable apenas se não hover outra chamada de emissão

- Usado para emitir um valor para o do Observable depois de um período de tempo e SE não ocorrer entre esse período outra emissão de evento  
- Utilizado para dar *delay* na execução do Observable
- Cenários comuns como **input** do Reactive Forms que envolvam chamadas de API

### `take` - Controlar a quantidade de valores que são emitidos para o Observable

- Utilizado para controlar a quantidade de valores que serão emitidos para os Observables
- Quando o valor de take é alcançado, o Observable é automaticamente `completed`
- Exemplo utilizando o  `take` para pegar apenas os 4 primeiros do `interval`

```ts
import { take, interval, pipe} from 'rxjs';

// dentro de uma classe
numbersTake$ = interval(1000);

// dentro de um método
takeOperator() {
  const emitter$ = this.numbersTake$.pipe(take(4));

  emitter$.subscribe((val) =>
    console.log(`Emitted from take operator - ${val}`)
  );
}
```

### `takeUntil` - Emitir valores até outro Observable emitir um valor

- Utilizado para emitir valores ATÉ o Observable que é passado como argumento emitir um valor
- Muito utilizado para fazer unsubscribe de Observables quando haver o método `ngOnDestroy` de um componente Angular
- Exemplo de utilização do `takeUntil` utilizando um `timer` do RXJS

```ts
import { interval, pipe, takeUntil} from 'rxjs';

// dentro de uma classe
timer$ = timer(6000);
numbersTake$ = interval(1000);

takeUntilOperator() {
  const emitter$ = this.numbersTake$.pipe(takeUntil(this.timer$));

  emitter$.subscribe((val) =>
    console.log(`Emitted from takeUntil operator - ${val}`)
  );
}
```

## Operadores para captura de error

### `catchError` - Capturar erros do Observable

- Utilizado para capturar o erro do observable e não parar o fluxo do Observable, retornando um novo observable ou lançar um erro
- Geralmente dentro da função desse operador é retornado um novo Observable junto com o `of`

Exemplo de utilização para a captura de um erro

```ts
switchMap((query) => {
  return ajax
    .getJSON<any>(`https://api.github.com/users/${query}`)
    .pipe(
      catchError((err) => {
        console.log('Ocorreu uma falha na requisição!');
        return of(err);
      })
    );
})
```

## Exemplo prático

Exemplo de utilização de operadores usando a API do github e o Ajax para requisições. No exemplo é utilizado:

- `pipe` para combinar vários **operadores do RXJS**
- `debounceTime` para dar o delay quando o usuário digitar o número de usuário no controle  de `username` do formulário reativo `formGithub`
- `filter` para apenas permitir requisições se o input com whitespace (espaço em branco)
- `tap` para mostrar no console o valor que está sendo passado pelo Observable (depois do filtro)
- `distinctUntilChanged` para permitir a execução do Observable apenas se for um valor diferente do que foi passado anteriormente
- `switchMap` para executar a requisição através do `ajax`, de forma performática

```ts
import { debounceTime, distinctUntilChanged, from, map, switchMap, tap, filter, } from 'rxjs';

this.formGithub.controls.username.valueChanges
  .pipe(
    debounceTime(1000),
    filter((string) => string?.trim() != ''),
    tap(console.log),
    distinctUntilChanged(),
    switchMap((query) => {
      return ajax.getJSON<any>(`https://api.github.com/users/${query}`);
    })
  )
  .subscribe((response) => {
    this.user = {
      name: response?.name,
      exists: true,
      avatar_url: response?.avatar_url,
    };
    console.log(response);
  });
```

O `ajax.getJson` retorna um Observable, podendo então ser utilizado com o método `pipe` depois de sua invocação e em seguida ser usado outros operadores do RXJS

```ts
//...
  switchMap((query) => {
    return ajax.getJSON<any>(`https://api.github.com/users/${query}`).pipe(
      switchMap(user => ajax.getJSON(user.repos_url))
    );
  })
//...
```

## Operadores de combinações

### `forkJoin` combinar a última emissão de 1 ou mais Observables

- É utilizado para combinar a última emissão de vários observables que são emitidos em um tempo parecido
- Exemplo combinando vários observables e usando a desestruturação para pegar cada valor único emitido

```ts
import { of, forkJoin } from 'rxjs';

// dentro de uma classe
observable1$ = of('value 1');
observable2$ = of('value 2');
observable3$ = of('value 3');

forkJoinOperator() {
  const result$ = forkJoin([
    this.observable1$,
    this.observable2$,
    this.observable3$,
  ]);
  result$.subscribe((values) => {
    const [firstValue, secondValue, thirdValue] = values;
    console.log(`First Value: ${firstValue}`);
    console.log(`Second Value: ${secondValue}`);
    console.log(`Third Value: ${thirdValue}`);
  });
}
```
