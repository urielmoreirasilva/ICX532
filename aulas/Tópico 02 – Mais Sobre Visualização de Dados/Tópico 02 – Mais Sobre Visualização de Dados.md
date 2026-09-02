---
layout: default
title: "Tópico 02 – Mais Sobre Visualização de Dados"
parent: "Aulas Computacionais"
nav_order: 2
---
# Tópico 02 – Mais Sobre Visualização de Dados [<img src="https://raw.githubusercontent.com/urielmoreirasilva/EST/main/aulas/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados/images/colag_logo.svg" style="float: right; vertical-align: middle; width: 42px; height: 42px;">](https://colab.research.google.com/github/urielmoreirasilva/EST/blob/main/aulas/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados.ipynb) [<img src="https://raw.githubusercontent.com/urielmoreirasilva/EST/main/aulas/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados/images/github_logo.svg" style="float: right; margin-right: 12px; vertical-align: middle; width: 36px; height: 36px;">](https://github.com/urielmoreirasilva/EST/blob/main/aulas/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados.ipynb)

Vamos agora aprender um pouco sobre transformação de dados, e ver mais exemplos de visualização!

### Resultados Esperados
1. Aprender como transformar certos conjuntos de dados para melhorar nossas visualizações.
1. Aprender algumas maneiras de apresentar dados sobrepostos.

### Referências
- [CIT, Capítulo 7](https://inferentialthinking.com/)

Material adaptado do [DSC10 (UCSD)](https://dsc10.com/) por [Flavio Figueiredo (DCC-UFMG)](https://flaviovdf.io/fcd/) e [Uriel Silva (DEST-UFMG)](https://urielmoreirasilva.github.io)


```python
# Importando Pandas, Numpy e Matplotlib
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
plt.style.use('ggplot')
```

## Distribuições

### O que é a distribuição de uma variável?

- A _distribuição_ de uma variável consiste em todos os valores da variável que ocorrem no conjunto de dados, juntamente com suas frequências.
- As distribuições nos dizem qual a frequência de ocorrência de um valor ou conjunto de valores, e entre outras coisas nos ajudam a entender o comportamento "esperado" de uma variável. 
- Ambas as variáveis ​​categóricas e numéricas têm distribuições.

### Variáveis ​​categóricas

A distribuição de uma variável categórica é tipicamente exibida como uma _tabela de distribuição de frequências_, ou um _gráfico de barras_.

Como exemplo, vejamos qual a distribuição do tipo de ensino médio dos alunos do Bacharelado em Ciência de Dados, turma 2024/1:


```python
# Tabela de distribuição de frequências
tipo_medio = pd.DataFrame().assign(
    Tipo_Escola=['Privado', 'Público (Estadual)', 'Público (Municipal)', 'Público (Federal)'], 
    Num_Discentes=[15, 8, 3, 7]
)
tipo_medio
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
      <th>Tipo_Escola</th>
      <th>Num_Discentes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Privado</td>
      <td>15</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Público (Estadual)</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Público (Municipal)</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Público (Federal)</td>
      <td>7</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Gráfico de barras (tipo de escola vs. num. de discentes)
tipo_medio.plot(kind='barh', x='Tipo_Escola', y='Num_Discentes');
```


    
![png](T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_8_0.png)
    



```python
# Gráfico de barras (num. de discentes vs. tipo de escola)
tipo_medio.plot(kind='bar', x='Tipo_Escola', y='Num_Discentes');
```


    
![png](T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_9_0.png)
    


### Variáveis ​​numéricas

A distribuição de uma variável numérica nem sempre pode ser representada com precisão por um gráfico de barras, por duas razões comuns:
1. O número de valores distintos assumidos pela variável é grande demais para representarmos em um gráfico;
1. Os valores assumidos pela variável se repetem poucas vezes. 

Como exemplo, vejamos abaixo o número de streams de cada uma das 200 músicas 🎵 mais populares no Spotify nos EUA:


```python
# Carregando o DataFrame
charts = pd.read_csv('https://raw.githubusercontent.com/urielmoreirasilva/EST/main/aulas/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados/data/regional-us-daily-2023-01-21.csv')

# Atribuindo um índice, criando a coluna `million_streams` e filtrando o DataFrame pelas colunas desejadas 
charts = (charts.set_index('rank')
          .assign(million_streams = np.round(charts.get('streams')/1000000, 2))
          .get(['track_name', 'artist_names', 'streams', 'million_streams'])
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
      <th>million_streams</th>
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
      <td>2.48</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kill Bill</td>
      <td>SZA</td>
      <td>2479445</td>
      <td>1.34</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Creepin' (with The Weeknd &amp; 21 Savage)</td>
      <td>Metro Boomin, The Weeknd, 21 Savage</td>
      <td>1337320</td>
      <td>1.24</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Superhero (Heroes &amp; Villains) [with Future &amp; C...</td>
      <td>Metro Boomin, Future, Chris Brown</td>
      <td>1235285</td>
      <td>1.11</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Rich Flex</td>
      <td>Drake, 21 Savage</td>
      <td>1109704</td>
      <td>1.05</td>
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
      <td>0.27</td>
    </tr>
    <tr>
      <th>197</th>
      <td>LET GO</td>
      <td>Central Cee</td>
      <td>267401</td>
      <td>0.27</td>
    </tr>
    <tr>
      <th>198</th>
      <td>Major Distribution</td>
      <td>Drake, 21 Savage</td>
      <td>266986</td>
      <td>0.27</td>
    </tr>
    <tr>
      <th>199</th>
      <td>Sun to Me</td>
      <td>Zach Bryan</td>
      <td>266968</td>
      <td>0.27</td>
    </tr>
    <tr>
      <th>200</th>
      <td>The Real Slim Shady</td>
      <td>Eminem</td>
      <td>266698</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>200 rows × 4 columns</p>
</div>



Para ver a distribuição do número de streams, precisamos agrupar pela coluna `'million_streams'`.


```python
# Agrupando por milhões de streams (`million_streams`)
stream_counts = charts.groupby('million_streams').count()
stream_counts = stream_counts.assign(Count=stream_counts.get('track_name')).drop(columns=['track_name', 'artist_names', 'streams'])
stream_counts
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
      <th>Count</th>
    </tr>
    <tr>
      <th>million_streams</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0.27</th>
      <td>17</td>
    </tr>
    <tr>
      <th>0.28</th>
      <td>20</td>
    </tr>
    <tr>
      <th>0.29</th>
      <td>19</td>
    </tr>
    <tr>
      <th>0.30</th>
      <td>8</td>
    </tr>
    <tr>
      <th>0.31</th>
      <td>14</td>
    </tr>
    <tr>
      <th>0.32</th>
      <td>7</td>
    </tr>
    <tr>
      <th>0.33</th>
      <td>14</td>
    </tr>
    <tr>
      <th>0.34</th>
      <td>7</td>
    </tr>
    <tr>
      <th>0.35</th>
      <td>10</td>
    </tr>
    <tr>
      <th>0.36</th>
      <td>8</td>
    </tr>
    <tr>
      <th>0.37</th>
      <td>1</td>
    </tr>
    <tr>
      <th>0.38</th>
      <td>7</td>
    </tr>
    <tr>
      <th>0.39</th>
      <td>2</td>
    </tr>
    <tr>
      <th>0.40</th>
      <td>5</td>
    </tr>
    <tr>
      <th>0.41</th>
      <td>3</td>
    </tr>
    <tr>
      <th>0.42</th>
      <td>2</td>
    </tr>
    <tr>
      <th>0.43</th>
      <td>4</td>
    </tr>
    <tr>
      <th>0.44</th>
      <td>1</td>
    </tr>
    <tr>
      <th>0.45</th>
      <td>2</td>
    </tr>
    <tr>
      <th>0.46</th>
      <td>1</td>
    </tr>
    <tr>
      <th>0.47</th>
      <td>4</td>
    </tr>
    <tr>
      <th>0.48</th>
      <td>2</td>
    </tr>
    <tr>
      <th>0.49</th>
      <td>1</td>
    </tr>
    <tr>
      <th>0.50</th>
      <td>1</td>
    </tr>
    <tr>
      <th>0.52</th>
      <td>5</td>
    </tr>
    <tr>
      <th>0.53</th>
      <td>1</td>
    </tr>
    <tr>
      <th>0.54</th>
      <td>2</td>
    </tr>
    <tr>
      <th>0.55</th>
      <td>2</td>
    </tr>
    <tr>
      <th>0.56</th>
      <td>1</td>
    </tr>
    <tr>
      <th>0.57</th>
      <td>1</td>
    </tr>
    <tr>
      <th>0.58</th>
      <td>2</td>
    </tr>
    <tr>
      <th>0.61</th>
      <td>1</td>
    </tr>
    <tr>
      <th>0.64</th>
      <td>1</td>
    </tr>
    <tr>
      <th>0.66</th>
      <td>1</td>
    </tr>
    <tr>
      <th>0.67</th>
      <td>1</td>
    </tr>
    <tr>
      <th>0.69</th>
      <td>1</td>
    </tr>
    <tr>
      <th>0.74</th>
      <td>2</td>
    </tr>
    <tr>
      <th>0.75</th>
      <td>1</td>
    </tr>
    <tr>
      <th>0.76</th>
      <td>1</td>
    </tr>
    <tr>
      <th>0.79</th>
      <td>5</td>
    </tr>
    <tr>
      <th>0.83</th>
      <td>1</td>
    </tr>
    <tr>
      <th>0.86</th>
      <td>2</td>
    </tr>
    <tr>
      <th>0.87</th>
      <td>1</td>
    </tr>
    <tr>
      <th>0.94</th>
      <td>1</td>
    </tr>
    <tr>
      <th>1.00</th>
      <td>1</td>
    </tr>
    <tr>
      <th>1.05</th>
      <td>1</td>
    </tr>
    <tr>
      <th>1.11</th>
      <td>1</td>
    </tr>
    <tr>
      <th>1.24</th>
      <td>1</td>
    </tr>
    <tr>
      <th>1.34</th>
      <td>1</td>
    </tr>
    <tr>
      <th>2.48</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Gráfico de barras: milhões de streams
stream_counts.plot(kind = 'bar', y = 'Count', figsize = (15, 5));
```


    
![png](T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_15_0.png)
    


- Essa visualização não nos mostra um fato crucial sobre esse conjunto, isto é, que as duas músicas mais tocadas são _atípicas_ (_outliers_), com **muito mais streams** do que as outras músicas.
- Para contornar esse problema, faz sentido tomarmos o eixo horizontal como _numérico_, não categórico.
- Além disso, faz mais sentido termos mais espaço entre certas barras do que outras, e dessa maneira agruparmos valores que estejam muito próximos uns dos outros (pois esses poderiam ser considerados equivalentes).

## Histogramas

- Visualizaremos agora a distribuição de uma variável numérica com um **histograma**.

Vamos primeiro ao exemplo: abaixo, temos um _histograma de densidade_ para `'million_streams'`.


```python
# Ignore e execute o código abaixo.
charts.plot(
    kind = 'hist',
    y = 'million_streams',
    bins = np.arange(0, 4, 0.5),
    ec = 'w'  # borda branca
);
```


    
![png](T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_20_0.png)
    


Quais são suas impressões sobre esse gráfico?

#### Construindo um histograma: especificando as classes

- A primeira escolha que devemos fazer ao construir um histograma é escolher as **classes** que formarão esse histograma.
- As classes de um histograma são usualmente intervalos _igualmente espaçados_, mas isso não é estritamente necessário.
- O histograma é essencialmente um gráfico de barras onde os valores da variável numérica são categorizados/classificados em classes apropriadas.

#### Escolha do número de classes

- Como padrão, o Python agrupará os dados em 10 compartimentos de tamanhos iguais.
- Podemos especificar outro número de compartimentos de tamanhos iguais definindo o argumento opcional `bins` igual a algum outro valor inteiro.
- Podemos também especificar classes de tamanho diferentes tomando `bins` como uma sequência de pontos finais dos intervalos que definem cada classe.
    - Nesse último caso, essa sequência pode ser um `array` ou uma `list`, por exemplo.


```python
charts.plot(
    kind = 'hist',
    y = 'million_streams',
    bins = 20,
    ec = 'w'
);
```


    
![png](T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_24_0.png)
    



```python
charts.plot(
    kind = 'hist', y = 'million_streams', density = True,
    bins=[0, 1, 2, 3, 4, 5],
    ec = 'w'
);
```


    
![png](T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_25_0.png)
    


Você percebe alguma diferença nos histogramas acima?

#### Histogramas de densidade

- A forma geral dos dois histogramas acima é a mesma, independentemente da diferença nas classes.
    - Esta forma é denominada *assimétrica à direita*.
- Quanto mais classes temos um histograma, mais temos uma imagem mais precisa e granular da distribuição da variável em questão.
- Por outro lado, com muitas classes voltamos ao mesmo problema que tínhamos anteriormente com o gráfico de barras!

- Apesar do comportamento geral ser muito similar, note que os valores no eixo $y$ são bem diferentes entre os dois histogramas.
- Isso se deve ao fato de que o primeiro é um **histograma de frequências**, enquanto o segundo é um **histograma de densidade**.

- Em um histograma de densidade, o eixo $y$ pode ser difícil de interpretar, mas foi projetado para dar ao histograma uma propriedade muito boa: **As barras de um histograma de densidade têm uma área total igual a 1**.
- Isso significa que a área de uma barra é igual à proporção (porcentagem) de todos os valores pertencentes à classe correspondente.

#### Exemplo do cálculo de proporções com base em um histograma


```python
charts.plot(
    kind = 'hist',
    y = 'million_streams',
    density = True,
    bins = [0, 0.5, 1, 1.5, 2.5, 4],
    ec = 'w'
);
```


    
![png](T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_31_0.png)
    


Com base neste histograma, qual proporção das 200 músicas mais populares teve menos de meio milhão de streams?

Primeiramente, verificamos que a altura da barra correspondente à classe $[0, 0.5)$ parece ser igual a $1.6$.

Em segundo lugar, a amplitude dessa classe (base do retângulo) é igual a $0.5 - 0 = 0.5$. 

Podemos calcular a proporção dessa classe com base na fórmula da área de um retângulo, isto é,

$$\begin{align}\text{Area} &= \text{Altura} \times \text{Largura} \\ &= 1,6 \times 0,5 \\ &= 0,8
\end{align}$$

Como aqui as áreas representam proporções, isso significa que a proporção das 200 músicas mais populares com menos de 0,5 milhão de streams foi de aproximadamente 0,8 (ou 80\%).

Podemos verificar os cálculos acima diretamente utilizando:


```python
first_bin = charts[charts.get('million_streams') < 0.5].shape[0]
first_bin
```




    159




```python
first_bin/200
```




    0.795



que é próximo o suficiente (lembre que acima tivemos que estimar a altura em $1.6$).

As unidades do eixo $y$ aqui são "proporção por milhão de fluxos", já que o eixo $x$ representa milhões de fluxos.
- Infelizmente, as unidades do eixo $y$ no histograma sempre são exibidas como "Frequência". **Isto está errado!**
- Podemos corrigir com `plt.ylabel(...)`

### Exercício ✅

Suponha que tenhamos criado um histograma de densidade dos tamanhos dos sapatos das pessoas 👟. Abaixo estão as janelas que escolhemos junto com suas alturas:

| Classe | Altura da barra |
| --- | --- |
| [33, 35) | 0.05 |
| [35, 37) | 0.10 |
| [37, 40) | 0.15 |
| [41, 45] | $x$ |


Qual deve ser o valor de $x$ para que este seja um histograma de densidade válido? Preencha a célula de texto abaixo com a resposta correspondente.

**A.** $x = 0.02$

**B.** $x = 0.05$

**C.** $x = 0.20$

**D.** $x = 0.50$

**E.** $x = 0.70$

> ...

### Gráficos de barras vs. histogramas

Gráfico de barras | Histograma
---|---
Mostra a distribuição de uma variável categórica | Mostra a distribuição de uma variável numérica
1 eixo categórico, 1 eixo numérico | 2 eixos numéricos
As barras têm larguras e espaçamentos arbitrários, mas iguais | O eixo horizontal é numérico, e as classes não necessariamente são iguais
Os comprimentos das barras são proporcionais à quantidade numérica de interesse | A altura das barras mede a densidade; as áreas são proporcionais à proporção (porcentagem) de indivíduos

## Gráficos sobrepostos

### Exemplo: populações de San Diego e San Jose ao longo do tempo

- Os dados desse exemplo, para ambas as cidades, vêm de [macrotrends.net](https://www.macrotrends.net/cities/23129/san-diego/population).


```python
population = pd.read_csv('https://raw.githubusercontent.com/urielmoreirasilva/EST/main/aulas/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados/data/sd-sj-2022.csv').set_index('date')
population
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
      <th>Pop SD</th>
      <th>Growth SD</th>
      <th>Pop SJ</th>
      <th>Growth SJ</th>
    </tr>
    <tr>
      <th>date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1970</th>
      <td>1209000</td>
      <td>3.69</td>
      <td>1009000</td>
      <td>4.34</td>
    </tr>
    <tr>
      <th>1971</th>
      <td>1252000</td>
      <td>3.56</td>
      <td>1027000</td>
      <td>1.78</td>
    </tr>
    <tr>
      <th>1972</th>
      <td>1297000</td>
      <td>3.59</td>
      <td>1046000</td>
      <td>1.85</td>
    </tr>
    <tr>
      <th>1973</th>
      <td>1344000</td>
      <td>3.62</td>
      <td>1064000</td>
      <td>1.72</td>
    </tr>
    <tr>
      <th>1974</th>
      <td>1392000</td>
      <td>3.57</td>
      <td>1084000</td>
      <td>1.88</td>
    </tr>
    <tr>
      <th>1975</th>
      <td>1442000</td>
      <td>3.59</td>
      <td>1103000</td>
      <td>1.75</td>
    </tr>
    <tr>
      <th>1976</th>
      <td>1493000</td>
      <td>3.54</td>
      <td>1123000</td>
      <td>1.81</td>
    </tr>
    <tr>
      <th>1977</th>
      <td>1547000</td>
      <td>3.62</td>
      <td>1143000</td>
      <td>1.78</td>
    </tr>
    <tr>
      <th>1978</th>
      <td>1602000</td>
      <td>3.56</td>
      <td>1163000</td>
      <td>1.75</td>
    </tr>
    <tr>
      <th>1979</th>
      <td>1660000</td>
      <td>3.62</td>
      <td>1184000</td>
      <td>1.81</td>
    </tr>
    <tr>
      <th>1980</th>
      <td>1718000</td>
      <td>3.49</td>
      <td>1204000</td>
      <td>1.69</td>
    </tr>
    <tr>
      <th>1981</th>
      <td>1774000</td>
      <td>3.26</td>
      <td>1221000</td>
      <td>1.41</td>
    </tr>
    <tr>
      <th>1982</th>
      <td>1832000</td>
      <td>3.27</td>
      <td>1237000</td>
      <td>1.31</td>
    </tr>
    <tr>
      <th>1983</th>
      <td>1891000</td>
      <td>3.22</td>
      <td>1254000</td>
      <td>1.37</td>
    </tr>
    <tr>
      <th>1984</th>
      <td>1953000</td>
      <td>3.28</td>
      <td>1271000</td>
      <td>1.36</td>
    </tr>
    <tr>
      <th>1985</th>
      <td>2017000</td>
      <td>3.28</td>
      <td>1288000</td>
      <td>1.34</td>
    </tr>
    <tr>
      <th>1986</th>
      <td>2082000</td>
      <td>3.22</td>
      <td>1305000</td>
      <td>1.32</td>
    </tr>
    <tr>
      <th>1987</th>
      <td>2150000</td>
      <td>3.27</td>
      <td>1323000</td>
      <td>1.38</td>
    </tr>
    <tr>
      <th>1988</th>
      <td>2220000</td>
      <td>3.26</td>
      <td>1341000</td>
      <td>1.36</td>
    </tr>
    <tr>
      <th>1989</th>
      <td>2293000</td>
      <td>3.29</td>
      <td>1359000</td>
      <td>1.34</td>
    </tr>
    <tr>
      <th>1990</th>
      <td>2356000</td>
      <td>2.75</td>
      <td>1376000</td>
      <td>1.25</td>
    </tr>
    <tr>
      <th>1991</th>
      <td>2387000</td>
      <td>1.32</td>
      <td>1392000</td>
      <td>1.16</td>
    </tr>
    <tr>
      <th>1992</th>
      <td>2418000</td>
      <td>1.30</td>
      <td>1408000</td>
      <td>1.15</td>
    </tr>
    <tr>
      <th>1993</th>
      <td>2450000</td>
      <td>1.32</td>
      <td>1424000</td>
      <td>1.14</td>
    </tr>
    <tr>
      <th>1994</th>
      <td>2482000</td>
      <td>1.31</td>
      <td>1441000</td>
      <td>1.19</td>
    </tr>
    <tr>
      <th>1995</th>
      <td>2514000</td>
      <td>1.29</td>
      <td>1457000</td>
      <td>1.11</td>
    </tr>
    <tr>
      <th>1996</th>
      <td>2547000</td>
      <td>1.31</td>
      <td>1474000</td>
      <td>1.17</td>
    </tr>
    <tr>
      <th>1997</th>
      <td>2580000</td>
      <td>1.30</td>
      <td>1491000</td>
      <td>1.15</td>
    </tr>
    <tr>
      <th>1998</th>
      <td>2614000</td>
      <td>1.32</td>
      <td>1508000</td>
      <td>1.14</td>
    </tr>
    <tr>
      <th>1999</th>
      <td>2648000</td>
      <td>1.30</td>
      <td>1525000</td>
      <td>1.13</td>
    </tr>
    <tr>
      <th>2000</th>
      <td>2681000</td>
      <td>1.25</td>
      <td>1541000</td>
      <td>1.05</td>
    </tr>
    <tr>
      <th>2001</th>
      <td>2708000</td>
      <td>1.01</td>
      <td>1554000</td>
      <td>0.84</td>
    </tr>
    <tr>
      <th>2002</th>
      <td>2735000</td>
      <td>1.00</td>
      <td>1566000</td>
      <td>0.77</td>
    </tr>
    <tr>
      <th>2003</th>
      <td>2763000</td>
      <td>1.02</td>
      <td>1578000</td>
      <td>0.77</td>
    </tr>
    <tr>
      <th>2004</th>
      <td>2791000</td>
      <td>1.01</td>
      <td>1591000</td>
      <td>0.82</td>
    </tr>
    <tr>
      <th>2005</th>
      <td>2819000</td>
      <td>1.00</td>
      <td>1603000</td>
      <td>0.75</td>
    </tr>
    <tr>
      <th>2006</th>
      <td>2848000</td>
      <td>1.03</td>
      <td>1616000</td>
      <td>0.81</td>
    </tr>
    <tr>
      <th>2007</th>
      <td>2876000</td>
      <td>0.98</td>
      <td>1629000</td>
      <td>0.80</td>
    </tr>
    <tr>
      <th>2008</th>
      <td>2905000</td>
      <td>1.01</td>
      <td>1642000</td>
      <td>0.80</td>
    </tr>
    <tr>
      <th>2009</th>
      <td>2935000</td>
      <td>1.03</td>
      <td>1655000</td>
      <td>0.79</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>2964000</td>
      <td>0.99</td>
      <td>1668000</td>
      <td>0.79</td>
    </tr>
    <tr>
      <th>2011</th>
      <td>2994000</td>
      <td>1.01</td>
      <td>1681000</td>
      <td>0.78</td>
    </tr>
    <tr>
      <th>2012</th>
      <td>3024000</td>
      <td>1.00</td>
      <td>1694000</td>
      <td>0.77</td>
    </tr>
    <tr>
      <th>2013</th>
      <td>3055000</td>
      <td>1.03</td>
      <td>1708000</td>
      <td>0.83</td>
    </tr>
    <tr>
      <th>2014</th>
      <td>3086000</td>
      <td>1.01</td>
      <td>1721000</td>
      <td>0.76</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>3117000</td>
      <td>1.00</td>
      <td>1735000</td>
      <td>0.81</td>
    </tr>
    <tr>
      <th>2016</th>
      <td>3148000</td>
      <td>0.99</td>
      <td>1749000</td>
      <td>0.81</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>3180000</td>
      <td>1.02</td>
      <td>1762000</td>
      <td>0.74</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>3212000</td>
      <td>1.01</td>
      <td>1776000</td>
      <td>0.79</td>
    </tr>
    <tr>
      <th>2019</th>
      <td>3231000</td>
      <td>0.59</td>
      <td>1783000</td>
      <td>0.39</td>
    </tr>
    <tr>
      <th>2020</th>
      <td>3251000</td>
      <td>0.62</td>
      <td>1791000</td>
      <td>0.45</td>
    </tr>
    <tr>
      <th>2021</th>
      <td>3272000</td>
      <td>0.65</td>
      <td>1799000</td>
      <td>0.45</td>
    </tr>
    <tr>
      <th>2022</th>
      <td>3295000</td>
      <td>0.70</td>
      <td>1809000</td>
      <td>0.56</td>
    </tr>
    <tr>
      <th>2023</th>
      <td>3319000</td>
      <td>0.73</td>
      <td>1821000</td>
      <td>0.66</td>
    </tr>
  </tbody>
</table>
</div>



#### Gráficos de linha: população ao longo do tempo


```python
population.plot(kind = 'line', y = 'Growth SD', 
                title = 'San Diego population growth rate', legend = False);
```


    
![png](T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_49_0.png)
    



```python
population.plot(kind = 'line', y = 'Growth SJ', 
                title = 'San Jose population growth rate', legend = False);
```


    
![png](T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_50_0.png)
    


Note que nos gráficos acima especificamos os argumentos opcionais `title` e `legend`.

Existem [muitos outros argumentos opcionais](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.plot.html) em um plot: alguns dos mais comuns incluem `figsize`, `xlabel` e `ylabel`.

#### Gráficos de linhas sobrepostos

- Se `y = column_name` for omitido do plot, **todas** as colunas do DataFrame serão plotadas!


```python
population.plot(kind = 'line');
```


    
![png](T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_54_0.png)
    


Nesse exemplo, porém, a diferença de escala entre as variáveis distorce bastante o comportamento em favor das variáveis com valores mais altos.

### Selecionando várias colunas de uma vez

- Para selecionar várias colunas de um DataFrame, utilize `.get([column_1, ..., column_k])`.
- Alterntaivamente, passar uma `lista` de rótulos de colunas como argumento para `.get` também retorna um DataFrame com as colunas desejadas.


```python
growths = population.get(['Growth SD', 'Growth SJ'])
growths
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
      <th>Growth SD</th>
      <th>Growth SJ</th>
    </tr>
    <tr>
      <th>date</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1970</th>
      <td>3.69</td>
      <td>4.34</td>
    </tr>
    <tr>
      <th>1971</th>
      <td>3.56</td>
      <td>1.78</td>
    </tr>
    <tr>
      <th>1972</th>
      <td>3.59</td>
      <td>1.85</td>
    </tr>
    <tr>
      <th>1973</th>
      <td>3.62</td>
      <td>1.72</td>
    </tr>
    <tr>
      <th>1974</th>
      <td>3.57</td>
      <td>1.88</td>
    </tr>
    <tr>
      <th>1975</th>
      <td>3.59</td>
      <td>1.75</td>
    </tr>
    <tr>
      <th>1976</th>
      <td>3.54</td>
      <td>1.81</td>
    </tr>
    <tr>
      <th>1977</th>
      <td>3.62</td>
      <td>1.78</td>
    </tr>
    <tr>
      <th>1978</th>
      <td>3.56</td>
      <td>1.75</td>
    </tr>
    <tr>
      <th>1979</th>
      <td>3.62</td>
      <td>1.81</td>
    </tr>
    <tr>
      <th>1980</th>
      <td>3.49</td>
      <td>1.69</td>
    </tr>
    <tr>
      <th>1981</th>
      <td>3.26</td>
      <td>1.41</td>
    </tr>
    <tr>
      <th>1982</th>
      <td>3.27</td>
      <td>1.31</td>
    </tr>
    <tr>
      <th>1983</th>
      <td>3.22</td>
      <td>1.37</td>
    </tr>
    <tr>
      <th>1984</th>
      <td>3.28</td>
      <td>1.36</td>
    </tr>
    <tr>
      <th>1985</th>
      <td>3.28</td>
      <td>1.34</td>
    </tr>
    <tr>
      <th>1986</th>
      <td>3.22</td>
      <td>1.32</td>
    </tr>
    <tr>
      <th>1987</th>
      <td>3.27</td>
      <td>1.38</td>
    </tr>
    <tr>
      <th>1988</th>
      <td>3.26</td>
      <td>1.36</td>
    </tr>
    <tr>
      <th>1989</th>
      <td>3.29</td>
      <td>1.34</td>
    </tr>
    <tr>
      <th>1990</th>
      <td>2.75</td>
      <td>1.25</td>
    </tr>
    <tr>
      <th>1991</th>
      <td>1.32</td>
      <td>1.16</td>
    </tr>
    <tr>
      <th>1992</th>
      <td>1.30</td>
      <td>1.15</td>
    </tr>
    <tr>
      <th>1993</th>
      <td>1.32</td>
      <td>1.14</td>
    </tr>
    <tr>
      <th>1994</th>
      <td>1.31</td>
      <td>1.19</td>
    </tr>
    <tr>
      <th>1995</th>
      <td>1.29</td>
      <td>1.11</td>
    </tr>
    <tr>
      <th>1996</th>
      <td>1.31</td>
      <td>1.17</td>
    </tr>
    <tr>
      <th>1997</th>
      <td>1.30</td>
      <td>1.15</td>
    </tr>
    <tr>
      <th>1998</th>
      <td>1.32</td>
      <td>1.14</td>
    </tr>
    <tr>
      <th>1999</th>
      <td>1.30</td>
      <td>1.13</td>
    </tr>
    <tr>
      <th>2000</th>
      <td>1.25</td>
      <td>1.05</td>
    </tr>
    <tr>
      <th>2001</th>
      <td>1.01</td>
      <td>0.84</td>
    </tr>
    <tr>
      <th>2002</th>
      <td>1.00</td>
      <td>0.77</td>
    </tr>
    <tr>
      <th>2003</th>
      <td>1.02</td>
      <td>0.77</td>
    </tr>
    <tr>
      <th>2004</th>
      <td>1.01</td>
      <td>0.82</td>
    </tr>
    <tr>
      <th>2005</th>
      <td>1.00</td>
      <td>0.75</td>
    </tr>
    <tr>
      <th>2006</th>
      <td>1.03</td>
      <td>0.81</td>
    </tr>
    <tr>
      <th>2007</th>
      <td>0.98</td>
      <td>0.80</td>
    </tr>
    <tr>
      <th>2008</th>
      <td>1.01</td>
      <td>0.80</td>
    </tr>
    <tr>
      <th>2009</th>
      <td>1.03</td>
      <td>0.79</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>0.99</td>
      <td>0.79</td>
    </tr>
    <tr>
      <th>2011</th>
      <td>1.01</td>
      <td>0.78</td>
    </tr>
    <tr>
      <th>2012</th>
      <td>1.00</td>
      <td>0.77</td>
    </tr>
    <tr>
      <th>2013</th>
      <td>1.03</td>
      <td>0.83</td>
    </tr>
    <tr>
      <th>2014</th>
      <td>1.01</td>
      <td>0.76</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>1.00</td>
      <td>0.81</td>
    </tr>
    <tr>
      <th>2016</th>
      <td>0.99</td>
      <td>0.81</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>1.02</td>
      <td>0.74</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>1.01</td>
      <td>0.79</td>
    </tr>
    <tr>
      <th>2019</th>
      <td>0.59</td>
      <td>0.39</td>
    </tr>
    <tr>
      <th>2020</th>
      <td>0.62</td>
      <td>0.45</td>
    </tr>
    <tr>
      <th>2021</th>
      <td>0.65</td>
      <td>0.45</td>
    </tr>
    <tr>
      <th>2022</th>
      <td>0.70</td>
      <td>0.56</td>
    </tr>
    <tr>
      <th>2023</th>
      <td>0.73</td>
      <td>0.66</td>
    </tr>
  </tbody>
</table>
</div>




```python
growths.plot(kind = 'line');
```


    
![png](T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_58_0.png)
    


- Ao elaborar gráficos sobrepostos, lembre-se sempre de omitir o argumento $y$.
- Quando o DataFrame possui uma coluna de índices, naturalmente esse índice será escolhido para o eixo $x$.
    - Caso contrário, podemos especificar a variável do eixo $x$ através de `.plot(x = column_name)`.
    - Note que não é necessário especificar mais de uma variável para o eixo $x$; todas as variáveis do eixo $y$ compartilharão o mesmo eixo $x$.

### Outro exemplo: alturas das crianças e de seus pais 👪 📏

- Os dados desse exemplo consistem em um conjunto de medidas antropométricas de várias famílias, coletados no final do século XVIII por [Francis Galton](https://en.wikipedia.org/wiki/Francis_Galton).
- Galton foi um dos pioneiros da Eugenia, e essa é uma das principais razões pelas quais ele coletou esses dados.
- A análise sistemática desses dados fez com que Galton recebesse reconhecimento como o descobridor do fenômeno de **regressão à média** em certos fenômenos da natureza, e à técnica de regressão linear em geral.  

Para esse exemplo, selecionaremos apenas duas colunas do DataFrame original: `'mother'` e `'childHeight'`.


```python
mother_child = pd.read_csv('https://raw.githubusercontent.com/urielmoreirasilva/EST/main/aulas/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados/data/galton.csv').get(['mother', 'childHeight'])
mother_child
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
      <th>mother</th>
      <th>childHeight</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>67.0</td>
      <td>73.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>67.0</td>
      <td>69.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>67.0</td>
      <td>69.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>67.0</td>
      <td>69.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>66.5</td>
      <td>73.5</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>929</th>
      <td>66.0</td>
      <td>64.0</td>
    </tr>
    <tr>
      <th>930</th>
      <td>66.0</td>
      <td>62.0</td>
    </tr>
    <tr>
      <th>931</th>
      <td>66.0</td>
      <td>61.0</td>
    </tr>
    <tr>
      <th>932</th>
      <td>63.0</td>
      <td>66.5</td>
    </tr>
    <tr>
      <th>933</th>
      <td>63.0</td>
      <td>57.0</td>
    </tr>
  </tbody>
</table>
<p>934 rows × 2 columns</p>
</div>



#### Histogramas sobrepostos

- A sobreposição de histogramas funciona da mesma maneira como vimos anteriormente: basta ignorar o argumento `'y'` na invocação do `.plot'.
- Quando `kind = 'hist'`, o parâmetro gráfico `alpha` controla o quão _transparentes_ as barras serão (`alpha = 1` é opaco, `alpha = 0` é transparente).


```python
height_bins = np.arange(55, 80, 2.5)
mother_child.plot(kind = 'hist', density = True, ec = 'w',
                  alpha = 0.65, bins = height_bins);
```


    
![png](T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_files/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados_64_0.png)
    


Analisando a sobreposição dos histogramas acima, concluímos que, em média, os filhos são mais altos do que suas mães.

Porém, note que ao escolhermos apenas `'mother'` e `'childHeight'`, ignoramos uma informação bem importante: o sexo dos filhos!

### Exercício ✅

Nas duas células de código abaixo, refaça os histogramas sobrepostos de `'mother'` e `'childHeight'`, mas agora filtrando pelo sexo dos filhos (uma célula para os homens e outra para as mulheres). Suas conclusões se mantiveram as mesmas, isto é, em média os filhos realmente parecem ser mais altos que suas mães?

*<u> Dica<u/>: Redeclare o DataFrame, invocando algo do tipo `df = pd.read_csv('https://raw.githubusercontent.com/urielmoreirasilva/EST/main/aulas/T%C3%B3pico%2002%20%E2%80%93%20Mais%20Sobre%20Visualiza%C3%A7%C3%A3o%20de%20Dados/data/galton.csv').get(['mother', 'childHeight', 'gender'])`.*


```python
# Histograma dos filhos do sexo masculino
...
```




    Ellipsis




```python
# Histograma dos filhos do sexo feminino
...
```




    Ellipsis



## Resumo

- A distribuição de uma variável descreve as frequências de ocorrência associadas à cada valor dessa variável no nosso conjunto de dados.  
- Os histogramas são ferramentas utilizadas para visualizar a distribuição de uma variável numérica.
- Nos histogramas de densidade, a área de uma barra representa a proporção (porcentagem) dos valores dentro da classe correspondente.
- Podemos sobrepor vários gráficos de linhas, gráficos de barras e histogramas uns sobre os outros para observar os relacionamentos entre diferentes distribuições.
