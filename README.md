# Questão ponderada: Método Simplex

Farei a resolução do exercício através desse arquivo _markdown_ dado a maior facilidade e flexibilidade para se trabalhar com o _latex_ usando o _vs code_. Tal necessidade foi percebida dado o grande número de iterações necessárias para resolver o exercício.

## Barema do card

Referente ao livro básico "Introdução à Pesquisa Operacional - Frederick S. Hillier; Gerald J. Lieberman", Capítulo 4, na página 165, faça o exercício 4-4-5, itens a) e b).

## Exercício:

$$
Max Z = 5x_1 + 9x_2 + 7x_3
$$

$\textbf{sujeito a:}$

$$
\begin{align*}
&x_1 + 3x_2 + 2x_3 \leq 10 \\
&3x_1 + 4x_2 + 2x_3 \leq 12 \\
&2x_1 + x_2 + 2x_3 \leq 8 \\
&x_1, x_2, x_3 \geq 0
\end{align*}
$$

## Resolução

**1° passo:**
$$
Max Z = 5x_1 + 9x_2 + 7x_3 \rightarrow Z - 5x_1 - 9x_2 - 7x_3 = 0
$$

**2° passo:** Passando as restrições para o formato padrão
$$
\begin{align*}
&x_1 + 3x_2 + 2x_3 + f_1 = 10 \\
&3x_1 + 4x_2 + 2x_3 + f_2 = 12 \\
&2x_1 + x_2 + 2x_3 + f_3 = 8 \\
&x_1, x_2, x_3, f_1, f_2, f_3 \geq 0
\end{align*}
$$

**Tabela - 1° iteração**

|         | $x_1$ | $x_2$ | $x_3$ | $f_1$ |  $f_2$ |  $f_3$ |   $b$  |
|---------|-------|-------|-------|-------|--------|--------|--------|
|  Z      |   -5  |  -9   |  -7   |   0   |    0   |    0   |    0   |
|  $f_1$  |    1  |   3   |   2   |   1   |    0   |    0   |   10   |
|  $f_2$  |    3  |   4   |   2   |   0   |    1   |    0   |   12   |
|  $f_3$  |    2  |   1   |   2   |   0   |    0   |    1   |    8   |

Na linha dos valores de Z, deve-se encontrar o menor valor para definir qual a coluna pivô da iteração, sendo essa a coluna da variável $x_2$ com o valor $-9$.

A partir desse valor, deve-se calcular a razão entre a coluna $b$ e a respectiva coluna pivô para encontrar o menor valor e definir a linha pivô, portanto:

$$
\begin{align*}
f_1 \rightarrow \frac{10}{3} \\
f_2 \rightarrow \frac{12}{4} = 3 \\
f_3 \rightarrow \frac{8}{1} = 8 \\
\end{align*}
$$

O menor valor é o da restrição $f_2$, sendo assim pode-se concluir que o elemento pivô é o valor 4 localizado na interseção entre a coluna pivô e a linha pivô.

A partir disso, deve-se dividir a linha pelo pivô, logo temos:

|         | $x_1$ | $x_2$ | $x_3$ | $f_1$ |  $f_2$ |  $f_3$ |   $b$  |
|---------|-------|-------|-------|-------|--------|--------|--------|
|  $f_2$  |  3/4  |  4/4  | 2/4   |   0   |  1/4   |    0   |  12/4  |

Resultando em:

|         | $x_1$ | $x_2$ | $x_3$ | $f_1$ |  $f_2$ |  $f_3$ |   $b$  |
|---------|-------|-------|-------|-------|--------|--------|--------|
|  Z      |   -5  |  -9   |  -7   |   0   |    0   |    0   |    0   |
|  $f_1$  |    1  |   3   |   2   |   1   |    0   |    0   |   10   |
|  $f_2$  |  3/4  |   1   | 1/2   |   0   |  1/4   |    0   |   3    |
|  $f_3$  |    2  |   1   |   2   |   0   |    0   |    1   |    8   |


Com isso, tal nova linha deve ser usada para para, através de uma soma, zerar os valores da coluna pivô. Para zerar o valor $-9$ da coluna $x_2$ na linha Z, deve-se multiplicar a linha $f_2$ por 9 e depois somar os valores das duas linhas. O mesmo procedimento deve ser seguido para as linhas $f_1$ e $f_3$, sendo assim:

$Z = Z + (f_2 \cdot 9)$:

|         | $x_1$ | $x_2$ | $x_3$ | $f_1$ |  $f_2$ |  $f_3$ |   $b$  |
|---------|-------|-------|-------|-------|--------|--------|--------|
|  Z      |  7/4  |   0   | -5/2  |   0   |  9/4   |    0   |   27   |
|  $f_1$  |    1  |   3   |   2   |   1   |    0   |    0   |   10   |
|  $f_2$  |  3/4  |   1   | 1/2   |   0   |  1/4   |    0   |   3    |
|  $f_3$  |    2  |   1   |   2   |   0   |    0   |    1   |    8   |

<br>

$f_1 = f_1 - (f_2 \cdot 3)$:

|         | $x_1$ | $x_2$ | $x_3$ | $f_1$ |  $f_2$ |  $f_3$ |   $b$  |
|---------|-------|-------|-------|-------|--------|--------|--------|
|  Z      |  7/4  |   0   | -5/2  |   0   |  9/4   |    0   |   27   |
|  $f_1$  | -5/4  |   0   |  1/2  |   1   |  -3/4  |    0   |   1    |
|  $f_2$  |  3/4  |   1   | 1/2   |   0   |  1/4   |    0   |   3    |
|  $f_3$  |    2  |   1   |   2   |   0   |    0   |    1   |    8   |

<br>

$f_3 = f_3 - f_2$:

|         | $x_1$ | $x_2$ | $x_3$ | $f_1$ |  $f_2$ |  $f_3$ |   $b$  |
|---------|-------|-------|-------|-------|--------|--------|--------|
|  Z      |  7/4  |   0   | -5/2  |   0   |  9/4   |    0   |   27   |
|  $f_1$  | -5/4  |   0   |  1/2  |   1   |  -3/4  |    0   |   1    |
|  $f_2$  |  3/4  |   1   | 1/2   |   0   |  1/4   |    0   |   3    |
|  $f_3$  |  5/4  |   0   |  3/2  |   0   |  -1/4  |    1   |   5    |

**Tabela - 2° iteração**

|         | $x_1$ | $x_2$ | $x_3$ | $f_1$ |  $f_2$ |  $f_3$ |   $b$  |
|---------|-------|-------|-------|-------|--------|--------|--------|
|  Z      |  7/4  |   0   | -5/2  |   0   |  9/4   |    0   |   27   |
|  $f_1$  | -5/4  |   0   |  1/2  |   1   |  -3/4  |    0   |   1    |
|  $f_2$  |  3/4  |   1   | 1/2   |   0   |  1/4   |    0   |   3    |
|  $f_3$  |  5/4  |   0   |  3/2  |   0   |  -1/4  |    1   |   5    |

Menor valor da tabela é -5/2 na coluna $x_3$. Novamente calculando as razões, temos:

$$
\begin{align*}
f_1 \rightarrow \frac{1}{\frac{1}{2}} = 2 \\
f_2 \rightarrow \frac{3}{\frac{1}{2}} = 6 \\
f_3 \rightarrow \frac{5}{\frac{1}{2}} = \frac{10}{3} \\
\end{align*}
$$

A menor variável fica em $f_1$, logo o elemento pivô é 1/2. Assim, deve-se multiplicar o valor de sua linha por 2 para que o elemento pivô seja 1. Logo:

|         | $x_1$ | $x_2$ | $x_3$ | $f_1$ |  $f_2$ |  $f_3$ |   $b$  |
|---------|-------|-------|-------|-------|--------|--------|--------|
|  Z      |  7/4  |   0   | -5/2  |   0   |  9/4   |    0   |   27   |
|  $f_1$  | -5/2  |   0   |  1    |   2   |  -3/2  |    0   |   2    |
|  $f_2$  |  3/4  |   1   | 1/2   |   0   |  1/4   |    0   |   3    |
|  $f_3$  |  5/4  |   0   |  3/2  |   0   |  -1/4  |    1   |   5    |

Com isso, o mesmo processo para zerar os valores da coluna pivô pode ser realizado:

$Z = Z + (f_1 \cdot \frac{5}{2})$:

|         | $x_1$ | $x_2$ | $x_3$ | $f_1$ |  $f_2$ |  $f_3$ |   $b$  |
|---------|-------|-------|-------|-------|--------|--------|--------|
|  Z      | -9/2  |   0   |   0   |   5   |  -3/2  |    0   |   32   |
|  $f_1$  | -5/2  |   0   |   1   |   2   |  -3/2  |    0   |   2    |
|  $f_2$  |  3/4  |   1   | 1/2   |   0   |  1/4   |    0   |   3    |
|  $f_3$  |  5/4  |   0   |  3/2  |   0   |  -1/4  |    1   |   5    |

<br>

$f_2 = f_2 - (f_1 / 2)$:

|         | $x_1$ | $x_2$ | $x_3$ | $f_1$ |  $f_2$ |  $f_3$ |   $b$  |
|---------|-------|-------|-------|-------|--------|--------|--------|
|  Z      | -9/2  |   0   |   0   |   5   |  -3/2  |    0   |   32   |
|  $f_1$  | -5/2  |   0   |   1   |   2   |  -3/2  |    0   |   2    |
|  $f_2$  |   2   |   1   |   0   |  -1   |    1   |    0   |   2    |
|  $f_3$  |  5/4  |   0   |  3/2  |   0   |  -1/4  |    1   |   5    |

<br>

$f_3 = f_3 - (f_1 \cdot \frac{3}{2})$:

|         | $x_1$ | $x_2$ | $x_3$ | $f_1$ |  $f_2$ |  $f_3$ |   $b$  |
|---------|-------|-------|-------|-------|--------|--------|--------|
|  Z      | -9/2  |   0   |   0   |   5   |  -3/2  |    0   |   32   |
|  $f_1$  | -5/2  |   0   |   1   |   2   |  -3/2  |    0   |   2    |
|  $f_2$  |   2   |   1   |   0   |  -1   |    1   |    0   |   2    |
|  $f_3$  |   5   |   0   |   0   |  -3   |    2   |    1   |   2    |

**Tabela - 3° iteração**

|         | $x_1$ | $x_2$ | $x_3$ | $f_1$ |  $f_2$ |  $f_3$ |   $b$  |
|---------|-------|-------|-------|-------|--------|--------|--------|
|  Z      | -9/2  |   0   |   0   |   5   |  -3/2  |    0   |   32   |
|  $f_1$  | -5/2  |   0   |   1   |   2   |  -3/2  |    0   |   2    |
|  $f_2$  |   2   |   1   |   0   |  -1   |    1   |    0   |   2    |
|  $f_3$  |   5   |   0   |   0   |  -3   |    2   |    1   |   2    |

Menor valor da tabela é -9/2 na coluna $x_1$. Novamente calculando as razões, temos:

$$
\begin{align*}
f_1 \rightarrow \frac{2}{-\frac{5}{2}} \\
f_2 \rightarrow \frac{2}{2} = 1 \\
f_3 \rightarrow \frac{2}{5} \\
\end{align*}
$$

A menor variável fica em $f_3$, logo o elemento pivô é 5. Assim, deve-se dividir o valor de sua linha por 5 para que o elemento pivô seja 1. Logo:

|         | $x_1$ | $x_2$ | $x_3$ | $f_1$ |  $f_2$ |  $f_3$ |   $b$  |
|---------|-------|-------|-------|-------|--------|--------|--------|
|  Z      | -9/2  |   0   |   0   |   5   |  -3/2  |    0   |   32   |
|  $f_1$  | -5/2  |   0   |   1   |   2   |  -3/2  |    0   |   2    |
|  $f_2$  |   2   |   1   |   0   |  -1   |    1   |    0   |   2    |
|  $f_3$  |   1   |   0   |   0   | -3/5  |   2/5  |   1/5  |   2/5  |

Com isso, o mesmo processo para zerar os valores da coluna pivô pode ser realizado:

$Z = Z + (f_3 \cdot \frac{9}{2})$:

|         | $x_1$ | $x_2$ | $x_3$ | $f_1$ |  $f_2$ |  $f_3$ |   $b$  |
|---------|-------|-------|-------|-------|--------|--------|--------|
|  Z      |   0   |   0   |   0   | 23/10 |  3/10  |  9/10  |  169/5 |
|  $f_1$  | -5/2  |   0   |   1   |   2   |  -3/2  |    0   |   2    |
|  $f_2$  |   2   |   1   |   0   |  -1   |    1   |    0   |   2    |
|  $f_3$  |   1   |   0   |   0   | -3/5  |   2/5  |   1/5  |   2/5  |

<br>

$f_1 = f_1 + (f_3 \cdot \frac{5}{2})$:

|         | $x_1$ | $x_2$ | $x_3$ | $f_1$ |  $f_2$ |  $f_3$ |   $b$  |
|---------|-------|-------|-------|-------|--------|--------|--------|
|  Z      |   0   |   0   |   0   | 23/10 |  3/10  |  9/10  |  169/5 |
|  $f_1$  |   0   |   0   |   1   |  1/2  |  -1/2  |  1/2   |   3    |
|  $f_2$  |   2   |   1   |   0   |  -1   |    1   |    0   |   2    |
|  $f_3$  |   1   |   0   |   0   | -3/5  |   2/5  |   1/5  |   2/5  |

<br>

$f_2 = f_2 - (f_3 \cdot 2)$:

|         | $x_1$ | $x_2$ | $x_3$ | $f_1$ |  $f_2$ |  $f_3$ |   $b$  |
|---------|-------|-------|-------|-------|--------|--------|--------|
|  Z      |   0   |   0   |   0   | 23/10 |  3/10  |  9/10  |  169/5 |
|  $f_1$  |   0   |   0   |   1   |  1/2  |  -1/2  |  1/2   |   3    |
|  $f_2$  |   0   |   1   |   0   |  1/5  |   1/5  |  -2/5  |  6/5   |
|  $f_3$  |   1   |   0   |   0   | -3/5  |   2/5  |   1/5  |   2/5  |

**Tabela - 4° iteração**

|         | $x_1$ | $x_2$ | $x_3$ | $f_1$ |  $f_2$ |  $f_3$ |   $b$  |
|---------|-------|-------|-------|-------|--------|--------|--------|
|  Z      |   0   |   0   |   0   | 23/10 |  3/10  |  9/10  |  169/5 |
|  $x_3$  |   0   |   0   |   1   |  1/2  |  -1/2  |  1/2   |   3    |
|  $x_2$  |   0   |   1   |   0   |  1/5  |   1/5  |  -2/5  |  6/5   |
|  $x_1$  |   1   |   0   |   0   | -3/5  |   2/5  |   1/5  |   2/5  |

Não há mais números negativos na linha Z, logo o resultado ótimo foi alcançado com os seguintes valores:

$$
\begin{align*}
x_1 = \frac{2}{5} \\
x_2 = \frac{6}{5} \\
x_3 = 3 \\
f_1 = 0 \\
f_2 = 0 \\
f_3 = 0 \\
\end{align*}
$$

Logo o valor ótimo para Z é:

$$
Z = 5 \cdot \frac{2}{5} + 9 \cdot \frac{6}{5} + 7 \cdot 3
$$

$$
Z = 33,8
$$
