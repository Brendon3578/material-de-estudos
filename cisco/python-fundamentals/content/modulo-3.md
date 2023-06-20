<h1> Fazendo cálculos com Python e Tomada de decisão com Python </h1>

<h2>Sumário</h2>

## Operadores básicos

Uma expressão é uma combinação de valores (ou variáveis, operadores, chamadas para funções) que resulta em um determinado valor 1 `+` 2.Operadores são símbolos especiais ou palavras-chave que são capazes de operar nos valores e realizar operações (matemáticas) o operador `*` multiplica dois valores: x `*` y.

Operadores aritméticos em Python: `+ - * /`, (atenção: a divisão sempre retorna um número float), `%` (módulo ‒ divide o operando esquerdo pelo operando direito e retorna o resto da operação, por exemplo , 5 % 2 = 1), `**` (exponenciação ‒ operando esquerdo elevado à potência do operando direito 2 ** 3 = 8), `//` (divisão inteira ou *floor division* (divisão de piso) ‒ retorna um número resultante da divisão, mas arredondado para o número inteiro mais próximo 3 // 2.0 = 1.0)

Nota: os dados e os operadores, quando conectados, formam expressões.

### Cálculo com números floats

```py
print(2 ** 3)
print(2 ** 3.)
# OUTPUT >> 8
# OUTPUT >> 8.0
```

Com a divisão, o retorno sempre será um número float, mas é possível usar o operador `//` para a **divisão arredondada** (ou divisão inteira ou **divisão de piso**/*floor division*) que retorna um número inteiro quando ambos operandos são inteiro. Exemplo:

```py
print(6 // 3)
print(6 // 3.)
# OUTPUT >> 2
# OUTPUT >> 2.0
# lembrando que: 6 / 4 é 1.5
print(6 // 4)
print(6. // 4)
# OUTPUT >> 1
# OUTPUT >> 1.0
```

### Operador binário e unário

Um operador unário é um operador com apenas um operando -1 ou +3. Já um operador binário é um operador com dois operandos 4 + 5 ou 12 % 5.

### Hierarquia dos operadores

Alguns operadores agem antes de outros - a **hierarquia de prioridades**:

- O operador de exponenciação `**`  tem a prioridade mais alta.
- Os operadores unários `+` e `-`, exemplo : `4 ** -1` que resulta em 0.25
- Operadores de : `*`, `/` e `%`
- Operadores com a prioridade mais baixa: `+` e `-`

Porém subexpressões entre parênteses são calculadas primeiro. Por exemplo: `15 - 1*(5* (1 + 2)) = 0`.

O operador de exponenciação usa a associação do lado direito 2 `**` 2 `**` 3 = 256.

## Tomada de decisão

Os operadores de comparação (também conhecidos como **relacionais**) são usados para **comparar** valores. Retornando `True` para verdadeiro e `False` para falso

- `==` compara se dois operandos são iguais: `1 == 2` - retorna False
- `!=` compara se dois operandos são diferentes: `1 != 2` - retorna True
- `>` compara se o operando do lado esquerdo é **maior** que o do lado direito: `1 > 2` - retorna False
- `>=` compara se o operando do lado esquerdo é **maior** ou igual que o do lado direito: `1 >= 2` - retorna False
- `<` compara se o operando do lado esquerdo é **menor** que o do lado direito: `1 < 2` - retorna False
- `<=` compara se o operando do lado esquerdo é **menor ou igual** que o do lado direito: `2 <= 2` - retorna True

Já quando você deseja executar algum bloco de código quando uma determinada condição for atendida, você pode usar uma declaração **condicional**, utilizando as palavras reservadas `if` (se) e `else` (se não) ou até `elif` (se não se):

```py
idade = 18
 
if idade >= 18: # condição
    print("Você ja é maior de idade")  # Executado se a condição for True.
```

Utilizando `if`, `else` e `elif`:

```py
x = 10
 
if x == 10: # True
    print("x == 10")
if x > 15: # False
    print("x > 15")
elif x > 10: # False
    print("x > 10")
elif x > 5: # True
    print("x > 5")
else:
    print("senão não será executado")
```

## Loops

Para fazer laços de repetições, isto é, um bloco de código que vai ser usado varias vezes, no Python existem duas formas de fazer isso, há dois tipos de loops no Python: `while` e `for`:

o loop while executa uma declaração ou um conjunto de declarações desde que uma condição booleana especificada seja verdadeira, por exemplo:

```py
# Exemplo 1
while True:
    print("Preso em um loop infinito.")
 
# Exemplo 2
contador = 5
while contador > 2:
    print(contador)
    contador -= 1
```

o loop `for` junto com a palavra reservada `in` executa um conjunto de instruções muitas vezes; é usado para **iterar** em uma sequência (por exemplo, uma lista, um dicionário, uma tupla ou um conjunto) ou outros objetos iteráveis (por exemplo, sequências de caracteres). Você pode usar o loop `for` para fazer iterações em uma sequência de números usando a função `range` integrada. Veja os exemplos abaixo:

```py
# Exemplo 1, pra cada letra na palavra "Python" será executado o código abaixo
palavra = "Python"
for letra in palavra:
    print(letra, end="*")
 
# Exemplo 2, verificar se o número em um intervalo de 1 a 10 é par
for i in range(1, 10):
    if i % 2 == 0:
        print(i)
```

É possível usar as instruções `break` e `continue` para alterar o fluxo normal de um loop:

Você usa break para sair de um loop, por exemplo:

```py
palavra = "OpenEDG Python Institute"
for letra in palavra:
    if letra == "P":
        break
    print(letra, end="")
# OUTPUT >> "OpenEDG "
```

Você usa `continue` para ignorar a iteração atual e continuar com a próxima iteração, por exemplo:

```py
palavra = "pyxpyxpyx"
for letra in palavra:
    if letra == "x":
        continue
    print(letra, end="")
# OUTPUT >> pypypy
```

Os loops `while` e `for` também podem ter uma cláusula `else` em Python. A cláusula else é executada depois que o loop termina sua execução, desde que não tenha sido finalizada por break, por exemplo:

```py
n = 0
 
while n != 3:
    print(n)
    n += 1
else:
    print(n, "else")

# OUTPUT >>0
# OUTPUT >>1
# OUTPUT >>2
# OUTPUT >>3 else
 
for i in range(0, 3):
    print(i)
else:
    print(i, "else")
# OUTPUT >> 0
# OUTPUT >> 1
# OUTPUT >> 2
# OUTPUT >> 2 else
```

### Função range

A função `range()` gera uma sequência de números. Ele aceita números inteiros e retorna objetos de intervalo. A sintaxe de range(): range(start, stop, step), em que:

- **start** é um parâmetro opcional que especifica o número inicial da sequência (0 por padrão)
- **stop** é um parâmetro opcional que especifica o fim da sequência gerada (não está incluída),
- **step** é um parâmetro opcional que especifica a diferença entre os números na sequência (1 por padrão).

```py
for i in range(3):
    print(i, end=" ")
# OUTPUT >> 0 1 2
for i in range(6, 1, -2):
    print(i, end=" ")
# OUTPUT >> 6, 4, 2
```

## Operador Lógico

O Python é compatível com os seguintes operadores lógicos:

- **and** se ambos os operandos forem verdadeiros, a condição é verdadeira (True and True) é True,
- **or** se qualquer um dos operandos for verdadeiro, a condição é verdadeira (True or False) é True,
- **not** retorna falso se o resultado for verdadeiro e retorna verdadeiro se o resultado for falso not True for False.

## Operadores bit a bit (bitwise)

É possível usar operadores bit a bit para **manipular** bits únicos de dados.

```py
x = 15 # que é **0000 1111** em binário
y = 16 # que é **0001 0000** em binário
# & faz um bit a bit (and)
x & y # resulta 0 que é 0000 0000 em binário
# | faz um bit a bit (or)
x | y # resulta 31 que é 0001 1111 em binário
# ˜ faz um bit a bit (not)
˜ x # resulta 240, que é 1111 0000 em binário
# ^ faz um bit a bit (xor)
x ^ y # resulta 31, que é 0001 1111 em binário
# >> faz um deslocamento à direita bit a bit
y >> 1 # resulta 8, que é 0000 1000 em binário,
## << faz um turno à esquerda bit a bit
y << 3 # resulta 128 que é 1000 0000 em binário,
```
