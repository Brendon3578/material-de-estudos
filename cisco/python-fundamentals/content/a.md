## Métodos da String

No Python existem métodos (que podemos entender por enquanto que são funções que um tipo de dado possui) que podem ser usados para trabalhar com Strings:

Para utilizar o método da String, escrevemos o nome da variavel que armazena a string, seguida do ponto `.` e o nome do método após isso

- `find` para encontrar uma substring dentro de uma string e retornar a posição onde ela foi encontrada
  - O método find retorna -1 quando a ocorrência não é encontrada
- `replace` para substituir ocorrências de substrings dentro de uma string.
- `split` separamos uma string em uma lista de várias strings através de um separador passado como argumento.
- `upper` retorna uma cópia da string com todas as letras minúsculas convertidas em maiúsculas.
- `lower` retorna uma cópia da string com todas as letras maiúsculas convertidas em minúsculas.

```py
mensagem = 'string no Python'
print(mensagem.find('Python'))
# OUTPUT >> 10

print(mensagem.find('Java'))
# OUTPUT >> -1

mensagem = "Quero aprender Elixir, procuro saber sobre os fundamentos de Elixir."
nova_mensagem = mensagem.replace('Java', 'Python')
print(nova_mensagem)
# OUTPUT >> Quero aprender Python, procuro saber sobre os fundamentos de Python
mensagem = 'Estou aprendendo Python'
mensagem_picotada = mensagem.split(' ')
print(mensagem_picotada)
# OUTPUT >> ['Estou', 'aprendendo', 'Python']

mensagem = 'eu gosto de Python'
mensagem_caixa_alta = mensagem.upper()
print(mensagem_caixa_alta)
# OUTPUT >> EU GOSTO DE PYTHON

mensagem_caixa_baixa = mensagem_caixa_alta.lower()
print(mensagem_caixa_baixa)
# OUTPUT >> eu gosto de python
```
