---
layout: default
title: "Tópico 01 – Visualização de Dados"
parent: "Aulas Computacionais"
nav_order: 1
---
# Tópico 01 – Visualização de Dados [<img src="https://raw.githubusercontent.com/urielmoreirasilva/EST/main/aulas/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados/images/colag_logo.svg" style="float: right; vertical-align: middle; width: 42px; height: 42px;">](https://colab.research.google.com/github/urielmoreirasilva/EST/blob/main/aulas/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados.ipynb) [<img src="https://raw.githubusercontent.com/urielmoreirasilva/EST/main/aulas/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados/images/github_logo.svg" style="float: right; margin-right: 12px; vertical-align: middle; width: 36px; height: 36px;">](https://github.com/urielmoreirasilva/EST/blob/main/aulas/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados.ipynb)

Um pouco sobre como representar dados de maneira visual!

### Resultados Esperados
1. Aprender algumas ferramentas simples para exploração de dados.
1. Aprender os conceitos básicos de visualização de dados.
1. Aprender a manipular os DataFrames de `pandas` para produzir gráficos elementares.  

### Referências
- [CIT, Capítulo 7](https://inferentialthinking.com/)

Material adaptado do [DSC10 (UCSD)](https://dsc10.com/) por [Flavio Figueiredo (DCC-UFMG)](https://flaviovdf.io/fcd/) e [Uriel Silva (DEST-UFMG)](https://urielmoreirasilva.github.io)


```python
# Importando Pandas e Numpy
import pandas as pd
import numpy as np

# Importando Matplotlib
import matplotlib.pyplot as plt
plt.style.use('ggplot')

# Importando alguns outros módulos para nos ajudar nas visualizações
from IPython.display import HTML, display, IFrame
```

## Visualização de dados

### Por que visualizar?

- Os computadores são melhores que os humanos para processar números, mas os humanos (em geral) são melhores para identificar padrões visuais.
- As visualizações nos permitem compreender rapidamente um grande volume de dados, facilitando a identificação de tendências e a comunicação de resultados.
- Existem _vários_ tipos de visualizações – neste tópico, veremos gráficos de dispersão, gráficos de linhas, gráficos de barras e histogramas.
- A escolha "certa" do método de visualização depende sempre do tipo de dado em questão!

## Prelúdio: um pouco de terminologia

### Indivíduos e variáveis

<center><img src="https://raw.githubusercontent.com/urielmoreirasilva/EST/main/aulas/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados/images/ind-var.png" width = "90%"></center>

- <span style="color:#6d9eeb"><b>Indivíduo (linha):</b></span> Pessoa/lugar/coisa para a qual os dados são registrados. Também chamado de **observação**, ou _data point_.

- <span style="color:#ff9900"><b>Variável (coluna):</b></span> Característica observada para cada indivíduo. Também chamado de **recurso**, ou _feature_.

### Tipos de variáveis

Existem dois tipos principais de variáveis:

- **Numéricas**: Variáveis tais que seus valores permitam operações de aritmética básica.
- **Categóricas**: Variáveis cujos valores se enquadram em _categorias_, que podem ou não ter alguma _ordem_ entre elas.

### Exemplos de variáveis ​​numéricas

- Conjunto de dados: Salários dos jogadores da NBA. 🏀
    - Indivíduo: um jogador da NBA.
    - Variável: seu salário.

- Conjunto de dados: O rendimento no _box office_ de vários filmes. 🎬💰
    - Indivíduo: um filme.
    - Variável: o rendimento do filme no _box office_.

- Conjunto de dados: Doses de reforço de vacinas administradas por dia. 💉
    - Indivíduo: data de cada dia onde foram administradas as vacinas.
    - Variável: número de doses de reforço administradas em cada data.

### Exemplos de variáveis ​​​​categóricas

- Conjunto de dados: Gêneros de filmes. 🎬
    - Indivíduo: um filme.
    - Variável: seu gênero.

- Conjunto de dados: Códigos de Endereço Postais (CEPs). 🏠
    - Indivíduo: um habitante de uma cidade, ou região.
    - Variável: seu CEP.

Nota: apesar de serem reportados como números, os CEPs na verdade são categóricos (operações aritméticas básicas não têm sentido quando aplicadas aos CEPs).

- Conjunto de dados: Nível de experiência anterior em programação para alunos de Ciência de Dados 🧑‍🎓.
    - Indivíduo: um aluno.
    - Variável: seu nível de experiência anterior em programação, por ex.: "nenhum", "baixo", "médio" ou "alto".

Nota: essa é uma variável categórica _ordenada_!

### Exercício ✅

Qual destas **não** é uma variável numérica? Preencha a célula de texto abaixo com a resposta correspondente.

**A.** Gasto de combustível em quilômetros por litro.

**B.** Número de semestres de um curso na UFMG.

**C.** Período do curso na UFMG (primeiro, quinto, sétimo, etc).

**D.** Número de uma conta bancária.

**E.** Mais de uma das acima não são variáveis numéricas.

> ...

### Tipos de visualizações

O _tipo de visualização_ que criamos depende dos _tipos de variáveis_ ​​que estamos visualizando.

- **Gráfico de dispersão**: numérica vs. numérica.
- **Gráfico de linhas**: numérica "sequencial" (por exemplo no tempo) vs. numérica.
- **Gráfico de barras**: categórica vs. numérica.
- **Histograma**: numérica.

Veremos todos os esses tipos de gráficos nesse e no próximo tópico.

## Gráficos de dispersão

### Exemplo: os 50 atores de maior bilheteria

|Coluna |Conteúdo|
|----------|------------|
`'Actor'`|Nome do ator
`'Total Gross'`| Receita total bruta no _box office_, em milhões de dólares, de todos os filmes do ator
`'Number of Movies'`| O número total de filmes em que o ator esteve
`'Average per Movie'`| O total de receita bruta dividido pelo número total de filmes
`'#1 Movie'`| O filme de maior bilheteria em que o ator já esteve
`'Gross'`| Receita bruta de bilheteria interna, em milhões de dólares, do filme de maior bilheteria do ator


```python
actors = pd.read_csv('https://raw.githubusercontent.com/urielmoreirasilva/EST/main/aulas/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados/data/actors.csv').set_index('Actor')
actors
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Gross</th>
      <th>Number of Movies</th>
      <th>Average per Movie</th>
      <th>#1 Movie</th>
      <th>Gross</th>
    </tr>
    <tr>
      <th>Actor</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Harrison Ford</th>
      <td>4871.7</td>
      <td>41</td>
      <td>118.8</td>
      <td>Star Wars: The Force Awakens</td>
      <td>936.7</td>
    </tr>
    <tr>
      <th>Samuel L. Jackson</th>
      <td>4772.8</td>
      <td>69</td>
      <td>69.2</td>
      <td>The Avengers</td>
      <td>623.4</td>
    </tr>
    <tr>
      <th>Morgan Freeman</th>
      <td>4468.3</td>
      <td>61</td>
      <td>73.3</td>
      <td>The Dark Knight</td>
      <td>534.9</td>
    </tr>
    <tr>
      <th>Tom Hanks</th>
      <td>4340.8</td>
      <td>44</td>
      <td>98.7</td>
      <td>Toy Story 3</td>
      <td>415.0</td>
    </tr>
    <tr>
      <th>Robert Downey, Jr.</th>
      <td>3947.3</td>
      <td>53</td>
      <td>74.5</td>
      <td>The Avengers</td>
      <td>623.4</td>
    </tr>
    <tr>
      <th>Eddie Murphy</th>
      <td>3810.4</td>
      <td>38</td>
      <td>100.3</td>
      <td>Shrek 2</td>
      <td>441.2</td>
    </tr>
    <tr>
      <th>Tom Cruise</th>
      <td>3587.2</td>
      <td>36</td>
      <td>99.6</td>
      <td>War of the Worlds</td>
      <td>234.3</td>
    </tr>
    <tr>
      <th>Johnny Depp</th>
      <td>3368.6</td>
      <td>45</td>
      <td>74.9</td>
      <td>Dead Man's Chest</td>
      <td>423.3</td>
    </tr>
    <tr>
      <th>Michael Caine</th>
      <td>3351.5</td>
      <td>58</td>
      <td>57.8</td>
      <td>The Dark Knight</td>
      <td>534.9</td>
    </tr>
    <tr>
      <th>Scarlett Johansson</th>
      <td>3341.2</td>
      <td>37</td>
      <td>90.3</td>
      <td>The Avengers</td>
      <td>623.4</td>
    </tr>
    <tr>
      <th>Gary Oldman</th>
      <td>3294.0</td>
      <td>38</td>
      <td>86.7</td>
      <td>The Dark Knight</td>
      <td>534.9</td>
    </tr>
    <tr>
      <th>Robin Williams</th>
      <td>3279.3</td>
      <td>49</td>
      <td>66.9</td>
      <td>Night at the Museum</td>
      <td>250.9</td>
    </tr>
    <tr>
      <th>Bruce Willis</th>
      <td>3189.4</td>
      <td>60</td>
      <td>53.2</td>
      <td>Sixth Sense</td>
      <td>293.5</td>
    </tr>
    <tr>
      <th>Stellan Skarsgard</th>
      <td>3175.0</td>
      <td>43</td>
      <td>73.8</td>
      <td>The Avengers</td>
      <td>623.4</td>
    </tr>
    <tr>
      <th>Anthony Daniels</th>
      <td>3162.9</td>
      <td>7</td>
      <td>451.8</td>
      <td>Star Wars: The Force Awakens</td>
      <td>936.7</td>
    </tr>
    <tr>
      <th>Ian McKellen</th>
      <td>3150.4</td>
      <td>31</td>
      <td>101.6</td>
      <td>Return of the King</td>
      <td>377.8</td>
    </tr>
    <tr>
      <th>Will Smith</th>
      <td>3149.1</td>
      <td>24</td>
      <td>131.2</td>
      <td>Independence Day</td>
      <td>306.2</td>
    </tr>
    <tr>
      <th>Stanley Tucci</th>
      <td>3123.9</td>
      <td>50</td>
      <td>62.5</td>
      <td>Catching Fire</td>
      <td>424.7</td>
    </tr>
    <tr>
      <th>Matt Damon</th>
      <td>3107.3</td>
      <td>39</td>
      <td>79.7</td>
      <td>The Martian</td>
      <td>228.4</td>
    </tr>
    <tr>
      <th>Robert DeNiro</th>
      <td>3081.3</td>
      <td>79</td>
      <td>39.0</td>
      <td>Meet the Fockers</td>
      <td>279.3</td>
    </tr>
    <tr>
      <th>Cameron Diaz</th>
      <td>3031.7</td>
      <td>34</td>
      <td>89.2</td>
      <td>Shrek 2</td>
      <td>441.2</td>
    </tr>
    <tr>
      <th>Liam Neeson</th>
      <td>2942.7</td>
      <td>63</td>
      <td>46.7</td>
      <td>The Phantom Menace</td>
      <td>474.5</td>
    </tr>
    <tr>
      <th>Andy Serkis</th>
      <td>2890.6</td>
      <td>23</td>
      <td>125.7</td>
      <td>Star Wars: The Force Awakens</td>
      <td>936.7</td>
    </tr>
    <tr>
      <th>Don Cheadle</th>
      <td>2885.4</td>
      <td>34</td>
      <td>84.9</td>
      <td>Avengers: Age of Ultron</td>
      <td>459.0</td>
    </tr>
    <tr>
      <th>Ben Stiller</th>
      <td>2827.0</td>
      <td>37</td>
      <td>76.4</td>
      <td>Meet the Fockers</td>
      <td>279.3</td>
    </tr>
    <tr>
      <th>Helena Bonham Carter</th>
      <td>2822.0</td>
      <td>36</td>
      <td>78.4</td>
      <td>Harry Potter / Deathly Hallows (P2)</td>
      <td>381.0</td>
    </tr>
    <tr>
      <th>Orlando Bloom</th>
      <td>2815.8</td>
      <td>17</td>
      <td>165.6</td>
      <td>Dead Man's Chest</td>
      <td>423.3</td>
    </tr>
    <tr>
      <th>Woody Harrelson</th>
      <td>2815.8</td>
      <td>50</td>
      <td>56.3</td>
      <td>Catching Fire</td>
      <td>424.7</td>
    </tr>
    <tr>
      <th>Cate Blanchett</th>
      <td>2802.6</td>
      <td>39</td>
      <td>71.9</td>
      <td>Return of the King</td>
      <td>377.8</td>
    </tr>
    <tr>
      <th>Julia Roberts</th>
      <td>2735.3</td>
      <td>42</td>
      <td>65.1</td>
      <td>Ocean's Eleven</td>
      <td>183.4</td>
    </tr>
    <tr>
      <th>Elizabeth Banks</th>
      <td>2726.3</td>
      <td>35</td>
      <td>77.9</td>
      <td>Catching Fire</td>
      <td>424.7</td>
    </tr>
    <tr>
      <th>Ralph Fiennes</th>
      <td>2715.3</td>
      <td>36</td>
      <td>75.4</td>
      <td>Harry Potter / Deathly Hallows (P2)</td>
      <td>381.0</td>
    </tr>
    <tr>
      <th>Emma Watson</th>
      <td>2681.9</td>
      <td>17</td>
      <td>157.8</td>
      <td>Harry Potter / Deathly Hallows (P2)</td>
      <td>381.0</td>
    </tr>
    <tr>
      <th>Tommy Lee Jones</th>
      <td>2681.3</td>
      <td>46</td>
      <td>58.3</td>
      <td>Men in Black</td>
      <td>250.7</td>
    </tr>
    <tr>
      <th>Brad Pitt</th>
      <td>2680.9</td>
      <td>40</td>
      <td>67.0</td>
      <td>World War Z</td>
      <td>202.4</td>
    </tr>
    <tr>
      <th>Adam Sandler</th>
      <td>2661.0</td>
      <td>32</td>
      <td>83.2</td>
      <td>Hotel Transylvania 2</td>
      <td>169.7</td>
    </tr>
    <tr>
      <th>Daniel Radcliffe</th>
      <td>2634.4</td>
      <td>17</td>
      <td>155.0</td>
      <td>Harry Potter / Deathly Hallows (P2)</td>
      <td>381.0</td>
    </tr>
    <tr>
      <th>Jonah Hill</th>
      <td>2605.1</td>
      <td>29</td>
      <td>89.8</td>
      <td>The LEGO Movie</td>
      <td>257.8</td>
    </tr>
    <tr>
      <th>Owen Wilson</th>
      <td>2602.3</td>
      <td>39</td>
      <td>66.7</td>
      <td>Night at the Museum</td>
      <td>250.9</td>
    </tr>
    <tr>
      <th>Idris Elba</th>
      <td>2580.6</td>
      <td>26</td>
      <td>99.3</td>
      <td>Avengers: Age of Ultron</td>
      <td>459.0</td>
    </tr>
    <tr>
      <th>Bradley Cooper</th>
      <td>2557.7</td>
      <td>25</td>
      <td>102.3</td>
      <td>American Sniper</td>
      <td>350.1</td>
    </tr>
    <tr>
      <th>Mark Wahlberg</th>
      <td>2549.8</td>
      <td>36</td>
      <td>70.8</td>
      <td>Transformers 4</td>
      <td>245.4</td>
    </tr>
    <tr>
      <th>Jim Carrey</th>
      <td>2545.2</td>
      <td>27</td>
      <td>94.3</td>
      <td>The Grinch</td>
      <td>260.0</td>
    </tr>
    <tr>
      <th>Dustin Hoffman</th>
      <td>2522.1</td>
      <td>43</td>
      <td>58.7</td>
      <td>Meet the Fockers</td>
      <td>279.3</td>
    </tr>
    <tr>
      <th>Leonardo DiCaprio</th>
      <td>2518.3</td>
      <td>25</td>
      <td>100.7</td>
      <td>Titanic</td>
      <td>658.7</td>
    </tr>
    <tr>
      <th>Jeremy Renner</th>
      <td>2500.3</td>
      <td>21</td>
      <td>119.1</td>
      <td>The Avengers</td>
      <td>623.4</td>
    </tr>
    <tr>
      <th>Philip Seymour Hoffman</th>
      <td>2463.7</td>
      <td>40</td>
      <td>61.6</td>
      <td>Catching Fire</td>
      <td>424.7</td>
    </tr>
    <tr>
      <th>Sandra Bullock</th>
      <td>2462.6</td>
      <td>35</td>
      <td>70.4</td>
      <td>Minions</td>
      <td>336.0</td>
    </tr>
    <tr>
      <th>Chris Evans</th>
      <td>2457.8</td>
      <td>23</td>
      <td>106.9</td>
      <td>The Avengers</td>
      <td>623.4</td>
    </tr>
    <tr>
      <th>Anne Hathaway</th>
      <td>2416.5</td>
      <td>25</td>
      <td>96.7</td>
      <td>The Dark Knight Rises</td>
      <td>448.1</td>
    </tr>
  </tbody>
</table>
</div>



### Visualizando a relação entre duas variáveis

#### Qual é a relação entre `'Number of Movies'` e `'Total Gross'`?

Uma das maneiras de visualizar essa relação é através de um **diagrama de dispersão**, também conhecido como **gráfico de dispersão**:


```python
actors.plot(kind = 'scatter', x = 'Number of Movies', y = 'Total Gross');
```


    
![png](T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_27_0.png)
    


- Os diagramas de dispersão (_scatter plots_) consistem de um arranjo dos valores de cada uma das duas colunas selecionadas de um `DataFrame` em pontos nas ordenadas $x$ e $y$ de um diagrama Cartesiano.
- Cada um dos pontos do diagrama de dispersão representam uma linha no nosso DataFrame. 
- Os diagramas de dispersão são muito úteis para visualizar a relação entre duas variáveis _​​numéricas_!

- Para criar um gráfico de dispersão a partir de um DataFrame `df` genérico com duas colunas numéricas `'x_column_for_horizontal'` e `'y_column_for_vertical'`, invocamos
```
df.plot(
    kind = 'scatter', 
    x = x_column_for_horizontal, 
    y = y_column_for_vertical
)
```

Nota: em geral coloamos um ponto e vírgula após uma chamada para `.plot`, para ocultar a saída de texto que acompanha a execução desse método.


```python
# O texto que aparece após a execução da célula abaixo não aparece quando colocamos ";" após chamarmos o método `.plot`
actors.plot(kind = 'scatter', x = 'Number of Movies', y = 'Total Gross')
```




    <Axes: xlabel='Number of Movies', ylabel='Total Gross'>




    
![png](T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_30_1.png)
    


Analisando o diagrama de dispersão acima, vemos uma associação positiva, mas bem dispersa, entre o número de filmes de um ator e o total de suas receitas no box office.

#### Qual é a relação entre `'Number of Movies'` e `'Average per Movie'`?


```python
actors.plot(kind = 'scatter', x = 'Number of Movies', y = 'Average per Movie');
```


    
![png](T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_33_0.png)
    


No gráfico acima, vamos associação _negativa_ entre as duas variáveis, e um _valor discrepante_ (_outlier_).

#### Qual ator esteve em 60 ou mais filmes?


```python
actors[actors.get('Number of Movies') >= 60]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Gross</th>
      <th>Number of Movies</th>
      <th>Average per Movie</th>
      <th>#1 Movie</th>
      <th>Gross</th>
    </tr>
    <tr>
      <th>Actor</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Samuel L. Jackson</th>
      <td>4772.8</td>
      <td>69</td>
      <td>69.2</td>
      <td>The Avengers</td>
      <td>623.4</td>
    </tr>
    <tr>
      <th>Morgan Freeman</th>
      <td>4468.3</td>
      <td>61</td>
      <td>73.3</td>
      <td>The Dark Knight</td>
      <td>534.9</td>
    </tr>
    <tr>
      <th>Bruce Willis</th>
      <td>3189.4</td>
      <td>60</td>
      <td>53.2</td>
      <td>Sixth Sense</td>
      <td>293.5</td>
    </tr>
    <tr>
      <th>Robert DeNiro</th>
      <td>3081.3</td>
      <td>79</td>
      <td>39.0</td>
      <td>Meet the Fockers</td>
      <td>279.3</td>
    </tr>
    <tr>
      <th>Liam Neeson</th>
      <td>2942.7</td>
      <td>63</td>
      <td>46.7</td>
      <td>The Phantom Menace</td>
      <td>474.5</td>
    </tr>
  </tbody>
</table>
</div>



#### E quem é o outlier no último diagrama?

Podemos identificar o outlier no diagrama anterior buscando pelo único ator que fez menos que 10 filmes.


```python
actors[actors.get('Number of Movies') < 10]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Gross</th>
      <th>Number of Movies</th>
      <th>Average per Movie</th>
      <th>#1 Movie</th>
      <th>Gross</th>
    </tr>
    <tr>
      <th>Actor</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Anthony Daniels</th>
      <td>3162.9</td>
      <td>7</td>
      <td>451.8</td>
      <td>Star Wars: The Force Awakens</td>
      <td>936.7</td>
    </tr>
  </tbody>
</table>
</div>



A média de receita no box office desse ator é bem alta!

#### Anthony Daniels

<center><img src='https://raw.githubusercontent.com/urielmoreirasilva/EST/main/aulas/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados/images/c3po.png' width=200></center>

## Gráficos de linha 📉

### Exemplo: agregando filmes por ano

|Coluna| Conteúdo|
|------|-----------|
`'Year'`| Ano
`'Total Gross in Billions'`| Total bruto de bilheteria doméstica, em bilhões de dólares, de todos os filmes lançados no ano
`'Number of Movies'`| Número de filmes lançados no ano
`'#1 Movie'`| Filme de maior bilheteria no ano


```python
movies_by_year = pd.read_csv('https://raw.githubusercontent.com/urielmoreirasilva/EST/main/aulas/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados/data/movies_by_year.csv').set_index('Year')
movies_by_year
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Gross in Billions</th>
      <th>Number of Movies</th>
      <th>#1 Movie</th>
    </tr>
    <tr>
      <th>Year</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2022</th>
      <td>5.64</td>
      <td>380</td>
      <td>Top Gun: Maverick</td>
    </tr>
    <tr>
      <th>2021</th>
      <td>4.48</td>
      <td>439</td>
      <td>Spider-Man: No Way Home</td>
    </tr>
    <tr>
      <th>2020</th>
      <td>2.11</td>
      <td>456</td>
      <td>Bad Boys for Life</td>
    </tr>
    <tr>
      <th>2019</th>
      <td>11.36</td>
      <td>910</td>
      <td>Avengers: Endgame</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>11.89</td>
      <td>993</td>
      <td>Black Panther</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>11.08</td>
      <td>854</td>
      <td>Star Wars: Episode VIII - The Last Jedi</td>
    </tr>
    <tr>
      <th>2016</th>
      <td>11.38</td>
      <td>855</td>
      <td>Finding Dory</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>11.15</td>
      <td>845</td>
      <td>Jurassic World</td>
    </tr>
    <tr>
      <th>2014</th>
      <td>10.37</td>
      <td>849</td>
      <td>Guardians of the Galaxy</td>
    </tr>
    <tr>
      <th>2013</th>
      <td>10.96</td>
      <td>826</td>
      <td>Iron Man 3</td>
    </tr>
    <tr>
      <th>2012</th>
      <td>10.84</td>
      <td>807</td>
      <td>The Avengers</td>
    </tr>
    <tr>
      <th>2011</th>
      <td>10.16</td>
      <td>731</td>
      <td>Harry Potter and the Deathly Hallows: Part 2</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>10.59</td>
      <td>651</td>
      <td>Avatar</td>
    </tr>
    <tr>
      <th>2009</th>
      <td>10.62</td>
      <td>646</td>
      <td>Transformers: Revenge of the Fallen</td>
    </tr>
    <tr>
      <th>2008</th>
      <td>9.65</td>
      <td>725</td>
      <td>The Dark Knight</td>
    </tr>
    <tr>
      <th>2007</th>
      <td>9.68</td>
      <td>775</td>
      <td>Spider-Man 3</td>
    </tr>
    <tr>
      <th>2006</th>
      <td>9.20</td>
      <td>746</td>
      <td>Pirates of the Caribbean: Dead Man's Chest</td>
    </tr>
    <tr>
      <th>2005</th>
      <td>8.83</td>
      <td>676</td>
      <td>Star Wars: Episode III - Revenge of the Sith</td>
    </tr>
    <tr>
      <th>2004</th>
      <td>9.35</td>
      <td>700</td>
      <td>Shrek 2</td>
    </tr>
    <tr>
      <th>2003</th>
      <td>9.23</td>
      <td>667</td>
      <td>Finding Nemo</td>
    </tr>
    <tr>
      <th>2002</th>
      <td>9.16</td>
      <td>570</td>
      <td>Spider-Man</td>
    </tr>
    <tr>
      <th>2001</th>
      <td>7.96</td>
      <td>412</td>
      <td>Harry Potter and the Sorcerer's Stone</td>
    </tr>
    <tr>
      <th>2000</th>
      <td>7.48</td>
      <td>439</td>
      <td>How the Grinch Stole Christmas</td>
    </tr>
    <tr>
      <th>1999</th>
      <td>7.34</td>
      <td>448</td>
      <td>Star Wars: Episode I - The Phantom Menace</td>
    </tr>
    <tr>
      <th>1998</th>
      <td>6.70</td>
      <td>334</td>
      <td>Titanic</td>
    </tr>
    <tr>
      <th>1997</th>
      <td>6.08</td>
      <td>310</td>
      <td>Men in Black</td>
    </tr>
    <tr>
      <th>1996</th>
      <td>5.60</td>
      <td>306</td>
      <td>Independence Day</td>
    </tr>
    <tr>
      <th>1995</th>
      <td>5.11</td>
      <td>291</td>
      <td>Batman Forever</td>
    </tr>
    <tr>
      <th>1994</th>
      <td>5.06</td>
      <td>259</td>
      <td>The Lion King</td>
    </tr>
    <tr>
      <th>1993</th>
      <td>4.82</td>
      <td>267</td>
      <td>Jurassic Park</td>
    </tr>
    <tr>
      <th>1992</th>
      <td>4.52</td>
      <td>247</td>
      <td>Batman Returns</td>
    </tr>
    <tr>
      <th>1991</th>
      <td>4.34</td>
      <td>253</td>
      <td>Terminator 2: Judgment Day</td>
    </tr>
    <tr>
      <th>1990</th>
      <td>4.33</td>
      <td>236</td>
      <td>Ghost</td>
    </tr>
    <tr>
      <th>1989</th>
      <td>4.08</td>
      <td>235</td>
      <td>Batman</td>
    </tr>
    <tr>
      <th>1988</th>
      <td>3.54</td>
      <td>239</td>
      <td>Who Framed Roger Rabbit</td>
    </tr>
    <tr>
      <th>1987</th>
      <td>3.34</td>
      <td>226</td>
      <td>Beverly Hills Cop II</td>
    </tr>
    <tr>
      <th>1986</th>
      <td>3.07</td>
      <td>201</td>
      <td>Top Gun</td>
    </tr>
    <tr>
      <th>1985</th>
      <td>3.02</td>
      <td>191</td>
      <td>Back to the Future</td>
    </tr>
    <tr>
      <th>1984</th>
      <td>3.07</td>
      <td>169</td>
      <td>Ghostbusters</td>
    </tr>
    <tr>
      <th>1983</th>
      <td>2.74</td>
      <td>149</td>
      <td>Star Wars: Episode VI - Return of the Jedi</td>
    </tr>
    <tr>
      <th>1982</th>
      <td>3.00</td>
      <td>132</td>
      <td>E.T. the Extra-Terrestrial</td>
    </tr>
    <tr>
      <th>1981</th>
      <td>0.90</td>
      <td>56</td>
      <td>Superman II</td>
    </tr>
    <tr>
      <th>1980</th>
      <td>1.64</td>
      <td>68</td>
      <td>Star Wars: Episode V - The Empire Strikes Back</td>
    </tr>
    <tr>
      <th>1979</th>
      <td>1.23</td>
      <td>40</td>
      <td>Superman</td>
    </tr>
    <tr>
      <th>1978</th>
      <td>0.83</td>
      <td>13</td>
      <td>Grease</td>
    </tr>
    <tr>
      <th>1977</th>
      <td>0.44</td>
      <td>9</td>
      <td>Star Wars: Episode IV - A New Hope</td>
    </tr>
  </tbody>
</table>
</div>



- **Pergunta**: como o número de filmes lançados por ano mudou ao longo do tempo? 🤔


```python
movies_by_year.plot(kind = 'line', y = 'Number of Movies');
```


    
![png](T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_46_0.png)
    


### Gráficos de linha

- Os gráficos de linhas mostram tendências em variáveis ​​numéricas ao longo do tempo.

- Para criar um gráfico de linhas a partir de um DataFrame `df` genérico com duas colunas numéricas `'x_column_for_horizontal'` e `'y_column_for_vertical'`, invocamos

````python
df.plot(
    kind = 'line', 
    x = x_column_for_horizontal, 
    y = y_column_for_vertical
)
````

- **Dica**: quando quisermos que o eixo $x$ seja o índice do DataFrame, basta omitirmos o argumento `x =`!

Naturalmente, isso não funciona para gráficos de dispersão, mas funciona para a maioria dos outros tipos de gráficos.


```python
movies_by_year.plot(kind = 'line', y = 'Number of Movies');
```


    
![png](T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_50_0.png)
    


#### Filtrando pelo índice

- Muitas vezes estamos interessados em _encurtar_ o horizonte de um gráfico de linhas.
- Isso pode nos ajudar a melhorar a visualização geral ou nos permitir discernir melhor algum detalhe específico, por exemplo.
- Para realizar esse encurtamento, basta invocar o plot após filtrar o DataFrame da maneira desejada por seu índice.

No exemplo acima, podemos criar um gráfico de linhas considerando apenas os anos de 2000 em diante:


```python
movies_by_year[movies_by_year.index >= 2000].plot(kind='line', y='Number of Movies');
```


    
![png](T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_53_0.png)
    


Note agora que as quedas em torno de 2008 e 2020 estão muito mais aparentes!

#### Como as quedas em 2008 e 2020 afetaram o total bruto de bilheteria doméstica?


```python
movies_by_year[movies_by_year.index >= 2000].plot(kind = 'line', y = 'Total Gross in Billions');
```


    
![png](T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_56_0.png)
    


#### Curiosidade: qual foi o filme de maior bilheteria de 2016? 🐟


```python
movies_by_year[movies_by_year.index == 2016]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Gross in Billions</th>
      <th>Number of Movies</th>
      <th>#1 Movie</th>
    </tr>
    <tr>
      <th>Year</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2016</th>
      <td>11.38</td>
      <td>855</td>
      <td>Finding Dory</td>
    </tr>
  </tbody>
</table>
</div>



## Gráficos de barras 📊

### Exemplo: [200 músicas mais tocadas no Spotify dos EUA](https://spotifycharts.com/regional) (21/01/23)


```python
charts = (pd.read_csv('https://raw.githubusercontent.com/urielmoreirasilva/EST/main/aulas/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados/data/regional-us-daily-2023-01-21.csv')
          .set_index('rank')
          .get(['track_name', 'artist_names', 'streams', 'uri'])
         )
charts
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>track_name</th>
      <th>artist_names</th>
      <th>streams</th>
      <th>uri</th>
    </tr>
    <tr>
      <th>rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Flowers</td>
      <td>Miley Cyrus</td>
      <td>3356361</td>
      <td>spotify:track:0yLdNVWF3Srea0uzk55zFn</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kill Bill</td>
      <td>SZA</td>
      <td>2479445</td>
      <td>spotify:track:1Qrg8KqiBpW07V7PNxwwwL</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Creepin' (with The Weeknd &amp; 21 Savage)</td>
      <td>Metro Boomin, The Weeknd, 21 Savage</td>
      <td>1337320</td>
      <td>spotify:track:2dHHgzDwk4BJdRwy9uXhTO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Superhero (Heroes &amp; Villains) [with Future &amp; C...</td>
      <td>Metro Boomin, Future, Chris Brown</td>
      <td>1235285</td>
      <td>spotify:track:0vjeOZ3Ft5jvAi9SBFJm1j</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Rich Flex</td>
      <td>Drake, 21 Savage</td>
      <td>1109704</td>
      <td>spotify:track:1bDbXMyjaUIooNwFE9wn0N</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>196</th>
      <td>Burn, Burn, Burn</td>
      <td>Zach Bryan</td>
      <td>267772</td>
      <td>spotify:track:5jfhLCSIFUO4ndzNRh4w4G</td>
    </tr>
    <tr>
      <th>197</th>
      <td>LET GO</td>
      <td>Central Cee</td>
      <td>267401</td>
      <td>spotify:track:3zkyus0njMCL6phZmNNEeN</td>
    </tr>
    <tr>
      <th>198</th>
      <td>Major Distribution</td>
      <td>Drake, 21 Savage</td>
      <td>266986</td>
      <td>spotify:track:46s57QULU02Voy0Kup6UEb</td>
    </tr>
    <tr>
      <th>199</th>
      <td>Sun to Me</td>
      <td>Zach Bryan</td>
      <td>266968</td>
      <td>spotify:track:1SjsVdSXpwm1kTdYEHoPIT</td>
    </tr>
    <tr>
      <th>200</th>
      <td>The Real Slim Shady</td>
      <td>Eminem</td>
      <td>266698</td>
      <td>spotify:track:3yfqSUWxFvZELEM4PmlwIR</td>
    </tr>
  </tbody>
</table>
<p>200 rows × 4 columns</p>
</div>



### Motivação

Quantos streams as 10 músicas mais populares têm?


```python
charts
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>track_name</th>
      <th>artist_names</th>
      <th>streams</th>
      <th>uri</th>
    </tr>
    <tr>
      <th>rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Flowers</td>
      <td>Miley Cyrus</td>
      <td>3356361</td>
      <td>spotify:track:0yLdNVWF3Srea0uzk55zFn</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kill Bill</td>
      <td>SZA</td>
      <td>2479445</td>
      <td>spotify:track:1Qrg8KqiBpW07V7PNxwwwL</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Creepin' (with The Weeknd &amp; 21 Savage)</td>
      <td>Metro Boomin, The Weeknd, 21 Savage</td>
      <td>1337320</td>
      <td>spotify:track:2dHHgzDwk4BJdRwy9uXhTO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Superhero (Heroes &amp; Villains) [with Future &amp; C...</td>
      <td>Metro Boomin, Future, Chris Brown</td>
      <td>1235285</td>
      <td>spotify:track:0vjeOZ3Ft5jvAi9SBFJm1j</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Rich Flex</td>
      <td>Drake, 21 Savage</td>
      <td>1109704</td>
      <td>spotify:track:1bDbXMyjaUIooNwFE9wn0N</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>196</th>
      <td>Burn, Burn, Burn</td>
      <td>Zach Bryan</td>
      <td>267772</td>
      <td>spotify:track:5jfhLCSIFUO4ndzNRh4w4G</td>
    </tr>
    <tr>
      <th>197</th>
      <td>LET GO</td>
      <td>Central Cee</td>
      <td>267401</td>
      <td>spotify:track:3zkyus0njMCL6phZmNNEeN</td>
    </tr>
    <tr>
      <th>198</th>
      <td>Major Distribution</td>
      <td>Drake, 21 Savage</td>
      <td>266986</td>
      <td>spotify:track:46s57QULU02Voy0Kup6UEb</td>
    </tr>
    <tr>
      <th>199</th>
      <td>Sun to Me</td>
      <td>Zach Bryan</td>
      <td>266968</td>
      <td>spotify:track:1SjsVdSXpwm1kTdYEHoPIT</td>
    </tr>
    <tr>
      <th>200</th>
      <td>The Real Slim Shady</td>
      <td>Eminem</td>
      <td>266698</td>
      <td>spotify:track:3yfqSUWxFvZELEM4PmlwIR</td>
    </tr>
  </tbody>
</table>
<p>200 rows × 4 columns</p>
</div>




```python
charts.take(np.arange(10))
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>track_name</th>
      <th>artist_names</th>
      <th>streams</th>
      <th>uri</th>
    </tr>
    <tr>
      <th>rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Flowers</td>
      <td>Miley Cyrus</td>
      <td>3356361</td>
      <td>spotify:track:0yLdNVWF3Srea0uzk55zFn</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kill Bill</td>
      <td>SZA</td>
      <td>2479445</td>
      <td>spotify:track:1Qrg8KqiBpW07V7PNxwwwL</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Creepin' (with The Weeknd &amp; 21 Savage)</td>
      <td>Metro Boomin, The Weeknd, 21 Savage</td>
      <td>1337320</td>
      <td>spotify:track:2dHHgzDwk4BJdRwy9uXhTO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Superhero (Heroes &amp; Villains) [with Future &amp; C...</td>
      <td>Metro Boomin, Future, Chris Brown</td>
      <td>1235285</td>
      <td>spotify:track:0vjeOZ3Ft5jvAi9SBFJm1j</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Rich Flex</td>
      <td>Drake, 21 Savage</td>
      <td>1109704</td>
      <td>spotify:track:1bDbXMyjaUIooNwFE9wn0N</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Shakira: Bzrp Music Sessions, Vol. 53</td>
      <td>Bizarrap, Shakira</td>
      <td>1051226</td>
      <td>spotify:track:4nrPB8O7Y7wsOCJdgXkthe</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Just Wanna Rock</td>
      <td>Lil Uzi Vert</td>
      <td>998684</td>
      <td>spotify:track:4FyesJzVpA39hbYvcseO2d</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Anti-Hero</td>
      <td>Taylor Swift</td>
      <td>936166</td>
      <td>spotify:track:0V3wPSX9ygBnCm8psDIegu</td>
    </tr>
    <tr>
      <th>9</th>
      <td>golden hour</td>
      <td>JVKE</td>
      <td>870031</td>
      <td>spotify:track:5odlY52u43F5BjByhxg7wg</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Unholy (feat. Kim Petras)</td>
      <td>Sam Smith, Kim Petras</td>
      <td>859271</td>
      <td>spotify:track:3nqQXoyQOWXiESFLlDF1hG</td>
    </tr>
  </tbody>
</table>
</div>




```python
charts.take(np.arange(10)).plot(kind = 'barh', x = 'track_name', y = 'streams');
```


    
![png](T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_65_0.png)
    


### Gráficos de barra

- Os gráficos de barras nos permitem visualizar a relação entre uma variável categórica e uma variável numérica.

- Para criar um gráfico de barras a partir de um DataFrame `df` genérico com uma coluna categórica `'categorical_column_name'` e uma coluna numérica `'numerical_column_name'`, invocamos

````python
df.plot(
    kind = 'barh', 
    x = categorical_column_name, 
    y = numerical_column_name
)
````

- O **"h"** em `'barh'` significa **"horizontal"**.
- Tipicamente, é mais fácil ler os rótulos quando o gráfico de barras é organizado de maneira horizontal.
- No gráfico anterior, definimos `y = 'Streams'`, ainda que os streams sejam medidos pelo comprimento do eixo $x$.
    - Isso ocorre porque em um gráfico de barras, _canonicamente_, a variável categórica está no eixo $x$ e a numérica no eixo $y$ – a opção `'barh'` apenas muda a "orientação" do gráfico de maneira a produzir uma visualização melhor (mais sobre isso abaixo). 


```python
# As barras no gráfico abaixo aparecem na ordem "oposta" à que aparecem no DataFrame.
(charts
 .take(np.arange(10))
 .sort_values(by = 'streams')
 .plot(kind = 'barh', x = 'track_name', y = 'streams')
);
```


    
![png](T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_69_0.png)
    


- Embora em geral na maior parte dos casos consigamos escolher parâmetros que nos ajudem a visualizar melhor nosso dados, a _espessura_ e o _espaçamento_ das barras em um gráfico de barras são _arbitrários_.
- Da mesma forma, a _ordem dos rótulos_ categóricos também é arbitrária.

#### Quantas músicas os 15 melhores artistas têm entre as 200 mais tocadas?

Para responder essa pergunta, primeiro vamos criar um DataFrame com uma única coluna que descreve o número de músicas entre as 200 melhores por artista.

Faremos isso utilizando o `.groupby` com `.size()`, agrupando por `'artist_names'`:


```python
charts
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>track_name</th>
      <th>artist_names</th>
      <th>streams</th>
      <th>uri</th>
    </tr>
    <tr>
      <th>rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Flowers</td>
      <td>Miley Cyrus</td>
      <td>3356361</td>
      <td>spotify:track:0yLdNVWF3Srea0uzk55zFn</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kill Bill</td>
      <td>SZA</td>
      <td>2479445</td>
      <td>spotify:track:1Qrg8KqiBpW07V7PNxwwwL</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Creepin' (with The Weeknd &amp; 21 Savage)</td>
      <td>Metro Boomin, The Weeknd, 21 Savage</td>
      <td>1337320</td>
      <td>spotify:track:2dHHgzDwk4BJdRwy9uXhTO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Superhero (Heroes &amp; Villains) [with Future &amp; C...</td>
      <td>Metro Boomin, Future, Chris Brown</td>
      <td>1235285</td>
      <td>spotify:track:0vjeOZ3Ft5jvAi9SBFJm1j</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Rich Flex</td>
      <td>Drake, 21 Savage</td>
      <td>1109704</td>
      <td>spotify:track:1bDbXMyjaUIooNwFE9wn0N</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>196</th>
      <td>Burn, Burn, Burn</td>
      <td>Zach Bryan</td>
      <td>267772</td>
      <td>spotify:track:5jfhLCSIFUO4ndzNRh4w4G</td>
    </tr>
    <tr>
      <th>197</th>
      <td>LET GO</td>
      <td>Central Cee</td>
      <td>267401</td>
      <td>spotify:track:3zkyus0njMCL6phZmNNEeN</td>
    </tr>
    <tr>
      <th>198</th>
      <td>Major Distribution</td>
      <td>Drake, 21 Savage</td>
      <td>266986</td>
      <td>spotify:track:46s57QULU02Voy0Kup6UEb</td>
    </tr>
    <tr>
      <th>199</th>
      <td>Sun to Me</td>
      <td>Zach Bryan</td>
      <td>266968</td>
      <td>spotify:track:1SjsVdSXpwm1kTdYEHoPIT</td>
    </tr>
    <tr>
      <th>200</th>
      <td>The Real Slim Shady</td>
      <td>Eminem</td>
      <td>266698</td>
      <td>spotify:track:3yfqSUWxFvZELEM4PmlwIR</td>
    </tr>
  </tbody>
</table>
<p>200 rows × 4 columns</p>
</div>




```python
songs_per_artist = charts.groupby('artist_names').size()
songs_per_artist
```




    artist_names
    21 Savage, Metro Boomin    1
    80purppp                   1
    A Boogie Wit da Hoodie     1
    Arctic Monkeys             2
    Arcángel, Bad Bunny        1
                              ..
    XXXTENTACION               1
    Yeat                       1
    Zach Bryan                 4
    d4vd                       2
    Ñengo Flow, Bad Bunny      1
    Length: 145, dtype: int64



Agora, utilizando `.sort_values` e `.take`, manteremos apenas os 15 melhores artistas:


```python
top_15_artists = (songs_per_artist
                  .sort_values(ascending = False)
                  .take(np.arange(15)))
top_15_artists
```




    artist_names
    SZA                 11
    Taylor Swift         8
    Morgan Wallen        6
    Drake, 21 Savage     5
    The Weeknd           4
    Zach Bryan           4
    Mac DeMarco          3
    J. Cole              3
    Juice WRLD           2
    Brent Faiyaz         2
    Bad Bunny            2
    Kanye West           2
    Harry Styles         2
    Childish Gambino     2
    Lil Uzi Vert         2
    dtype: int64



Antes de invocar `.plot(kind = 'barh', y = 'count')`, ordenaremos `top_15_artists` em ordem **crescente**.

Devemos fazer isso porque o Python _inverte_ a ordem das linhas ao criar barras em gráficos de barras horizontais.


```python
top_15_artists.sort_values().plot(kind = 'barh', y = 'count');
```


    
![png](T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_80_0.png)
    


Note que no comando acima, omitimos a opção `x = 'artist_names'` sem nenhum problema porque como `top_15_artists` é uma `Series` e que já está indexada, o método `.plot` subentende que `x` é o seu índice. 


```python
# Descomente e execute.
# top_15_artists.sort_values().plot(kind = 'barh', x = 'artist_names', y = 'count');
```

### Gráficos de barras verticais

- Para criar um gráfico de barras verticais, utilizamos `kind = 'bar'` ao invés de `kind = 'barh'`.

No nosso exemplo:


```python
top_15_artists.plot(kind = 'bar', y = 'count');
```


    
![png](T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_85_0.png)
    


- Aqui fica clara a razão do Python tomar a variável categórica como a variável correspondente ao eixo $x$, e a variável numérica como a variável correspondente ao eixo $y$.
- Ainda sobre esse ponto, reforçamos aqui a ideia de que `kind = 'barh'` apenas muda a orientação do tipo "canônico", que é `kind = 'bar'`.

#### Quantas vezes as músicas do The Weeknd foram tocadas?


```python
(charts
 [charts.get('artist_names') == 'The Weeknd']
 .sort_values('streams')
 .plot(kind='barh', x='track_name', y='streams')
);
```


    
![png](T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_88_0.png)
    


Parece que não estamos incluindo todas as músicas do The Weeknd aqui...

E como resolvemos esse problema? 🤔

Resposta: Usando `.str.contains`!


```python
weeknd = charts[charts.get('artist_names').str.contains('The Weeknd')]
weeknd
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>track_name</th>
      <th>artist_names</th>
      <th>streams</th>
      <th>uri</th>
    </tr>
    <tr>
      <th>rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>Creepin' (with The Weeknd &amp; 21 Savage)</td>
      <td>Metro Boomin, The Weeknd, 21 Savage</td>
      <td>1337320</td>
      <td>spotify:track:2dHHgzDwk4BJdRwy9uXhTO</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Die For You</td>
      <td>The Weeknd</td>
      <td>794924</td>
      <td>spotify:track:2LBqCSwhJGcFQeTHMVGwy3</td>
    </tr>
    <tr>
      <th>76</th>
      <td>Stargirl Interlude</td>
      <td>The Weeknd, Lana Del Rey</td>
      <td>372624</td>
      <td>spotify:track:5gDWsRxpJ2lZAffh5p7K0w</td>
    </tr>
    <tr>
      <th>78</th>
      <td>Starboy</td>
      <td>The Weeknd, Daft Punk</td>
      <td>361999</td>
      <td>spotify:track:7MXVkk9YMctZqd1Srtv4MB</td>
    </tr>
    <tr>
      <th>102</th>
      <td>The Hills</td>
      <td>The Weeknd</td>
      <td>334354</td>
      <td>spotify:track:7fBv7CLKzipRk6EC6TWHOB</td>
    </tr>
    <tr>
      <th>110</th>
      <td>I Was Never There</td>
      <td>The Weeknd, Gesaffelstein</td>
      <td>328724</td>
      <td>spotify:track:1cKHdTo9u0ZymJdPGSh6nq</td>
    </tr>
    <tr>
      <th>128</th>
      <td>Blinding Lights</td>
      <td>The Weeknd</td>
      <td>311176</td>
      <td>spotify:track:0VjIjW4GlUZAMYd2vXMi3b</td>
    </tr>
    <tr>
      <th>168</th>
      <td>Call Out My Name</td>
      <td>The Weeknd</td>
      <td>281141</td>
      <td>spotify:track:09mEdoA6zrmBPgTEN5qXmN</td>
    </tr>
  </tbody>
</table>
</div>




```python
weeknd.sort_values('streams').plot(kind='barh', x='track_name', y='streams');
```


    
![png](T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados_93_0.png)
    


- As comparações do tipo `charts.get('artist_names') == 'The Weeknd'` filtram apenas pelas músicas cujo artista é **exatamente** `'The Weekend'`.
- Nos casos acima em que esse artista fez algum tipo de colaboração, isso não foi detectado!
- Utilizando o método `.str.contains` em `charts.get('artist_names').str.contains('The Weeknd')`, podemos captar tanto as músicas autoradas _apenas_ por `'The Weekend'`, mas também as que ele fez algum tipo de participação, isto é, autoradas _não somente_ por ele.

### Exercício ✅

Modifique a célula de código abaixo para exibir a quantidade de streams das músicas de algum artista de sua preferência.

<u> Dica</u>: tente utilizar apenas *parte* do nome do artista e verifique como o método `.str.contains` lida com isso! 


```python
# ## Descomente e execute!
# artist = charts[charts.get('artist_names').str.contains('...')]
# artist
```


```python
# ## Descomente e execute!
# artist.sort_values('streams').plot(kind='barh', x='track_name', y='streams');
```

#### Uma demonstração interessante 🎵


```python
# Execute essa célula, mas por enquanto não se preocupe com o que ela faz.
def show_spotify(uri):
    code = uri[uri.rfind(':')+1:]
    src = f"https://open.spotify.com/embed/track/{code}"
    width = 400
    height = 75
    display(IFrame(src, width, height))
```

- Vamos encontrar o URI (_Unique Resource Identifier_) de uma música que nos interessa!


```python
charts
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>track_name</th>
      <th>artist_names</th>
      <th>streams</th>
      <th>uri</th>
    </tr>
    <tr>
      <th>rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Flowers</td>
      <td>Miley Cyrus</td>
      <td>3356361</td>
      <td>spotify:track:0yLdNVWF3Srea0uzk55zFn</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kill Bill</td>
      <td>SZA</td>
      <td>2479445</td>
      <td>spotify:track:1Qrg8KqiBpW07V7PNxwwwL</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Creepin' (with The Weeknd &amp; 21 Savage)</td>
      <td>Metro Boomin, The Weeknd, 21 Savage</td>
      <td>1337320</td>
      <td>spotify:track:2dHHgzDwk4BJdRwy9uXhTO</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Superhero (Heroes &amp; Villains) [with Future &amp; C...</td>
      <td>Metro Boomin, Future, Chris Brown</td>
      <td>1235285</td>
      <td>spotify:track:0vjeOZ3Ft5jvAi9SBFJm1j</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Rich Flex</td>
      <td>Drake, 21 Savage</td>
      <td>1109704</td>
      <td>spotify:track:1bDbXMyjaUIooNwFE9wn0N</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>196</th>
      <td>Burn, Burn, Burn</td>
      <td>Zach Bryan</td>
      <td>267772</td>
      <td>spotify:track:5jfhLCSIFUO4ndzNRh4w4G</td>
    </tr>
    <tr>
      <th>197</th>
      <td>LET GO</td>
      <td>Central Cee</td>
      <td>267401</td>
      <td>spotify:track:3zkyus0njMCL6phZmNNEeN</td>
    </tr>
    <tr>
      <th>198</th>
      <td>Major Distribution</td>
      <td>Drake, 21 Savage</td>
      <td>266986</td>
      <td>spotify:track:46s57QULU02Voy0Kup6UEb</td>
    </tr>
    <tr>
      <th>199</th>
      <td>Sun to Me</td>
      <td>Zach Bryan</td>
      <td>266968</td>
      <td>spotify:track:1SjsVdSXpwm1kTdYEHoPIT</td>
    </tr>
    <tr>
      <th>200</th>
      <td>The Real Slim Shady</td>
      <td>Eminem</td>
      <td>266698</td>
      <td>spotify:track:3yfqSUWxFvZELEM4PmlwIR</td>
    </tr>
  </tbody>
</table>
<p>200 rows × 4 columns</p>
</div>




```python
favorite_song = 'Blinding Lights'
```


```python
song_uri = (charts
            [charts.get('track_name') == favorite_song]
            .get('uri')
            .iloc[0])
song_uri
```




    'spotify:track:0VjIjW4GlUZAMYd2vXMi3b'



Agora, veja o que acontece! 🎶


```python
show_spotify(song_uri)
```



<iframe
    width="400"
    height="75"
    src="https://open.spotify.com/embed/track/0VjIjW4GlUZAMYd2vXMi3b"
    frameborder="0"
    allowfullscreen

></iframe>



## Visualizações "ruins"

- Conforme mencionado anteriormente, as visualizações nos permitem identificar facilmente tendências e comunicar nossos resultados de maneira mais informativa a outras pessoas.
- Porém, algumas visualizações podem tornar os padrões nos dados _mais difíceis_ de ver!
- Os elementos adicionais (e na maioria das vezes desnecessários) que dificultam visualizações são popularmente conhecidos como ["chart junk"](https://eagereyes.org/criticism/chart-junk-considered-useful-after-all).

Além do chart junk, algumas manipulações clássicas dos gráficos incluem distorções dos eixos/unidades, inclusão de elementos de comparação relativa com tamanhos incorretos, etc. 

Seguem abaixo alguns exemplos de visualizações "ruins":

<left>
    <img src = "https://raw.githubusercontent.com/urielmoreirasilva/EST/main/aulas/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados/images/usefuljunk-monster.jpg" width = "50%">
</left>    

<left>
    <img src = "https://raw.githubusercontent.com/urielmoreirasilva/EST/main/aulas/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados/images/average_height.png" width = "50%">
</left>

<left>
    <img src = "https://raw.githubusercontent.com/urielmoreirasilva/EST/main/aulas/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados/images/bananas.png" width = "50%">
</left>

<left>
    <img src = "https://raw.githubusercontent.com/urielmoreirasilva/EST/main/aulas/T%C3%B3pico%2001%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados/images/weather.png" width = "50%">
</left>

## Resumo

- As visualizações facilitam a extração de padrões de conjuntos de dados, e a comunicar esses padrões de maneira clara e intuitiva.
- Existem dois tipos principais de variáveis: **categóricas** e **numéricas**.
- Os tipos de variáveis ​​que estamos visualizando usualmente informam nossa escolha de qual tipo de visualização usar.
- Nesse tópico, introduzimos os **gráficos de dispersão**, **gráficos de linhas** e os **gráficos de barras**.
