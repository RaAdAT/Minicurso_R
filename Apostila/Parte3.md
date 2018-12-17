# Estatísticas descritivas no R

Antes de iniciar o conteúdo dessa parte da terceira parte do minicurso, vale o aprendizado de como se carrega todo o material utilizado numa sessão anterior do R. A função para tanto é a `load`:

```{r}
load("myWorkspace.RData")
```

## Criação de estatísticas descritivas com _tidyverse_

O _tidyverse_ permite através do _dyplyr_ a criação de diversas estatísticas descritivas. Junto da função `group_by`, é possível, por exemplo, gerar estatísticas das variáveis da base criada na [Parte 2](https://github.com/RaAdAT/Minicurso_R/blob/master/Apostila/Parte2.Rmd) por UF. Abaixo estão alguns exemplos:

### Tabela com a proporção média de gastos com pessoal UF:

```{r}
prop_pessoal_uf <- base_final %>% group_by(uf) %>% summarise(prop_pessoal = mean(prop_desp_pessoal, na.rm = TRUE))
```

### Tabela com a soma de gastos de pessoal por UF:

```{r}
total_pessoal_uf <- base_final %>% group_by(uf) %>% summarise(total_pessoal = mean(despesa_pessoal, na.rm = TRUE))
```

### Tabela com a proporção mediana de gastos com pessoal por UF:

```{r}
prop_pessoal_med_uf <- base_final %>% group_by(uf) %>% summarise(prop_med_pessoal = median(prop_desp_pessoal, na.rm = TRUE))
```

### Tabela com várias estatísticas descritivas:

```{r}
estat_desc_uf <- base_final %>% group_by(uf) %>% summarise(prop_pessoal = mean(prop_desp_pessoal, na.rm = TRUE),
                                                           med_pessoal = median(prop_desp_pessoal, na.rm = TRUE),
                                                           min_pessoal = min(prop_desp_pessoal, na.rm = TRUE),
                                                           max_pessoal = max(prop_desp_pessoal, na.rm = TRUE),
                                                           total_pessoal = sum(despesa_pessoal, na.rm = TRUE))
```

## Gráficos com o _tidyverse_

O pacote do _tidyverse_ para a criação de gráficos é o _ggplot2_. Alguns exemplos:

```{r}
ggplot(data = base_final) +
  geom_histogram(mapping = aes(x = prop_desp_pessoal*100, y = ..density..), binwidth = 0.5) +
  geom_density(mapping = aes(x = prop_desp_pessoal*100), color = "blue") +
  labs(x = "Proporção de gastos com pessoal (%)", y = "Densidade")

ggplot(data = base_final) +
  geom_histogram(mapping = aes(x = prop_desp_pessoal*100, y = ..density..), binwidth = 0.5) +
  geom_density(mapping = aes(x = prop_desp_pessoal*100), color = "blue") +
  labs(x = "Proporção de gastos com pessoal (%)", y = "Densidade")

ggplot(data = estat_desc_uf) +
  geom_boxplot(mapping = aes(x = uf, y = prop_pessoal*100)) +
  coord_cartesian(ylim = c(0, 100)) +
  labs(x = NULL, y = "Proporção de gastos com pessoal (%)")

ggplot(base_final, aes(x=total_func_pref, y=prop_desp_pessoal*100)) + 
  geom_point()+
  geom_smooth(method=lm, se=FALSE) +
  coord_cartesian(ylim = c(0, 100), xlim = c(0, 5000)) +
  labs(x = "Número de funcionários da prefeitura", y = "Proporção de gastos com pessoal (%)")

```




