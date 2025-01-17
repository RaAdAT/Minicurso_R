# Parte 1 - O básico do R

A ideia dessa primeira parte é comentar sobre os principais elementos fundamentais da linguagem R. Pode-se pensar também como uma apresentação dos principais vocábulos da linguagem.

## Referências para estudo

Antes de iniciar o conteúdo do curso propriamente dito, vale comentar sobre algumas boas referências disponíveis na internet para estudo posterior:

- Livros [R for Data Science](http://r4ds.had.co.nz/) e [Advanced R](http://adv-r.had.co.nz/) : Bons livros para estudo do R. Sugiro começar pelo primeiro.
- [_Cheatsheets_ do RStudio](https://www.rstudio.com/resources/cheatsheets/): Essa página contém resumos com comandos para diversos pacotes/operações do R. É uma boa fonte de consulta rápida. 

## Interface do RStudio

A interface do RStudio é separada em quatro "janelas": 
- _Script_: documento em que se escreve uma rotina de operações no R
- _Console_: scripts simples e resultados
- _Workspace/Environment/History_: objetos/variáveis ativos e histórico de comandos realizados
- _Files/Plots/Packages/Help/Viewer_: utilizado para pesquisar sobre funções, pacotes. Além disso, é possível visualizar figuras

![RStudio](https://github.com/RaAdAT/Minicurso_R/blob/master/RStudio.PNG)

## Alguns atalhos do R

- **Crtl + Enter**:	        executa a(s) linha(s) selecionada(s) do script
- **Crtl + a**: 	          seleciona todas as linhas do script
- **Ctrl + Shift + Enter**: executa todas as linhas do script
- **Crtl + l**:	            limpa o console
- **Esc**: 	                interrompe execução

## Alguns comandos úteis

- `#`:             comentários na linha
- `;`: 	           códigos na mesma linha
- `{}`: 		       códigos em linhas distintas
- `ls()`:   	     mostra as objetos criados
- `rm(X)`: 	       remove o objeto X
- `?X`:            visualiza o help referente ao comando X
- `help(X)`:       igual ao anterior

## O Script

Uma grande vantagem de se utilizar programas como o R, Matlab e Stata para analisar dados é a possibilidade de documentar o "passo-a-passo" de uma sequência de operações realizadas. No R, o arquivo que documenta trabalhos é o _script_, que tem extensão ".R". 

A ideia aqui é que se acompanhe o conteúdo apresentado no minicurso colocando as operações em seu próprio script. Afinal, a rotina de uso do programa será basicamente escrever _scripts_. Tente mantê-lo organizado! 

### Comentários no script

Comentários são peça-chave de um bom script. Com eles é possível comunicar o que está sendo feito no código (mesmo que para você mesma no futuro). Para fazer comentários no _script_ (ou garantir que o R não "lerá" como uma operação a ser feita), basta utilizar `#` no início da linha:

```{r}
# Esta linha contém um comentário
# A próxima linha não contém um comentário 
5
```
### Diretório de trabalho

Outra forma de organizar o script e o trabalho realizado por ele é definir o diretório de trabalho (wd: working directory) que será utilizado pelo R para importar/exportar arquivos. É possível também perguntar ao R qual o diretório atual de trabalho. As funções são bem intuitivas: `getwd` (diretório atual) e `setwd` (definir diretório).

```{r}
getwd()
setwd("")
```
Um ponto importante: **o caminho do diretório deve estar entre aspas**.

## Pacotes no R
O R é fundamentalmente baseado na contribuição de seus usuários. Portanto, é parte da rotina de programação no R instalar e carregar pacotes. Os comandos para instalar e carregar pacotes são, respectivamente:

```{r}
install.packages("dplyr")
library(dplyr)
```
Note que é necessário o uso de aspas para o comando de instalação de pacotes. Quanto ao carregamento de pacotes, o uso de aspas é opcional.

## Tipos de elementos do R

Há dois tipos de elementos do R:
- Objetos
- Funções

As funções são usadas para operar objetos, seja para criar objetos novos ou transformar o objeto original. Tipicamente uma função é escrita seguida de parenteses "( )". Por exemplo:

```{r}
x <- 1
log(x)
```
`x` é um objeto e `log()` é uma função que opera sobre `x`.

## Estruturas de dados

Os dados/informações utilizadas no R podem ser classificadas ou organizadas de acordo com sua (i) dimensionalidade (1d, 2d ou nd) e  (ii) se são homogêneas (todos os elementos são de mesmo tipo) ou heterogêneas (os elementos são de diferentes tipos). A partir desses parâmetros, pode-se classificar cinco tipos principais de estruturas de dados:


|           | Homogêneo | Heterogêneo    | 
| :-------- |:--------: | :------------: |
| **1d**    | Vetor     |   Lista        | 
| **2d**    | Matriz    |  Base de dados | 
| **nd**    | _Array_   |                | 

Neste minicurso, serão discutidos com mais calma os objetos de tipo "Vetor" e "Base de dados". Tal escolha parte do princípio de que os inscritos trabalharão prioritariamente com bases de dados. Como será visto, bases de dados são combinações de vários vetores.

## Operações matemáticas

O R serve como calculadora e realizar operações matemáticas é bem simples.

```{r}
15 + 5 # Soma

15 - 5 # Subtração

15 * 5 # Multiplicação

15 / 5 # Divisão

2 ^ 2 # Potência

16 %/% 5 # Divisão inteira (sem resto):

16 %% 5 # Resto da divisão
```

As operações matemáticas apresentadas acima são funções dentro do R. Para que fique claro, abaixo está a mesma soma, mas agora com a função explícita (entre crases):

```{r}
`+`(15, 5)
```

Para criar uma sequência simples de números no R, basta utilizar o operador `:`. Ele cria um vetor em sua forma mais simples:

```{r}
1:6
```

## Objetos e vetores

Pode até ser divertido utilizar o R como uma calculadora, mas sua principal virtude está em criar todo o tipo de objeto. Dos mais simples aos mais complexos. Talvez sua versão mais simples seja o que conhecemos como "variável" do ensino básico. Isto é:

```{r}
x <- 15
```
Note que é possível utilizar tanto o operador `<-` como `=`:

```{r}
x = 15
```
Note ainda que, diferentemente dos casos anteriores, não apareceu o "resultado" da operação logo após a execução do comando. Para imprimir o valor de uma variável no console basta digitar seu nome:

```{r}
x
```
Em alguns casos, é necessário utilizar a função `print`, que "imprime" o resultado no console:

```{r}
print(x)
```
Criando uma nova variável, é possível realizar operações como as que realizamos anteriormente com números:

```{r}
y <- 5

x + y
x - y
x / y
x * y
```
Novamente, é possível criar objetos que armazenem o resultado dessas operações. Veja os exemplos:

```{r}
v1 <- 42 / 3
v2 <- x + y
v3 <- 1/exp()
v3 <- exp(-(x^2)/2)/sqrt(2*pi)

```

É possível listar os objetos até então criados com a função `ls`:

```{r}
ls()
```

## Classes de vetores

Há três _classes_ principais de vetores:

```{r}
numero <- 10
texto <- "Texto"
logico <- TRUE
```
É possível examinar a classe de cada um dos vetores atômicos criados com a função `class`:

```{r}
class(numero)
class(texto)
class(logico)
```
Como os nomes sugerem, vetores de classe _numeric_ contêm números, vetores de classe _character_ contêm textos e vetores de classe _logical_ contêm valores lógicos (`TRUE` ou `FALSE`).

## Vetores de maiores dimensões

Para criar vetores de dimensão maior que 1, é preciso utilizar a função `c`, abreviado de _combine_:

```{r}
vetor_numerico <- c(42, 7, 999, 3.14)
vetor_texto <- c("sim", "a", '10', "15", "TRUE")
vetor_logico <- c(TRUE, FALSE, F, F, T)
```
Operações matemáticas com vetores de dimensão maior que 1 seguem a mesma lógica de vetores atômicos. As operações são feitas para cada posição dos vetores (ao invés de operações matriciais):

```{r}
x <- c(1, 2)
y <- c(3, 4)
x * y
```

## Combinação de vetores

É possível combinar vetores de forma a criar matrizes com as funções `cbind` e `rowbind`:

```{r}
cbind(x,y)  #  combina vetores pela coluna
rbind(x,y)  #  combina vetores pela linha
```

## Subconjunto de um vetor

Uma parte muito importante da linguagem R é a capacidade de manipular com facilidade subconjuntos das informações disponíveis. Isto é, caso se queira obter apenas alguns elementos de um vetor, é preciso utilizar colchetes `[]` indicando as posições dos elementos. No caso de um vetor, há apenas uma dimensão a se percorrer. Alguns exemplos:

```{r}
x <- c(10, 20, 30, 40)
x[2]
x[3:4]
x[c(2, 4)]
```
É possível também definir um subconjunto a partir de um novo objeto. Por exemplo, criando um vetor lógico "uma_parte_de_x":

```{r}
uma_parte_de_x <- x > 15
class(uma_parte_de_x)
print(uma_parte_de_x)
x[uma_parte_de_x]
```

## Estatísticas descritivas de um vetor

Fazer estatísticas descritivas de um vetor (ou de uma variável numa base de dados) é um processo bem simples. As funções são bem intuitivas (em inglês). Exemplo: meu consumo de litros de café por mês em 2017. Aproveitando, colocarei os nomes dos meses com a função `names`:

```{r}
litros_cafe <- c(4.3, 3.1, 5.3, 5.5, 6.9, 8.3)
names(litros_cafe) <- c("Janeiro", "Fevereiro", "Março", "Abril", "Maio", "Junho")
```
A seguir: soma, media, desvio padrão, variância, mediana, máximo, mínimo e quantil, na respectiva ordem.

```{r}
sum(litros_cafe)
mean(litros_cafe)
sd(litros_cafe)
var(litros_cafe)
median(litros_cafe)
max(litros_cafe)
min(litros_cafe)
quantile(litros_cafe, probs = c(0, 0.2, 0.4, 0.6, .8))
```
Note que a função `quantile` requer um segundo argumento que indica os quantis a serem reportados. Caso não seja indicado o segundo argumento `probs`, serão reportados os seguintes quantis: 0%, 25%, 50%, 75% e 100%.

## Operadores relacionais e lógicos

Há dois tipos de operadores no R. O primeiro deles é o _operador relacional_, que permite verificar se proposições são verdadeiras ou falsas. Há seis operadores:

| Operador       | Símbolo |
| -------------- |:-------:| 
| Igual          | ==      |
| Diferente      | !=      |
| Maior          | >       |
| Maior ou igual | >=      |
| Menor          | <       |
| Menor ou igual | <=      |

Alguns exemplos de seu uso:

```{r}
20 == 10
(2 + 2) != (3 + 1)
5 <= 10
"texto" == "Texto"
"a" > "b"
```
Vale também para objetos:

```{r}
x <- 5
y <- 10
x > y
```

O segundo tipo de operadores é conjunto de operadores lógicos, que servem para combinar ou juntar proposições Há três operadores:

| Operador | Símbolo |
| -------- |:-------:| 
| E        | &       |
| Ou       | \|      |
| Não      | !       |

Alguns exemplos:

```{r}
(4 > 3) & (4 < 3) 
(4 > 3) | (4 < 3)
!(3 < 4)
```
## Cláusulas condicionais

As cláusulas condicionais são fundamentais para a criação de funções e algorítmos no R. Com elas é possível indicar sob que condições se deve fazer determinada operação. Tais condições tipicamente fazem uso de operadores relacionais e lógicos. Ao todo, são três cláusulas: `if`, `else` e `ifelse`. Um exemplo:

```{r}
# Exemplo com x negativo
x <- -1

if (x < 0){
  x <- -x
  print(x)
 } 
 
# Exemplo com x positivo
x <- 1

if (x < 0){
  x <- -x
  print(x)
 } else {
    print("x já é positivo")
}
```
Note que a condição a ser atendida deve estar entre parênteses. A operação a ser realizada deve estar entre chaves "{}". No primeiro exemplo, foi dada apenas uma instrução, que é realizada caso "(x<0)". No segundo exemplo, há uma segunda instrução para quando "(x<0)" não é atendida.

## Repetição de operações: _while_

É útil colocar o computador para realizar tarefas repetitivas, já que isso pode ser feito a um custo bem baixo. Um dos operadores do R para tanto é o `while`. Com ele uma determinada tarefa é realizada enquanto uma determinada condição for satisteita. Por exemplo:

```{r}
i <- 1
while (i <= 10){
  print(i)
   i <- i + 1
}
```

## Repetição de operações: _for_

Outro elemento importante para a criação de funções é o `for` loop. Com ele é possível realizar a tarefa entre chaves "{}" para casos específicos. Por exemplo:

```{r}
for (i in 1:10){
  print(i)
}
```

## Funções

Funções são ferramentas incrivelmente úteis, como foi visto até aqui. Como último tópico dessa primeira parte, vale o aprendizado da criação de funções, com um exemplo bem simples:

```{r}
quadrado <- function(x){
  y <- x ^ 2
  return(y)
}

quadrado(4)
quadrado(10)
```
Note que a função é definida como um objeto, em que o nome do objeto será o nome da função. O argumento da função fica entre parênteses e o corpo da função fica entre chaves. É utlizado o `return` para definir o valor a ser apresentado pelo R. Isto é, a função segue a seguinte estrutura:

```{r}
# nome da função <- function( nome do(s) argumento(s) ) {
#   operação a ser feita ("corpo da função")
#   resultado a ser apresentado
# } 
```
Para um exemplo mais interessante, abaixo está a função densidade de probabilidade de uma variável normal padrão:

```{r}
dens_normal_p <- function(x){
   return(exp(-(x^2)/2)/sqrt(2*pi))
}
```

Nesse caso, a variável `x` tem uma distribuição normal padrão. Note que o código foi encurtado e ainda assim o R ainda entende o que foi escrito. 

É possível verificar o resultado comparando-o com a função nativa do R para a densidade da normal padrão: 

```{r}
dens_normal_p(3)
dnorm(3)
```
