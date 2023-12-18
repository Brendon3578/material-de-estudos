<h1> Modulo 2 - Programando em Python e Tipos de Dados </h1>

<h2>Sumário</h2>

- [Começando com um `Hello World!`](#começando-com-um-hello-world)
- [Comentário](#comentário)
- [O que é uma função](#o-que-é-uma-função)
- [Comportamento da função `print`](#comportamento-da-função-print)
  - [Argumentos Posicionais](#argumentos-posicionais)
  - [Argumentos de palavra-chave](#argumentos-de-palavra-chave)
    - [`end` para alterar o caractere do texto impresso](#end-para-alterar-o-caractere-do-texto-impresso)
    - [`sep` para adicionar um separador entre os argumentos](#sep-para-adicionar-um-separador-entre-os-argumentos)
- [Tipos de Dados](#tipos-de-dados)
  - [Números](#números)
    - [Inteiros](#inteiros)
    - [Floats](#floats)
  - [Strings (cadeia de caracteres)](#strings-cadeia-de-caracteres)
    - [Concatenando Strings](#concatenando-strings)
  - [Valores booleanos](#valores-booleanos)
  - [Como saber os tipos de dados](#como-saber-os-tipos-de-dados)
- [Bibliografia](#bibliografia)

## Começando com um `Hello World!`

Para as operações de I/O, Input e Output (Entrada e Saída de dados), podemos usar `input` e `print` respectivamente.

```py
input("Digite o seu nome: ")

print("Hello World!")
```

Podemos dizer que o `input` têm as seguintes características:

- é uma função (veremos isso mais tarde) que o próprio python provê para a entrada de dados
- recebe um argumento que está dentro dos parênteses
- esse argumento é uma *String* (que significa linha de texto ou **cadeia de caracteres**)
- esse argumento será a pergunta que o terminal mostrará para o usuário escrever algo

Porém, precisamos armazenar o valor de um input em uma variável, ou seja, atribuir o seu valor em uma informação para que possamos então, ter uma informação para que possamos trabalhar

```py
# A variável "Nome" recebe o valor que vai ser digitado pelo usuário,
nome = input("Digite o seu nome")

# O nome digitado pelo usuário será exibido em tela (no terminal)
print(nome)
```

## Comentário

Em toda as linguagens de programação, um recurso muito utilizado é os comentários, no qual é possível comentar o que determinado código faz, no python usa-se o símbolo de Cerquilha ou Hashtag: `#`, como visto nos blocos de comando anteriores, para comentar um trecho de código.

Em certas IDEs existem atalhos que podem fazer uma determinada linha ser comentada.

## O que é uma função

Uma função pode ser entendida como um "bloco de código" que resolve um problema específico, que possui um nome associado e que pode ser chamado várias vezes quando é necessário

Uma função pode:

- **causar algum efeito**, por exemplo, enviar um texto no terminal, perguntar ao usuário que digite algo, toque um som, exiba uma notificação em tela;
- **avaliar e transformar um valor**, no qual vai receber um dado (que no contexto das funções, é chamado de argumento) e transformar esse dado e **retorná-lo** como resultado da função, sendo esse dado transformado, por exemplo calcular a raiz quadrada de um número.

É possível escrever suas próprias funções ou usar as que o próprio Python provê para você utilizar, como `input`, `print` e `len` para saber o número de itens que está em uma lista

## Comportamento da função `print`

Essa função pode receber vários argumentos, veja seus comportamentos a seguir:

### Argumentos Posicionais

`print` recebe os argumentos de forma posicional, ou seja o significado do argumento é determinado pela sua posição (por exemplo, o segundo argumento será gerado após o primeiro, e não o contrário).

```py
print("Meu nome é", "Python.")
# OUTPUT >> Meu nome é Python.
print("Python.", "Meu nome é")
# OUTPUT >> Python. Meu nome é
```

### Argumentos de palavra-chave

O Python oferece outro mecanismo para alterar o comportamento da função print, utilizando palavras reservadas para mudar o texto que será exibido em tela. Veja alguns deles:

#### `end` para alterar o caractere do texto impresso

Por padrão, no **final** de cada texto impresso na tela pela função print, o Python pula uma linha no terminal, colocando no final da String um caractere de `\n` (NewLine). Podemos modificar esse comportamento definindo qual o último caractere que será impresso:

```py
print("Estou programando em ")
print("Python.")
# OUTPUT >> Estou programando em
# OUTPUT >> Python.

print("Estou programando em ", end="")
print("Python.")
# OUTPUT >> Estou programando em Python.

print("Estou programando em ", end="...")
print("Python.")
# OUTPUT >> Estou programando em ...Python.
```

#### `sep` para adicionar um separador entre os argumentos

```py
print("Meu", "nome", "é", "Monty", "Python.", sep="-")
# OUTPUT >> Meu-nome-é-Monty-Python.
```

É possível até combinar os dois argumentos de palavras chaves juntos.

```py
print("Sou", "Ultron", sep="_", end="*")
print("um", "robô.", sep="*", end="*\n")
# OUTPUT >> Sou_Ultron*um*robô.*
```

Vale lembrar, que esses dois argumentos `end` e `sep` deve sempre ser declarados no final da função print.

## Tipos de Dados

Um valor, sem nenhuma variável atribuída à ele, é chamado de **Literal**

Um literal é um valor expresso como ele mesmo e não como o valor de uma variável ou o resultado de uma expressão

Podemos entender que ele é um valor que nunca vai ser mudado durante sua execução, **um valor fixo**, pois é a variável que muda, não uma literal

Dentro de qualquer linguagem de programação, há algo que chamamos de **Tipos de dados**, sendo algo que diferencia o tipo de informação que o computador irá trabalhar.

### Números

Os números manipulados por computadores modernos podem ser desses dois tipos:

#### Inteiros

São aqueles que são desprovidos da parte fracionária, podendo ser positivos (pode ou não vim acompanhado do sinal de +) ou negativos

```py
numero_inteiro = 1
numero_inteiro_negativo = -3141519
print(numero_inteiro, numero_inteiro_negativo, +5)
# OUTPUT >> 1 -3141519 5
```

No Python há duas outras formas de representar números, sendo **octais** e **hexadecimais**

Se um número inteiro for precedido por um prefixo `0O` ou `0o` (zero-o), ele será tratado como um valor **octal**. Isso significa que o número deve conter dígitos retirados apenas do intervalo [0..7].

Se um número precede de `0x` ou `OX` (zero-x) ele é um **hexadecimal**.

```py
# 0o123 é um número octal com um valor (decimal) igual a 83.
print(0o123)
# OUTPUT >> 83

# 0xFF é um número hexadecimal com um valor (decimal) igual a 291
print(0xFF)
# OUTPUT >> 255
```

#### Floats

São números de ponto flutuante (**float**ing point), que contêm (ou são capazes de conter) a parte fracionária.

Deixo [aqui](https://pt.stackoverflow.com/questions/219211/qual-a-forma-correta-de-usar-os-tipos-float-double-e-decimal) um artigo sobre como um computador entende a **precisão** de números que usam **pontos flutuante**.

No nosso idioma utiliza-se a vírgula `,` para representar esses números fracionários, já em linguagens de programação utiliza-se o ponto, `.`

```py
print(2.5, -0.4)

# Você pode omitir zero quando for o único dígito antes ou depois da vírgula.
print(.5)
# OUTPUT >> 0.5
print(4.)
# OUTPUT >> 4.0
```

Quando você precisa usar números muito grandes ou muito pequenos, pode-se usar a notação científica, usando a letra `e`

A velocidade da luz (em metros por segundo) escrita diretamente é: `300000000`, já nos livros de física é provavelmente escrito `3 x 10^8`.

Diz: *Três vezes dez elevado a oito*

No Python, podemos escrever do seguinte modo: `3E8`. A letra `E` ou `e` ( vem da palavra expoente) é um registro simplificado da frase: "vezes dez à potência de". No qual:

- o **expoente** (o valor após o E) tem que ser um número inteiro;
- a **base** (o valor na frente do E) pode ser um número inteiro ou um valor flutuante.

```py
# Exemplo: constante de Plank (6,62607 x 10^-34)
print(6.62607E-34)
# OUTPUT >> 6.62607e-34

# O Python por padrão sempre escolhe a forma mais econômica de apresentação do número:
print(0.0000000000000000000001)
# OUTPUT >> 1e-22
```

### Strings (cadeia de caracteres)

Strings são usadas quando você precisa processar texto (como nomes, endereços, romances, etc.), não números que são usados em cálculos.

No python as strings são delimitadas pelas aspas duplas `" "`.

Porém surge  so seguinte problema: como escrever uma String, que dentro contêm outras aspas?

Há duas soluções:

- Utilizar o **caractere de escape:** `\` (barra invertida) que aponta que o próximo caractere terá um comportamento diferente, e colocar em seguida as apas `"`: `\"`.
  - Nota: chama-se **sequência de escape** o conjunto de adicionar o **caractere de escape** com outro **carácter qualquer**, exemplo de sequências de escape: `\n`, `\t` `\"`
- Ou usar um apóstrofo `'` em vez de aspas duplas

```py
print("Assim disse Sócrates: \"só sei que nada sei\"")
# OUTPUT >> Assim disse Sócrates: "só sei que nada sei"

print('Assim disse Irineu: "Irineu,você não sabe nem eu"')
# OUTPUT >> Assim disse Irineu: "Irineu,você não sabe nem eu"
```

Nota: a regra de utilizar o caractere de escape para representar aspas dentro de aspas, aplica-se aos apóstrofos:

```py
print('I\'m not in danger. I\'m the danger.')
# OUTPUT >> I'm not in Danger. I'm the Danger.
```

#### Concatenando Strings

As vezes é necessário juntar diversas informações e Textos em uma única variável, podemos fazer isso concatenando Strings, isto é, juntar elas em uma só, usa-se o operador de `+`:

```py
curso = "Fundamentos de Python"
plataforma = "Github"

o_que_estou_aprendendo = "Estou aprendendo "+ curso +" na plataforma do "+ plataforma
print(o_que_estou_aprendendo)
# OUTPUT >> Estou aprendendo Fundamentos de Python na plataforma do Github
```

### Valores booleanos

Booleano, vem do sobrenome de George Boole (1815-1864), autor da obra fundamental, The Laws of Thought, que contém a definição de álgebra booleana ‒ uma parte da álgebra que faz uso de apenas dois valores distintos: 0 ou 1, `False` ou `True` respectivamente no Python.

Na programação eles são usados para representar um valor abstrato - a veracidade, a verdade. Ou algo é verdadeiro ou é falso

```py
hoje_vai_chover = True
print(hoje_vai_chover)
```

### Como saber os tipos de dados

Uma ferramenta que pode ajudar em saber qual é o tipo de dado de uma variável é utilizar a função `type` que o próprio Python oferece para tal verificação

```py
print(type(1), type(0XFF), type(0o77))
# OUTPUT >> <class 'int'> <class 'int'> <class 'int'>
print(type(3.141519))
# OUTPUT <class 'float'>
print(type(True), type(False))
# OUTPUT <class 'bool'> <class 'bool'>
```

## Bibliografia

<https://pt.wikipedia.org/wiki/Python/>
<https://pt.stackoverflow.com/questions/114473/o-que-%C3%A9-um-literal/>
<https://www.devmedia.com.br/tipos-de-dados-em-python-string/40669#concatenacao/>
