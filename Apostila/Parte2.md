# Bases de Dados

Bases de dados podem ser entendidas como um conjunto de vetores de mesmo tamanho, em que cada coluna da base de dados é um vetor. No exemplo abaixo é apresentada uma base de dados com três vetores: "Nome", "Idade" e "Mulher", com classes _character_, _numerical_ e _logical_, respectivamente:

| Nome   | Idade | Mulher| 
| -------|:-----:| -----:|
| João   | 27    | FALSE | 
| Ana    | 18    |  TRUE | 
| Luiz   | 21    | FALSE | 
| Carla  | 22    |  TRUE | 
| Pedro  | 35    | FALSE | 

Construindo essa base de dados no R, tem-se:

```{r}
Nome   <- c("João", "Ana", "Luiz", "Carla", "Pedro")
Idade  <- c(27, 18, 21, 22, 35)
Mulher <- c(FALSE, TRUE, FALSE, TRUE, FALSE)

base_de_dados <- data.frame(Nome, Idade, Mulher, stringsAsFactors = FALSE)
print(base_de_dados)
```

Para acessar os antigos vetores criados (agora variáveis da base dados), basta escrever `"nome da base de dados"$"nome da variável"` (sem as aspas). Tal sintaxe se deve ao fato de que é possível abrir e manipular diversas bases de dados no R simultaneamente. Um exemplo para o _data.frame_ criado:

```{r}
print(base_de_dados$Nome)
```

## Interação com a base de dados

Há alguns comandos que permitem interagir visualmente com uma base de dados. Por exemplo, `View` (note a letra maiúscula) mostra a base de dados inteira.

```{r}
View(base_de_dados)
```

A função _head_ apresenta as 6 primeiras linhas da base de dados:

```{r}
head(base_de_dados)
```

A função `tail` apresenta as 6 últimas linhas da base de dados:

```{r}
tail(base_de_dados)
```

A função `str` mostra a _classe_ de cada variável:

```{r}
str(base_de_dados)
```

### Argumentos das funções

Tais funções possuem argumentos que podem ser definidos explicitamente. Por exemplo:

```{r}
head(x = base_de_dados, n = 3)
```

Para reportar os argumentos que uma função possui, basta utilizar a função `args`. Para o exemplo acima:

```{r}
args(head)
```

## Abertura de bases de dados no R

Criar bases de dados dentro do R é bem simples, mas de modo geral são importadas bases de dados já criadas que podem estar em diferentes formatos. Serão apresentados a seguir algumas funções do R de **importação de bases de dados**.

### Biblioteca de pacotes _tidyverse_

Até aqui todos os conteúdos apresentados foram baseados na biblioteca de pacotes nativa do R. Daqui em diante, serão utilizadas biblitecas não-nativas. Tal escolha tem uma origem prática: os comandos comumente utilizados para a abertura, manipulação e apresentação de dados no R são da biblioteca do [_tidyverse_](http://tidyverse.org/).

Vale, portanto, instalar e carregar desde já essa biblioteca:

```{r}
install.packages("tidyverse") 
library(tidyverse)
```
Note que o pacote _tidyverse_ carrega, na verdade, um conjunto de pacotes: _dplyr_, _ggplot2_, _readr_, dentre outros. Os comandos utilizados daqui para frente serão baseados neles.

### Importação de dados com _tidyverse_

Há dois pacotes que armazenam funções de importação dentro do _tidyverse_: o **_readr_** e o **_readxl_**. Os nomes das funções varia de acordo com a extensão do arquivo.

O **_readr_** é reponsável pela leitura de arquivos em formato "retangular" (csv, txt, etc.). Algumas de suas funções são:

- `read_csv()`: arquivos csv (separador: ,)
- `read_csv2()`: arquivos csv (separador: ;)
- `read_tsv()`: arquivos separados por tab
- `read_delim()`: arquivos com delimitador genérico
- `read_fwf()`: arquivos de largura fixa
- `read_table()`: arquivos de tabulação em que as colunas são separadas por espaço em branco
- `read_log()`: arquivos em formato web log (registros de atividade de servidores)

O **_readxl_** é um pacote específico para abrir arquivos em formato .xls ou .xlsx, tipicamente do Microsoft Excel. Sua função é:

- `read_excel()`: arquivos xls ou xlsx

**Detalhe:** todos os pacotes que fazem parte do tidyverse podem ser instalados e carregados diretamente. Por exemplo, o **readxl**:

```{r}
install.packages("readxl") 
library(readxl)
```

Para fins do minicurso, serão utilizadas duas bases de dados como exemplo: 

- Dados da Pesquisa de Informações Básicas Municipais (MUNIC) de 2015 em formato .xls ([link do IBGE](http://www.ibge.gov.br/home/estatistica/economia/perfilmunic/))
- Dados de despesas por natureza da despesa das Finanças Públicas Municipais (FINBRA) em formato .csv ([link do Tesouro Nacional](http://www.tesouro.fazenda.gov.br/pt_PT/contas-anuais))

O uso dos comandos é facilmente transbordável para arquivos com outras extensões. Os dados estão disponíveis no próprio repositório.

### Baixando dados da internet

É possível baixar dados da internet diretamente do R. É bom checar o _working directory_, afinal é para lá que o arquivo baixado irá.

```{r}
getwd()
```

Colocando os links das bases de dados em objetos:

```{r}
url_munic   <- "https://github.com/tavaresrafael/Minicurso_R/raw/master/base_munic_2015.xlsx"
url_finbra  <- "https://github.com/tavaresrafael/Minicurso_R/raw/master/despesa_natureza.csv"
```

Há um comando específico para baixar arquivos da internet: o `download.file`. Há dois argumentos básicos nele: o url e o nome do arquivo de destino:

```{r}
download.file(url_munic, "Base_MUNIC_2015.xlsx")
download.file(url_finbra, "despesa_natureza.csv")
```

Uma vez baixados os dados, é possível importar os arquivos com as funções `read_csv` e `read_excel`:

```{r}
base_munic  <- read_excel("base_munic_2015.xlsx", "Recursos humanos", col_names = T)
base_finbra <- read_csv2("despesa_natureza.csv", quote = "", col_names = T, skip = 3, locale = locale(encoding = "latin1"))
```

## Manipulação de dados com o tidyverse

A manipulação de dados dentro do _tidyverse_ é feita com o pacote _dplyr_. Há cinco funções principais, que podem ser combinadas com diversas funções já existentes no R:

- `mutate()`: adiciona novas variáveis como função das existentes (ou muda a própria variável)
- `select()`: seleciona variáveis (colunas) com base em seus nomes
- `filter()`: filtra observações (linhas) com base em seus valores
- `summarise()`: reduz valores das observações a estatísticas
- `arrange()`: muda a ordem das observações na base

#### Operador pipe: `%>%`

O **pipe** é um operador específico do _tidyverse_, que permite conectar uma sequência de operações. Elé é incrivelmente útil e deixa o script "limpo". Logo abaixo há um exemplo que deixa mais claro o seu papel.

### Manipulação da base de despesas municipais da FINBRA 

Suponha que a ideia da manipulação dos dados de despesas é saber como os municípios se comportam em termos de gastos de pessoal.

Uma breve olhada na base de dados da FINBRA com as funções `View` ou `head` permite notar que ela está bem diferente de uma base de dados "padrão", como mostrado no início dessa segunda parte da apostila. Em particular, é possível ver que para cada munícipio há várias linhas com rubricas de despesa (obviamente os valores não são reais):

| Município  | Conta              | Valor | 
| ---------- |:------------------:| :---: |
| São Paulo  | Despesa Total      | 100   | 
| São Paulo  | Despesa de Pessoal | 80    | 
| Vitória    | Despesa Total      | 30    | 
| Vitória    | Despesa de Pessoal | 20    |

O ideal é resolver o problema por partes. Primeiro, é importante definir a informação considerada relevante. Como exemplo, quer-se manter aqui informações de despesa total e despesa de pessoal por município. Para manter apenas essas rubricas, é preciso "filtrar observações com base em seus valores" ou usar a função `filter` do dplyr:

```{r}
base_finbra <- base_finbra %>% filter(Conta == "Total Despesa" | Conta == "3.1.00.00.00.00 - Pessoal e Encargos Sociais")
```

Para entender o que foi feito:

```{r}
# nova base de dados <- base de dados original %>% manipulação dos dados
```

Segundo, é preciso manter apenas as variáveis úteis. A função do _dplyr_ para tanto é a `select`:

```{r}
base_finbra <- base_finbra %>% select(Cod.IBGE, UF, Conta, Valor)
```

É hora de rearranjar a base de dados de modo a deixá-la com uma observação por município. Espera-se que ela fique assim :

| Município  | Despesa total      | Despesa de pessoal | 
| ---------- |:------------------:| :---: |
| São Paulo  | 100      | 80   | 
| Osasco  | 50 | 30    | 
| Vitória    | 30      | 20    | 
| Vila Velha    | 20 | 15    |

O pacote do _tidyverse_ que resolve esse problema é o _tidyr_. Ele tem duas funções importantes para o problema: `spread` e `gather`, em que uma faz o inverso da outra. No caso em questão, usa-se `spread`:

```{r}
base_finbra <- base_finbra %>% spread(Conta, Valor)
```
Note que só é preciso definir as variáveis que são transformadas pela função.

Uma outra coisa útil de se fazer é renomear as variáveis, de forma a deixá-las com nomes simples (sem espaços, caracteres especiais, etc):

```{r}
base_finbra <- base_finbra %>% rename(cod_ibge = `Cod.IBGE`, uf == UF, despesa_total = `Total Despesa`, despesa_pessoal = `3.1.00.00.00.00 - Pessoal e Encargos Sociais`)
```

Por fim, cria-se uma variável que dá uma ideia de quanto dos gastos dos municípios é voltado para gasto de pessoal:

```{r}
base_finbra <- base_finbra %>% mutate(prop_desp_pessoal = despesa_pessoal/despesa_total)
```

## Utilizando o pipe para fazer tudo de uma vez

Para ter uma ideia de como o **pipe** pode ser útil, o código abaixo refaz a mesma sequência de operações, mas de uma só vez:

```{r}
rm(base_finbra)

base_finbra <- read_csv2("despesa_natureza.csv", col_names = T, skip = 3, locale = locale(encoding = "latin1")) %>%
               filter(Conta == "Total Despesa" | Conta == "3.1.00.00.00.00 - Pessoal e Encargos Sociais") %>%
               select(Cod.IBGE, Conta, Valor) %>%
               spread(Conta, Valor) %>%
               rename(cod_ibge = `Cod.IBGE`, despesa_total = `Total Despesa`, despesa_pessoal = `3.1.00.00.00.00 - Pessoal e Encargos Sociais`) %>%
               mutate(prop_desp_pessoal = despesa_pessoal/despesa_total)
```

Caso se queira saber do gasto de pessoal por funcionário, é preciso juntar as duas bases de dados (Munic e FINBRA). Com o _tidyverse_ também é possível fazê-lo através da família de funções `_join`. Sua sintaxe é:

```{r}
base_nova <- x_join(base_esquerda, base_direita, by = "identificador")
```
O elemento relevante aqui é o "identificador". Para fazer sentido juntar duas bases de dados, é necessário que haja alguma variável em comum. Dentre as principais funções disponíveis, há:

- `left_join()`: Mantém todas as observações da _base_esquerda_
- `right_join()`: Mantém todas as observações da _base_direita_
- `inner_join()`: Mantém todas as observações estejam nas duas bases (simultaneamente)
- `full_join()`: Mantém todas as observações

Para o exemplo, será utilizado o `inner_join`, apenas para garantir que todos os municípios da base tenham toda a informação disponível:

```{r}
base_final <- inner_join(base_munic, base_finbra , by = "cod_ibge")
```

## Arquivos .RData

Arquivos .RData guardam todo o ambiente de trabalho (_working space_) utilizado no R. Diferentemente de programas como o Stata, que salva uma base de dados por vez, o R permite guardar de uma só vez num aquivo .RData várias bases de dados. A função que salva o ambiente de trabalho do R é `save.image`. Salvando o atual ambiente de trabalho, tem-se:

```{r}
save.image("material_minicurso.RData")
```
