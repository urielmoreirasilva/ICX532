---
layout: default
title: "Laboratório 2 – Visualização de Dados"
parent: "Gabaritos"
nav_order: 2
---
# Laboratório 2 – Visualização de Dados (gabarito) [<img src="https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs_gabs/Laborat%C3%B3rio%202%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados%20%28gabarito%29/images/colag_logo.svg" style="float: right; margin-right: 0%; vertical-align: middle; width: 6.5%;">](https://colab.research.google.com/github/urielmoreirasilva/ICX532/blob/main/labs_gabs/Laborat%C3%B3rio%202%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados%20%28gabarito%29/Laborat%C3%B3rio%202%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados%20%28gabarito%29.ipynb) [<img src="https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs_gabs/Laborat%C3%B3rio%202%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados%20%28gabarito%29/images/github_logo.svg" style="float: right; margin-right: 0%; vertical-align: middle; width: 3.25%;">](https://github.com/urielmoreirasilva/ICX532/blob/main/labs_gabs/Laborat%C3%B3rio%202%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados%20%28gabarito%29/Laborat%C3%B3rio%202%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados%20%28gabarito%29.ipynb)

Bem-vindo ao Laboratório 2! Nesta tarefa, aprenderemos mais sobre `array`s, `DataFrame`s, criar visualizações de dados e como escrever funções em Python.

Você deve concluir todo este laboratório e enviá-lo ao Moodle até às 23h59 da data de vencimento.

### Referências
- [BPD: Capítulos 6, 7, 8. 9, 10, 11 e 12](https://notes.dsc10.com/)
- [CIT: Capítulo 6, 7 e 8](https://inferentialthinking.com/)
- Aulas: Tópicos 4, 5, 6 e 7. 

Material adaptado do [DSC10 (UCSD)](https://dsc10.com/) por [Flavio Figueiredo (DCC-UFMG)](https://flaviovdf.io/fcd/) e [Uriel Silva (DEST-UFMG)](https://urielmoreirasilva.github.io)

**<u> NOTA</u>: Não use loops `for` em nenhuma pergunta deste laboratório.** Lembre do Tópico 08 que os loops em Python são lentos, e os loops em `arrays` e `DataFrame`s geralmente devem ser evitados. Como alternativa, devemos idealmente utilizar as funções nativas de bibliotecas como `numpy` e `pandas` para a manipulação desses objetos.


```python
## Imports para esse laboratório
import numpy as np
import pandas as pd

## Opções do MatplotLib 
import matplotlib.pyplot as plt
plt.style.use('ggplot')
plt.rcParams['figure.figsize'] = (10, 5)
```

# 1. Aplicativos da Google Play Store 📲

Neste problema, praticaremos manipulações de DataFrame e visualizações de dados com o [Google Play Store Apps Dataset](https://www.kaggle.com/lava18/google-play-store-apps), extraído da Google Play Store.

Começamos carregando o conjunto de dados de um arquivo `.csv` externo, utilizando o método `pd.csv()`: 


```python
apps = pd.read_csv("https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs_gabs/Laborat%C3%B3rio%202%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados%20%28gabarito%29/data/googleplaystore.csv")
apps
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
      <th>App</th>
      <th>Category</th>
      <th>Rating</th>
      <th>Reviews</th>
      <th>Size</th>
      <th>Installs</th>
      <th>Type</th>
      <th>Price</th>
      <th>Content Rating</th>
      <th>Genres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Photo Editor &amp; Candy Camera &amp; Grid &amp; ScrapBook</td>
      <td>ART_AND_DESIGN</td>
      <td>4.1</td>
      <td>159</td>
      <td>19M</td>
      <td>10000.0</td>
      <td>Free</td>
      <td>0</td>
      <td>Everyone</td>
      <td>Art &amp; Design</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Coloring book moana</td>
      <td>ART_AND_DESIGN</td>
      <td>3.9</td>
      <td>967</td>
      <td>14M</td>
      <td>500000.0</td>
      <td>Free</td>
      <td>0</td>
      <td>Everyone</td>
      <td>Art &amp; Design;Pretend Play</td>
    </tr>
    <tr>
      <th>2</th>
      <td>U Launcher Lite – FREE Live Cool Themes, Hide ...</td>
      <td>ART_AND_DESIGN</td>
      <td>4.7</td>
      <td>87510</td>
      <td>8.7M</td>
      <td>5000000.0</td>
      <td>Free</td>
      <td>0</td>
      <td>Everyone</td>
      <td>Art &amp; Design</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Sketch - Draw &amp; Paint</td>
      <td>ART_AND_DESIGN</td>
      <td>4.5</td>
      <td>215644</td>
      <td>25M</td>
      <td>50000000.0</td>
      <td>Free</td>
      <td>0</td>
      <td>Teen</td>
      <td>Art &amp; Design</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Pixel Draw - Number Art Coloring Book</td>
      <td>ART_AND_DESIGN</td>
      <td>4.3</td>
      <td>967</td>
      <td>2.8M</td>
      <td>100000.0</td>
      <td>Free</td>
      <td>0</td>
      <td>Everyone</td>
      <td>Art &amp; Design;Creativity</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>10820</th>
      <td>Sya9a Maroc - FR</td>
      <td>FAMILY</td>
      <td>4.5</td>
      <td>38</td>
      <td>53M</td>
      <td>5000.0</td>
      <td>Free</td>
      <td>0</td>
      <td>Everyone</td>
      <td>Education</td>
    </tr>
    <tr>
      <th>10821</th>
      <td>Fr. Mike Schmitz Audio Teachings</td>
      <td>FAMILY</td>
      <td>5.0</td>
      <td>4</td>
      <td>3.6M</td>
      <td>100.0</td>
      <td>Free</td>
      <td>0</td>
      <td>Everyone</td>
      <td>Education</td>
    </tr>
    <tr>
      <th>10822</th>
      <td>Parkinson Exercices FR</td>
      <td>MEDICAL</td>
      <td>NaN</td>
      <td>3</td>
      <td>9.5M</td>
      <td>1000.0</td>
      <td>Free</td>
      <td>0</td>
      <td>Everyone</td>
      <td>Medical</td>
    </tr>
    <tr>
      <th>10823</th>
      <td>The SCP Foundation DB fr nn5n</td>
      <td>BOOKS_AND_REFERENCE</td>
      <td>4.5</td>
      <td>114</td>
      <td>Varies with device</td>
      <td>1000.0</td>
      <td>Free</td>
      <td>0</td>
      <td>Mature 17+</td>
      <td>Books &amp; Reference</td>
    </tr>
    <tr>
      <th>10824</th>
      <td>iHoroscope - 2018 Daily Horoscope &amp; Astrology</td>
      <td>LIFESTYLE</td>
      <td>4.5</td>
      <td>398307</td>
      <td>19M</td>
      <td>10000000.0</td>
      <td>Free</td>
      <td>0</td>
      <td>Everyone</td>
      <td>Lifestyle</td>
    </tr>
  </tbody>
</table>
<p>10825 rows × 10 columns</p>
</div>



Cada linha no DataFrame `apps` acima corresponde à um aplicativo. Algumas das colunas nas quais estamos interessados aqui são:
- `'Category'`: Categoria à qual o aplicativo pertence;
- `'Rating'`: Avaliação geral do usuário do aplicativo, de 1 a 5 (no momento da recuperação de dados);
- `'Reviews'`: Número de avaliações do aplicativo (no momento da recuperação dos dados);
- `'Installs'`: Número de downloads/instalações do aplicativo (no momento da recuperação dos dados).
- `'Content Rating'`: Público-alvo do aplicativo.

*<u>Nota</u>: Observe que os conteúdos das colunas `'Rating'` e `'Content Rating'` são bem diferentes!*

Note que aqui não definimos o índice do DataFrame! Embora à primeira vista possa parecer que o nome do aplicativo (coluna `App`) seria um bom candidato para índice, os nomes dos aplicativos *não são exclusivos*! 

Podemos verificar a não-exclusividade da coluna `App` através do método `.unique()`. Quando chamado em uma `Series`, este método retorna um `array` contendo todos os valores distintos da Series, sem duplicatas.


```python
len(apps)
```




    10825




```python
len(apps.get('App').unique())
```




    9644



Vemos na célula de código acima que o DataFrame `apps` possui 10.825 linhas, e logo isso significa que existem 10.825 aplicativos no conjunto de dados. Porém, ao utilizar o método `.unique()`, vemos que apenas 9.644 desses nomes de aplicativos são únicos, o que nos leva a concluir que devem existir nomes duplicados.

#### **Pergunta 1.1.** 

É razoável pensar que, em uma escala de 1 a 5, um aplicativo "típico" deve ter uma classificação de aproximadamente 3.
Complete a célula de código abaixo com um histograma da coluna `'Rating'` para verificar esse raciocínio.


```python
## Descomente e execute!
apps.get("Rating").plot(kind = 'hist',
                        density = True,
                        ec = 'w',
                        bins = 15,
                        figsize = (15, 5));
```


    
![png](Laborat%C3%B3rio%202%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados%20%28gabarito%29_files/Laborat%C3%B3rio%202%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados%20%28gabarito%29_15_0.png)
    


Agora, uma pergunta natural ao analisar o histograma acima é: "será que os aplicativos com classificações mais altas também têm mais avaliações?"

#### **Pergunta 1.2.** 

Que tipo de gráfico você gostaria de criar para ajudar a determinar se os aplicativos com classificação mais alta também têm mais avaliações? Preencha a célula de texto abaixo com a resposta.

**A.** Gráfico de dispersão

**B.** Gráfico de linha

**C.** Gráfico de barras

**D.** Histograma

> **A**

#### **Pergunta 1.3.** 

Na célula de código abaixo, crie o gráfico correspondente à sua resposta da pergunta acima para ajudá-lo a determinar se os aplicativos com classificação mais alta também são os que têm mais avaliações.


```python
## Descomente e execute!
apps.plot(kind = 'scatter', 
          x = 'Reviews', 
          y = 'Rating',
          ec = 'w',
          figsize = (15, 5));
```


    
![png](Laborat%C3%B3rio%202%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados%20%28gabarito%29_files/Laborat%C3%B3rio%202%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados%20%28gabarito%29_20_0.png)
    


#### **Pergunta 1.4.**

Na célula de código abaixo, atribua ao objeto `by_content` um DataFrame contendo o número total de aplicativos em `apps`, organizados (ou "estratificados") por `'Content Rating'`.

*<u>Dica 1</u>: Utilize o método `.groupby()` e depois aplique o método `.count()`, agrupando pela coluna desejada.*

*<u>Dica 2</u>: Para sua saída ficar mais "limpa", antes de agrupar chame `.get` em `apps` com uma lista dos nomes de colunas que você deseja manter.*


```python
## Solução sem aplicar a Dica 2 (colunas redundantes)
by_content = apps.groupby('Content Rating').count()
by_content
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
      <th>App</th>
      <th>Category</th>
      <th>Rating</th>
      <th>Reviews</th>
      <th>Size</th>
      <th>Installs</th>
      <th>Type</th>
      <th>Price</th>
      <th>Genres</th>
    </tr>
    <tr>
      <th>Content Rating</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adults only 18+</th>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
      <td>3</td>
    </tr>
    <tr>
      <th>Everyone</th>
      <td>8702</td>
      <td>8702</td>
      <td>7420</td>
      <td>8702</td>
      <td>8702</td>
      <td>8702</td>
      <td>8702</td>
      <td>8702</td>
      <td>8702</td>
    </tr>
    <tr>
      <th>Everyone 10+</th>
      <td>413</td>
      <td>413</td>
      <td>397</td>
      <td>413</td>
      <td>413</td>
      <td>413</td>
      <td>413</td>
      <td>413</td>
      <td>413</td>
    </tr>
    <tr>
      <th>Mature 17+</th>
      <td>499</td>
      <td>499</td>
      <td>461</td>
      <td>499</td>
      <td>499</td>
      <td>499</td>
      <td>499</td>
      <td>499</td>
      <td>499</td>
    </tr>
    <tr>
      <th>Teen</th>
      <td>1206</td>
      <td>1206</td>
      <td>1084</td>
      <td>1206</td>
      <td>1206</td>
      <td>1206</td>
      <td>1206</td>
      <td>1206</td>
      <td>1206</td>
    </tr>
    <tr>
      <th>Unrated</th>
      <td>2</td>
      <td>2</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>




```python
## Solução escolhendo uma coluna específica (sem redundância)
by_content = apps.get(['App', 'Content Rating']).groupby('Content Rating').count()
by_content
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
      <th>App</th>
    </tr>
    <tr>
      <th>Content Rating</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adults only 18+</th>
      <td>3</td>
    </tr>
    <tr>
      <th>Everyone</th>
      <td>8702</td>
    </tr>
    <tr>
      <th>Everyone 10+</th>
      <td>413</td>
    </tr>
    <tr>
      <th>Mature 17+</th>
      <td>499</td>
    </tr>
    <tr>
      <th>Teen</th>
      <td>1206</td>
    </tr>
    <tr>
      <th>Unrated</th>
      <td>2</td>
    </tr>
  </tbody>
</table>
</div>



#### **Pergunta 1.5.**

Execute a célula de código abaixo para verificar o número de linhas contidas em `apps`. Depois,  na célula de código seguinte, confira se o `DataFrame` que você criou na Pergunta 1.4. tem o número correto de elementos aplicando o método `.sum()`.


```python
## Número de linhas em `apps`
apps.shape[0]
```




    10825




```python
## Número de aplicativos em `by_content`
by_content.sum()
```




    App    10825
    dtype: int64



#### **Pergunta 1.6.**

Na célula de código abaixo, crie um `DataFrame` e atribua-o ao objeto `install_stats`. Esse DataFrame deve possuir uma única coluna, `'Installs'`, contendo o número médio de `'Installs'` para cada tipo de classificação de conteúdo (`'Content Rating'`).

*<u>Dica 1</u>: Utilize novamente o método `.groupby()`, e depois aplique o método `.mean()`, agrupando pela coluna desejada.*

*<u>Dica 2</u>: Note pelo enunciado que nessa pergunta filtrar as colunas antes de aplicar o `.groupby()` é obrigatório, não opcional.*

*<u>Dica 3</u>: Dependendo de como o seu código for estruturado, pode ser que suas respostas sejam exibidas em notação científica.*


```python
install_stats = apps.get(['Content Rating', 'Installs']).groupby('Content Rating').mean()
install_stats
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
      <th>Installs</th>
    </tr>
    <tr>
      <th>Content Rating</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adults only 18+</th>
      <td>6.666667e+05</td>
    </tr>
    <tr>
      <th>Everyone</th>
      <td>1.311844e+07</td>
    </tr>
    <tr>
      <th>Everyone 10+</th>
      <td>3.204330e+07</td>
    </tr>
    <tr>
      <th>Mature 17+</th>
      <td>1.107112e+07</td>
    </tr>
    <tr>
      <th>Teen</th>
      <td>2.878636e+07</td>
    </tr>
    <tr>
      <th>Unrated</th>
      <td>2.525000e+04</td>
    </tr>
  </tbody>
</table>
</div>



#### **Pergunta 1.7.**

Crie na célula de código abaixo um `DataFrame` chamado `top_communication_apps`. Esse DataFrame deve atender às seguintes condições:

1. `'Category'` deve ser igual a `'COMMUNICATION'`;
1. `'Rating'` deve estar entre 4 e 5 (inclusive);
1. O DataFrame deve estar ordenado por `'Rating'`.

*<u>Dica 1</u>: Você pode fazer os filtros/queries/consultas em sequência, ou todos juntos em uma só linha de código utilizando o operador `&` (nesse caso, dentro dos colchetes `[]` é sempre uma boa ideia colocar as condições entre parênteses `()`).*

*<u>Dica 2</u>: A segunda condição pode ser verificada de maneira bem sucinta e "limpa" utilizando o método `.between(a, b)`, que opera elemento-a-elemento em uma `Series` e retorna `True` para cada valor que esteja entre `a` e `b`.*

*<u>Dica 3</u>: Embora você possa simplesmente inspecionar os primeiros e últimos elementos do DataFrame para verificar se a segunda condição foi satisfeita, você também pode analisar a coluna `'Rating'` após chamar `.describe()`. Esse método, quando aplicado a um `DataFrame`, nos fornece um conjunto básico de estatísticas descritivas (incluindo mínimos e máximos) de cada coluna numérica.  


```python
top_communication_apps = apps[(apps.get('Category') == 'COMMUNICATION') & (apps.get('Rating').between(4, 5))]
top_communication_apps = top_communication_apps.sort_values(by = 'Rating')
top_communication_apps
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
      <th>App</th>
      <th>Category</th>
      <th>Rating</th>
      <th>Reviews</th>
      <th>Size</th>
      <th>Installs</th>
      <th>Type</th>
      <th>Price</th>
      <th>Content Rating</th>
      <th>Genres</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>335</th>
      <td>Messenger – Text and Video Chat for Free</td>
      <td>COMMUNICATION</td>
      <td>4.0</td>
      <td>56642847</td>
      <td>Varies with device</td>
      <td>1.000000e+09</td>
      <td>Free</td>
      <td>0</td>
      <td>Everyone</td>
      <td>Communication</td>
    </tr>
    <tr>
      <th>341</th>
      <td>Hangouts</td>
      <td>COMMUNICATION</td>
      <td>4.0</td>
      <td>3419249</td>
      <td>Varies with device</td>
      <td>1.000000e+09</td>
      <td>Free</td>
      <td>0</td>
      <td>Everyone</td>
      <td>Communication</td>
    </tr>
    <tr>
      <th>8490</th>
      <td>DK Browser</td>
      <td>COMMUNICATION</td>
      <td>4.0</td>
      <td>1</td>
      <td>2.4M</td>
      <td>1.000000e+01</td>
      <td>Free</td>
      <td>0</td>
      <td>Everyone</td>
      <td>Communication</td>
    </tr>
    <tr>
      <th>386</th>
      <td>Hangouts</td>
      <td>COMMUNICATION</td>
      <td>4.0</td>
      <td>3419433</td>
      <td>Varies with device</td>
      <td>1.000000e+09</td>
      <td>Free</td>
      <td>0</td>
      <td>Everyone</td>
      <td>Communication</td>
    </tr>
    <tr>
      <th>384</th>
      <td>Hangouts Dialer - Call Phones</td>
      <td>COMMUNICATION</td>
      <td>4.0</td>
      <td>122498</td>
      <td>79k</td>
      <td>1.000000e+07</td>
      <td>Free</td>
      <td>0</td>
      <td>Everyone</td>
      <td>Communication</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>6847</th>
      <td>BV</td>
      <td>COMMUNICATION</td>
      <td>5.0</td>
      <td>3</td>
      <td>1.6M</td>
      <td>1.000000e+02</td>
      <td>Free</td>
      <td>0</td>
      <td>Everyone</td>
      <td>Communication</td>
    </tr>
    <tr>
      <th>7137</th>
      <td>Cb browser</td>
      <td>COMMUNICATION</td>
      <td>5.0</td>
      <td>5</td>
      <td>3.7M</td>
      <td>5.000000e+01</td>
      <td>Free</td>
      <td>0</td>
      <td>Everyone</td>
      <td>Communication</td>
    </tr>
    <tr>
      <th>9444</th>
      <td>EJ messenger</td>
      <td>COMMUNICATION</td>
      <td>5.0</td>
      <td>1</td>
      <td>25M</td>
      <td>1.000000e+01</td>
      <td>Free</td>
      <td>0</td>
      <td>Teen</td>
      <td>Communication</td>
    </tr>
    <tr>
      <th>6722</th>
      <td>BS-Mobile</td>
      <td>COMMUNICATION</td>
      <td>5.0</td>
      <td>1</td>
      <td>683k</td>
      <td>5.000000e+01</td>
      <td>Free</td>
      <td>0</td>
      <td>Everyone</td>
      <td>Communication</td>
    </tr>
    <tr>
      <th>9110</th>
      <td>chat dz</td>
      <td>COMMUNICATION</td>
      <td>5.0</td>
      <td>8</td>
      <td>29M</td>
      <td>1.000000e+02</td>
      <td>Free</td>
      <td>0</td>
      <td>Teen</td>
      <td>Communication</td>
    </tr>
  </tbody>
</table>
<p>268 rows × 10 columns</p>
</div>




```python
top_communication_apps.describe()
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
      <th>Rating</th>
      <th>Reviews</th>
      <th>Installs</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>268.000000</td>
      <td>2.680000e+02</td>
      <td>2.680000e+02</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>4.307090</td>
      <td>3.040149e+06</td>
      <td>1.215079e+08</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.203127</td>
      <td>9.701682e+06</td>
      <td>2.717256e+08</td>
    </tr>
    <tr>
      <th>min</th>
      <td>4.000000</td>
      <td>1.000000e+00</td>
      <td>1.000000e+01</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>4.200000</td>
      <td>7.138000e+03</td>
      <td>5.000000e+05</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>4.300000</td>
      <td>1.247890e+05</td>
      <td>1.000000e+07</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>4.400000</td>
      <td>2.451086e+06</td>
      <td>1.000000e+08</td>
    </tr>
    <tr>
      <th>max</th>
      <td>5.000000</td>
      <td>6.911932e+07</td>
      <td>1.000000e+09</td>
    </tr>
  </tbody>
</table>
</div>



#### **Pergunta 1.8.**

A partir do `DataFrame` criado na Pergunta 1.7., crie na célula de código abaixo um novo `DataFrame`, que deve ser atribuído ao objeto `top_communication_apps_by_content_rating`. Sua estrutura deve ser a seguinte:

1. O DataFrame deve conter o *número de aplicativos* em `top_communication_apps`, *agrupados* por `'Content_Rating'`;
1. O DataFrame deve conter apenas uma coluna, `'Top_Comm_Apps'`;
1. O DataFrame deve ser ordenado por `'Top_Comm_Apps'`, em ordem decrescente.

*<u>Dica 1</u>: Lembre que ao aplicar `.groupby()` pela coluna de interesse e aplicar o método `.count()`, o `DataFrame` resultante naturalmente será indexado pela coluna de interesse, e os valores de todas as colunas serão iguais.*

*<u>Dica 2</u>: Você pode utilizar o método `.drop()` no `DataFrame` resultante com a opção `columns = List` para remover as colunas em uma lista (`List`) de strings que você não deseja manter.*  


```python
top_communication_apps_by_content_rating = top_communication_apps.groupby('Content Rating').count()
top_communication_apps_by_content_rating = top_communication_apps_by_content_rating.assign(Top_Comm_Apps = top_communication_apps_by_content_rating.get('App'))
top_communication_apps_by_content_rating = top_communication_apps_by_content_rating.sort_values('Top_Comm_Apps', ascending = False)
top_communication_apps_by_content_rating = top_communication_apps_by_content_rating.drop(columns = ['App', 'Category', 'Rating', 'Reviews', 'Size', 'Installs', 'Type', 'Price', 'Genres'])
top_communication_apps_by_content_rating
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
      <th>Top_Comm_Apps</th>
    </tr>
    <tr>
      <th>Content Rating</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Everyone</th>
      <td>238</td>
    </tr>
    <tr>
      <th>Teen</th>
      <td>22</td>
    </tr>
    <tr>
      <th>Mature 17+</th>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>



#### **Pergunta 1.9.**

Suponha que um aplicativo seja considerado "bom" se esse aplicativo teve pelo menos um milhão de instalações e uma classificação de pelo menos 4. Atribua na célula de código abaixo à variável `best_category` o nome da categoria com o maior número de aplicativos "bons".

*<u>Dica</u>: Além de utilizar todas as ferramentas acima (inclusive múltiplos filtros), pode ser interessante acessar diretamente o índice do `DataFrame` resultante da consulta adequada através do acessador `.index`. Fazer isso nos permite acessar os elementos do índice através de uma indexação `.index[]` usual, e após um `.sort_values` adequado, o primeiro (ou último) valor de `.index` podem ser escolhidos para cumprir a condição acima.*   


```python
best_category = apps[(apps.get('Installs') >= 1e6) & (apps.get('Rating') >= 4)].groupby('Category').count()
best_category.sort_values('App', ascending = False).index[0]
```




    'GAME'



# 2. Renda dos CEOs 💼

No restante deste laboratório, analisaremos um conjunto de dados que trata da remuneração de 2015 dos Diretores Executivos (CEOs) das 100 maiores empresas da Califórnia. 

Os dados foram compilados para uma análise do [Los Angeles Times ](http://spreadsheets.latimes.com/california-ceo-compensation/) e esse consolidado é basicamente o exigido pela Comissão de Valores Mobiliários dos EUA, que faz a regulamentação de todas as empresas de capital aberto. Duas das empresas em nosso conjunto de dados têm dois CEOs, portanto há 102 CEOs no conjunto de dados.

Copiamos os dados da página do LA Times para um arquivo chamado `raw_compensation.csv`. Na página, os autores deixam explícito que todos os valores estão em *milhões de dólares*.


```python
raw_compensation = pd.read_csv("https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs_gabs/Laborat%C3%B3rio%202%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados%20%28gabarito%29/data/raw_compensation.csv").set_index('Rank')
raw_compensation
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
      <th>Name</th>
      <th>Company (Headquarters)</th>
      <th>Total Pay</th>
      <th>% Change</th>
      <th>Cash Pay</th>
      <th>Equity Pay</th>
      <th>Other Pay</th>
      <th>Ratio of CEO pay to average industry worker pay</th>
    </tr>
    <tr>
      <th>Rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Mark V. Hurd*</td>
      <td>Oracle (Redwood City)</td>
      <td>$53.25</td>
      <td>(No previous year)</td>
      <td>$0.95</td>
      <td>$52.27</td>
      <td>$0.02</td>
      <td>362.00000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Safra A. Catz*</td>
      <td>Oracle (Redwood City)</td>
      <td>$53.24</td>
      <td>(No previous year)</td>
      <td>$0.95</td>
      <td>$52.27</td>
      <td>$0.02</td>
      <td>362.00000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Robert A. Iger</td>
      <td>Walt Disney (Burbank)</td>
      <td>$44.91</td>
      <td>-3%</td>
      <td>$24.89</td>
      <td>$17.28</td>
      <td>$2.74</td>
      <td>477.00000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Marissa A. Mayer</td>
      <td>Yahoo! (Sunnyvale)</td>
      <td>$35.98</td>
      <td>-15%</td>
      <td>$1.00</td>
      <td>$34.43</td>
      <td>$0.55</td>
      <td>342.00000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Marc Benioff</td>
      <td>salesforce.com (San Francisco)</td>
      <td>$33.36</td>
      <td>-16%</td>
      <td>$4.65</td>
      <td>$27.26</td>
      <td>$1.45</td>
      <td>338.00000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>98</th>
      <td>Gregory N. Roberts</td>
      <td>A-Mark Precious Metals (Santa Monica)</td>
      <td>$0.94</td>
      <td>-11%</td>
      <td>$0.93</td>
      <td>$0.00</td>
      <td>$0.02</td>
      <td>17.00000</td>
    </tr>
    <tr>
      <th>99</th>
      <td>Jose L. Laparte</td>
      <td>PriceSmart (San Diego)</td>
      <td>$0.81</td>
      <td>-7%</td>
      <td>$0.71</td>
      <td>$0.00</td>
      <td>$0.10</td>
      <td>32.00000</td>
    </tr>
    <tr>
      <th>100</th>
      <td>Jack Dorsey</td>
      <td>Twitter (San Francisco)</td>
      <td>$0.07</td>
      <td>(No previous year)</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>$0.07</td>
      <td>0.63000</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Elon R. Musk</td>
      <td>Tesla Motors (Palo Alto)</td>
      <td>$0.04</td>
      <td>6%</td>
      <td>$0.04</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>0.46000</td>
    </tr>
    <tr>
      <th>102</th>
      <td>Lawrence Page***</td>
      <td>Alphabet (Mountain View)</td>
      <td>$0.00</td>
      <td>0%</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>0.00001</td>
    </tr>
  </tbody>
</table>
<p>102 rows × 8 columns</p>
</div>



Suponha então que você esteja interessado em calcular a média dos salários dos CEOs. 

A princípio isso parece fácil – descomente e tente executar a célula abaixo.


```python
# ## Descomente e execute!
# raw_compensation.get("Total Pay").mean()
```

Ao executar a célula de código acima, você provavelmente viu um erro. 

Vamos tentar entender por que esse erro ocorreu analisando em mais detalhes os valores na coluna `'Total Pay'`.

#### **Pergunta 2.1.** 

Na célula de código abaixo, utilize a função `type` para definir `total_pay_type` como o tipo do primeiro item da coluna `'Total Pay'`.


```python
total_pay_type = type(raw_compensation.get('Total Pay').iloc[0])
total_pay_type
```




    str



Ao analisar a saída da célula de código acima, entendemos o problema: os valores na coluna `'Total Pay'` são `string`s! 

Não faz sentido calcular a média dos valores de uma string (pois uma string essencialmente armazena texto), então precisamos antes converter esses valores em números.

#### **Pergunta 2.2.** 

Extraia na célula de código abaixo o primeiro valor na coluna `'Total Pay'`. Esse valor corresponde ao salário de 2015 de Mark Hurd, um dos dois CEOs da Oracle em 2015 (lembre que o valor está expresso em *milhões* de dólares). Atribua o valor extraído ao objeto `mark_hurd_pay_string`.


```python
mark_hurd_pay_string = raw_compensation.get('Total Pay').iloc[0]
mark_hurd_pay_string
```




    '$53.25 '



Para convertermos um valor que esteja no formato acima, primeiramente podemos utilizar o método `.strip()` com a opção "`$`" para remover o cifrão:  


```python
"$53.25".strip("$")
```




    '53.25'



Após removermos o cifrão, podemos utilizar a função `float()` para converter a string em um número (mais precisamente um `float`):


```python
float("$53.25".strip("$"))
```




    53.25



Finalmente, como os resultados devem estar em milhões de dólares, multiplicamos o resultado acima por 1 milhão ($10^6$, ou `1e6` em notação científica):


```python
1e6 * float("$53.25".strip("$"))
```




    53250000.0



#### **Pergunta 2.3.**

Utilizando os passos acima, converta na célula de código abaixo a string `mark_hurd_pay_string` em um número expresso *em dólares* (não em milhões) e armazene o resultado na variável `mark_hurd_pay`, cujo tipo deve ser `float`. Atribua o resultado ao objeto `mark_hurd_pay`.


```python
## Aqui utilizamos a notação científica 1e6 = 1.000.000 para evitar erros de digitação :)
mark_hurd_pay = 1e6 * float(mark_hurd_pay_string.strip("$"))
mark_hurd_pay
```




    53250000.0



Suponha agora que você queria calcular o salário médio dos 102 CEOs. Para evitar de copiar e colar o código acima 102 vezes, primeiro vamos criar uma função!

#### **Pergunta 2.4.** 

Defina na célula de código abaixo uma função `convert_pay_string_to_number`, que deve receber como argumento uma `string` (`some_pay_string`) no formato `"$X.XX"` e retornar seu valor em milhões de dólares. Na célula de código seguinte, aplique a sua função à `mark_hurd_pay_string`. O resultado deve ser o mesmo que você obteve anteriormente.


```python
def convert_pay_string_to_number(some_pay_string):
    """Converte uma string como '$100' (em milhões) para um número em dólares."""
    return(1e6 * float(some_pay_string.strip("$")))
```


```python
## Descomente e execute!
convert_pay_string_to_number(mark_hurd_pay_string)
```




    53250000.0



As funções são sempre úteis quando queremos *generalizar* algum comportamento que queremos para quaisquer argumentos que satisfaçam as nossas condições (além de evitar erros de código ao copiar e colar muitas vezes).

Aqui, por exemplo, podemos agora computar o pagamento de Safra Catzs (o 2º CEO em `raw_compensation`) com uma chamada bem mais simples:


```python
convert_pay_string_to_number(raw_compensation.get('Total Pay').iloc[1])
```




    53240000.0



# 3. Aplicando Funções em DataFrames e Series

Um método é extremamente útil quando queremos aplicar uma função *elemento-a-elemento* em uma `Series` é o método `.apply()`.

Essencialmente, `.apply()` recebe uma função como argumento e aplica essa função a cada elemento da `Series` da qual o método é chamado (ou, de maneira mais geral, a cada linha e coluna de um `DataFrame`).

Continuando com nosso exemplo anterior, vamos aplicar nossa função `convert_pay_string_to_number` à coluna `'Total Pay'` do `DataFrame` `raw_compensation`:


```python
raw_compensation.get('Total Pay').apply(convert_pay_string_to_number)
```




    Rank
    1      53250000.0
    2      53240000.0
    3      44910000.0
    4      35980000.0
    5      33360000.0
              ...    
    98       940000.0
    99       810000.0
    100       70000.0
    101       40000.0
    102           0.0
    Name: Total Pay, Length: 102, dtype: float64



Abaixo está uma ilustração do que a chamada acima faz:

<img src="https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs_gabs/Laborat%C3%B3rio%202%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados%20%28gabarito%29/images/apply.png" width=700/>

É importante notar que, ao chamar `.apply()`, especificamos a função sem `()`, isto é, fornecemos `convert_pay_string_to_number` como argumento, e não `convert_pay_string_to_number()`.

#### **Pergunta 3.1.** 

Na célula de código abaixo, refaça a aplicação acima de `.apply()` com a função `convert_pay_string_to_number` à coluna `'Total Pay'` do `DataFrame` `raw_compensation`. Atribua a `Series` resultante ao objeto `total_pay_dollars`.


```python
total_pay_dollars = raw_compensation.get('Total Pay').apply(convert_pay_string_to_number)
total_pay_dollars
```




    Rank
    1      53250000.0
    2      53240000.0
    3      44910000.0
    4      35980000.0
    5      33360000.0
              ...    
    98       940000.0
    99       810000.0
    100       70000.0
    101       40000.0
    102           0.0
    Name: Total Pay, Length: 102, dtype: float64



#### **Pergunta 3.2.** 

Utilizando o resultado da Pergunta 3.1., crie um novo `DataFrame` denominado `compensation`, que deve ser uma cópia de `raw_compensation` e conter uma coluna a mais, `'Total_Pay_Dollars'`, cujo conteúdo deve ser o mesmo do objeto `total_pay_dollars` definido acima.

*<u>Dica</u>: Lembre que `.apply()` retorna uma `Series`, e que `.assign()` pode ser utilizado para adicionar uma `Series` a um `DataFrame` como uma nova coluna.*


```python
compensation = raw_compensation.assign(Total_Pay_Dollars = total_pay_dollars)
compensation
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
      <th>Name</th>
      <th>Company (Headquarters)</th>
      <th>Total Pay</th>
      <th>% Change</th>
      <th>Cash Pay</th>
      <th>Equity Pay</th>
      <th>Other Pay</th>
      <th>Ratio of CEO pay to average industry worker pay</th>
      <th>Total_Pay_Dollars</th>
    </tr>
    <tr>
      <th>Rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Mark V. Hurd*</td>
      <td>Oracle (Redwood City)</td>
      <td>$53.25</td>
      <td>(No previous year)</td>
      <td>$0.95</td>
      <td>$52.27</td>
      <td>$0.02</td>
      <td>362.00000</td>
      <td>53250000.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Safra A. Catz*</td>
      <td>Oracle (Redwood City)</td>
      <td>$53.24</td>
      <td>(No previous year)</td>
      <td>$0.95</td>
      <td>$52.27</td>
      <td>$0.02</td>
      <td>362.00000</td>
      <td>53240000.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Robert A. Iger</td>
      <td>Walt Disney (Burbank)</td>
      <td>$44.91</td>
      <td>-3%</td>
      <td>$24.89</td>
      <td>$17.28</td>
      <td>$2.74</td>
      <td>477.00000</td>
      <td>44910000.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Marissa A. Mayer</td>
      <td>Yahoo! (Sunnyvale)</td>
      <td>$35.98</td>
      <td>-15%</td>
      <td>$1.00</td>
      <td>$34.43</td>
      <td>$0.55</td>
      <td>342.00000</td>
      <td>35980000.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Marc Benioff</td>
      <td>salesforce.com (San Francisco)</td>
      <td>$33.36</td>
      <td>-16%</td>
      <td>$4.65</td>
      <td>$27.26</td>
      <td>$1.45</td>
      <td>338.00000</td>
      <td>33360000.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>98</th>
      <td>Gregory N. Roberts</td>
      <td>A-Mark Precious Metals (Santa Monica)</td>
      <td>$0.94</td>
      <td>-11%</td>
      <td>$0.93</td>
      <td>$0.00</td>
      <td>$0.02</td>
      <td>17.00000</td>
      <td>940000.0</td>
    </tr>
    <tr>
      <th>99</th>
      <td>Jose L. Laparte</td>
      <td>PriceSmart (San Diego)</td>
      <td>$0.81</td>
      <td>-7%</td>
      <td>$0.71</td>
      <td>$0.00</td>
      <td>$0.10</td>
      <td>32.00000</td>
      <td>810000.0</td>
    </tr>
    <tr>
      <th>100</th>
      <td>Jack Dorsey</td>
      <td>Twitter (San Francisco)</td>
      <td>$0.07</td>
      <td>(No previous year)</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>$0.07</td>
      <td>0.63000</td>
      <td>70000.0</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Elon R. Musk</td>
      <td>Tesla Motors (Palo Alto)</td>
      <td>$0.04</td>
      <td>6%</td>
      <td>$0.04</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>0.46000</td>
      <td>40000.0</td>
    </tr>
    <tr>
      <th>102</th>
      <td>Lawrence Page***</td>
      <td>Alphabet (Mountain View)</td>
      <td>$0.00</td>
      <td>0%</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>0.00001</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>102 rows × 9 columns</p>
</div>



Finalmente, com todos os salários em números, podemos realizar operações aritméticas com eles!

#### **Pergunta 3.3.**

Na célula de código abaixo, calcule o salário total médio dos CEOs no conjunto de dados.

*<u>Dica</u>: Obtenha primeiro a coluna desejada de `compensation` utilizando `.get()`, e depois utilize o método `.mean()`.* 


```python
average_total_pay = compensation.get('Total_Pay_Dollars').mean()
average_total_pay
```




    np.float64(11445294.11764706)



Uma outra quantidade na qual podemos estar interessados ao analisar uma situação como essa é no *percentual* do salário de cada CEO que é realmente recebido na forma de *dinheiro*. 

Investigar o comportamento desse percentual pode ser interessante porque a maioria das empresas grandes rotineiramente complementam os pagamentos dos funcionários de alto escalão com ações, capital empresarial, jatos particulares e benefícios similares, etc.

#### **Pergunta 3.4.**

Na célula de código abaixo, utilize `.apply()` e `convert_pay_string_to_number` para converter a coluna `'Cash Pay'` de `compensation` para dólares. Seu resultado será novamente uma `Series`, que deverá ser atribuída ao objeto `cash_pay_dollars`.


```python
cash_pay_dollars = compensation.get('Cash Pay').apply(convert_pay_string_to_number)
cash_pay_dollars
```




    Rank
    1        950000.0
    2        950000.0
    3      24890000.0
    4       1000000.0
    5       4650000.0
              ...    
    98       930000.0
    99       710000.0
    100           0.0
    101       40000.0
    102           0.0
    Name: Cash Pay, Length: 102, dtype: float64



#### **Pergunta 3.5.** 

Utilizando o resultado da Pergunta 3.4., na célula de código abaixo adicione uma coluna denominada `'Cash_Pay_Dollars'` ao DataFrame `compensation`, cujo conteúdo deve ser o mesmo do objeto `cash_pay_dollars`.


```python
compensation = compensation.assign(Cash_Pay_Dollars = cash_pay_dollars)
compensation
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
      <th>Name</th>
      <th>Company (Headquarters)</th>
      <th>Total Pay</th>
      <th>% Change</th>
      <th>Cash Pay</th>
      <th>Equity Pay</th>
      <th>Other Pay</th>
      <th>Ratio of CEO pay to average industry worker pay</th>
      <th>Total_Pay_Dollars</th>
      <th>Cash_Pay_Dollars</th>
    </tr>
    <tr>
      <th>Rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Mark V. Hurd*</td>
      <td>Oracle (Redwood City)</td>
      <td>$53.25</td>
      <td>(No previous year)</td>
      <td>$0.95</td>
      <td>$52.27</td>
      <td>$0.02</td>
      <td>362.00000</td>
      <td>53250000.0</td>
      <td>950000.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Safra A. Catz*</td>
      <td>Oracle (Redwood City)</td>
      <td>$53.24</td>
      <td>(No previous year)</td>
      <td>$0.95</td>
      <td>$52.27</td>
      <td>$0.02</td>
      <td>362.00000</td>
      <td>53240000.0</td>
      <td>950000.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Robert A. Iger</td>
      <td>Walt Disney (Burbank)</td>
      <td>$44.91</td>
      <td>-3%</td>
      <td>$24.89</td>
      <td>$17.28</td>
      <td>$2.74</td>
      <td>477.00000</td>
      <td>44910000.0</td>
      <td>24890000.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Marissa A. Mayer</td>
      <td>Yahoo! (Sunnyvale)</td>
      <td>$35.98</td>
      <td>-15%</td>
      <td>$1.00</td>
      <td>$34.43</td>
      <td>$0.55</td>
      <td>342.00000</td>
      <td>35980000.0</td>
      <td>1000000.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Marc Benioff</td>
      <td>salesforce.com (San Francisco)</td>
      <td>$33.36</td>
      <td>-16%</td>
      <td>$4.65</td>
      <td>$27.26</td>
      <td>$1.45</td>
      <td>338.00000</td>
      <td>33360000.0</td>
      <td>4650000.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>98</th>
      <td>Gregory N. Roberts</td>
      <td>A-Mark Precious Metals (Santa Monica)</td>
      <td>$0.94</td>
      <td>-11%</td>
      <td>$0.93</td>
      <td>$0.00</td>
      <td>$0.02</td>
      <td>17.00000</td>
      <td>940000.0</td>
      <td>930000.0</td>
    </tr>
    <tr>
      <th>99</th>
      <td>Jose L. Laparte</td>
      <td>PriceSmart (San Diego)</td>
      <td>$0.81</td>
      <td>-7%</td>
      <td>$0.71</td>
      <td>$0.00</td>
      <td>$0.10</td>
      <td>32.00000</td>
      <td>810000.0</td>
      <td>710000.0</td>
    </tr>
    <tr>
      <th>100</th>
      <td>Jack Dorsey</td>
      <td>Twitter (San Francisco)</td>
      <td>$0.07</td>
      <td>(No previous year)</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>$0.07</td>
      <td>0.63000</td>
      <td>70000.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Elon R. Musk</td>
      <td>Tesla Motors (Palo Alto)</td>
      <td>$0.04</td>
      <td>6%</td>
      <td>$0.04</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>0.46000</td>
      <td>40000.0</td>
      <td>40000.0</td>
    </tr>
    <tr>
      <th>102</th>
      <td>Lawrence Page***</td>
      <td>Alphabet (Mountain View)</td>
      <td>$0.00</td>
      <td>0%</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>0.00001</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>102 rows × 10 columns</p>
</div>



#### **Pergunta 3.6.** 

Utilizando o resultado da Pergunta 3.5., calcule agora na célula de código abaixo o *percentual* dos salários de cada CEO que era pago em dinheiro. Atribua o resultado (que novamente será uma `Series`) ao objeto `cash_proportion`.

*<u>Dica 1</u>: Lembre que, no DataFrame `compensation`, a coluna `'Total_Pay_Dollars` contém o pagamento **total** de cada CEO, e que a coluna `Cash_Pay_Dollars` contém **apenas a parte** do pagamento total que foi feita **em dinheiro**.*

*<u>Dica 2</u>: Após calcular a proporção correspondente, não se esqueça de multiplicar o resultado por 100!*


```python
cash_proportion = 1e2 * compensation.get('Cash_Pay_Dollars') / compensation.get('Total_Pay_Dollars')
cash_proportion
```




    Rank
    1        1.784038
    2        1.784373
    3       55.421955
    4        2.779322
    5       13.938849
              ...    
    98      98.936170
    99      87.654321
    100      0.000000
    101    100.000000
    102           NaN
    Length: 102, dtype: float64



Observe atentamente a saída na célula acima. 

A última linha da `Series` produzida contém um valor `NaN`, que em inglês significa *Not a Number* (ou, em português, "não é um número").

Para entender o que aconteceu, vamos analisar as últimas linhas do DataFrame `compensation`:


```python
compensation.take(np.arange(-5, 0))
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
      <th>Name</th>
      <th>Company (Headquarters)</th>
      <th>Total Pay</th>
      <th>% Change</th>
      <th>Cash Pay</th>
      <th>Equity Pay</th>
      <th>Other Pay</th>
      <th>Ratio of CEO pay to average industry worker pay</th>
      <th>Total_Pay_Dollars</th>
      <th>Cash_Pay_Dollars</th>
    </tr>
    <tr>
      <th>Rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>98</th>
      <td>Gregory N. Roberts</td>
      <td>A-Mark Precious Metals (Santa Monica)</td>
      <td>$0.94</td>
      <td>-11%</td>
      <td>$0.93</td>
      <td>$0.00</td>
      <td>$0.02</td>
      <td>17.00000</td>
      <td>940000.0</td>
      <td>930000.0</td>
    </tr>
    <tr>
      <th>99</th>
      <td>Jose L. Laparte</td>
      <td>PriceSmart (San Diego)</td>
      <td>$0.81</td>
      <td>-7%</td>
      <td>$0.71</td>
      <td>$0.00</td>
      <td>$0.10</td>
      <td>32.00000</td>
      <td>810000.0</td>
      <td>710000.0</td>
    </tr>
    <tr>
      <th>100</th>
      <td>Jack Dorsey</td>
      <td>Twitter (San Francisco)</td>
      <td>$0.07</td>
      <td>(No previous year)</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>$0.07</td>
      <td>0.63000</td>
      <td>70000.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Elon R. Musk</td>
      <td>Tesla Motors (Palo Alto)</td>
      <td>$0.04</td>
      <td>6%</td>
      <td>$0.04</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>0.46000</td>
      <td>40000.0</td>
      <td>40000.0</td>
    </tr>
    <tr>
      <th>102</th>
      <td>Lawrence Page***</td>
      <td>Alphabet (Mountain View)</td>
      <td>$0.00</td>
      <td>0%</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>0.00001</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



À primeira vista, tudo parece bem normal, até nos darmos conta de que o último CEO (Lawrence Page) recebeu um total de $0$ dólares como pagamento em 2015!

É razoável pensar que uma remuneração de $0$ dólares represente $0\%$ do salário total, *ainda que esse salário seja de $0$ dólares*. Porém, não é assim que a aritmética feita pelos computadores funciona!

Em linhas gerais, alguns tipos de *indeterminação*, como $0 / 0$, $\infty / \infty$ e $+\infty - \infty$, não são avaliados como números pela maior parte de linguagens de programação – por isso o `NaN`.

### Diferenças Percentuais

Vamos na célula abaixo analisar o conteúdo da coluna `'% Change'` em `compensation`. Essa coluna contém a diferença percentual (aumento, se positivo, ou diminuição, se negativo) dos salários dos CEOs, do ano anterior (2014) para o atual (2015).


```python
compensation.get('% Change')
```




    Rank
    1      (No previous year)
    2      (No previous year)
    3                     -3%
    4                    -15%
    5                    -16%
                  ...        
    98                   -11%
    99                    -7%
    100    (No previous year)
    101                    6%
    102                    0%
    Name: % Change, Length: 102, dtype: object



Note que, para os CEOs sem pagamento em 2014, os valores de `'% Change'` são iguais a `'(No previous year)'`. 

Com exceção destes (que usualmente denominamos como *valores faltantes*), o resto dos valores são `string`s, não números. Dessa forma, assim como fizemos anteriormente com a coluna `'Total Pay'`, precisamos fazer um *pré-processamento* em `'% Change'` antes de utilizar seus valores em nossas análises.

#### **Pergunta 3.7.** 

Defina na célula de código abaixo uma função `convert_percentage_string_to_number`, que deve receber como argumento uma `string` (`percentage_string`) no formato `"%XX"` e retornar seu valor em números. Nas 2 células de código seguintes, aplique a sua função às strings correspondentes. O resultado da sua função deve ser o mesmo nas 2 células.

*<u>Dica 1</u>: Utilize novamente `.strip()`, mas converta a string para número utilizando `int()` (ao invés de `float()`) para obter um resultado mais "limpo".*

*<u>Dica 2</u>: Dado o formato de `'% Change'`, aqui não precisamos multiplicar os números por 100.*


```python
def convert_percentage_string_to_number(percentage_string):
    """Converte uma string como '10%' (10 porcento) para o número correspondente."""
    return(int(percentage_string.strip('%')))
```


```python
convert_percentage_string_to_number('6%')
```




    6




```python
convert_percentage_string_to_number(compensation.get('% Change').iloc[100])
```




    6



Agora, antes de aplicarmos sua função `convert_percentage_string_to_number` à coluna `'% Change'` em `compensation`, devemos primeiro eliminar os valores inválidos para essa função, isto é, `'(No previous year)'`.

Para ilustrar porque isso é necessário, descomente e execute a célula de código abaixo. Você deverá ver um erro.


```python
# ## Descomente e execute!
# convert_percentage_string_to_number('(No previous year)')
```

#### **Pergunta 3.8.** 

Crie na célula de código abaixo um novo DataFrame chamado `with_previous_compensation`. Esse `DataFrame` deve ser essencialmente uma cópia de `compensation`, mas com os CEOs `'(No previous year)'` filtrados.


```python
with_previous_compensation = compensation[compensation.get('% Change') != '(No previous year)']
```

#### **Pergunta 3.9.**

Na célula de código abaixo, utilize `.apply()` com `convert_pay_string_to_number` para converter os resultados de `'% Change'` em `with_previous_compensation` para números. Atribua o resultado à uma nova coluna, denominada `'percent_change_numerical'`, ao DataFrame `with_previous_compensation`.

*<u>Dica</u>: Você pode fazer o que se pede em apenas 1 linha de código. Porém, caso prefira, você pode primeiro atribuir o resultado a algum objeto (por exemplo, `percent_change_numerical`) antes de criar a coluna correspondente no DataFrame.*


```python
with_previous_compensation = with_previous_compensation.assign(percent_change_numerical = with_previous_compensation.get('% Change').apply(convert_percentage_string_to_number))
with_previous_compensation
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
      <th>Name</th>
      <th>Company (Headquarters)</th>
      <th>Total Pay</th>
      <th>% Change</th>
      <th>Cash Pay</th>
      <th>Equity Pay</th>
      <th>Other Pay</th>
      <th>Ratio of CEO pay to average industry worker pay</th>
      <th>Total_Pay_Dollars</th>
      <th>Cash_Pay_Dollars</th>
      <th>percent_change_numerical</th>
    </tr>
    <tr>
      <th>Rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>Robert A. Iger</td>
      <td>Walt Disney (Burbank)</td>
      <td>$44.91</td>
      <td>-3%</td>
      <td>$24.89</td>
      <td>$17.28</td>
      <td>$2.74</td>
      <td>477.00000</td>
      <td>44910000.0</td>
      <td>24890000.0</td>
      <td>-3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Marissa A. Mayer</td>
      <td>Yahoo! (Sunnyvale)</td>
      <td>$35.98</td>
      <td>-15%</td>
      <td>$1.00</td>
      <td>$34.43</td>
      <td>$0.55</td>
      <td>342.00000</td>
      <td>35980000.0</td>
      <td>1000000.0</td>
      <td>-15</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Marc Benioff</td>
      <td>salesforce.com (San Francisco)</td>
      <td>$33.36</td>
      <td>-16%</td>
      <td>$4.65</td>
      <td>$27.26</td>
      <td>$1.45</td>
      <td>338.00000</td>
      <td>33360000.0</td>
      <td>4650000.0</td>
      <td>-16</td>
    </tr>
    <tr>
      <th>6</th>
      <td>John H. Hammergren</td>
      <td>McKesson (San Francisco)</td>
      <td>$24.84</td>
      <td>-4%</td>
      <td>$12.10</td>
      <td>$12.37</td>
      <td>$0.37</td>
      <td>222.00000</td>
      <td>24840000.0</td>
      <td>12100000.0</td>
      <td>-4</td>
    </tr>
    <tr>
      <th>7</th>
      <td>John S. Watson</td>
      <td>Chevron (San Ramon)</td>
      <td>$22.04</td>
      <td>-15%</td>
      <td>$4.31</td>
      <td>$14.68</td>
      <td>$3.05</td>
      <td>183.00000</td>
      <td>22040000.0</td>
      <td>4310000.0</td>
      <td>-15</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>97</th>
      <td>David G. Hirz</td>
      <td>Smartæ&amp; Final Stores (Commerce)</td>
      <td>$1.53</td>
      <td>-66%</td>
      <td>$1.50</td>
      <td>$0.00</td>
      <td>$0.04</td>
      <td>26.00000</td>
      <td>1530000.0</td>
      <td>1500000.0</td>
      <td>-66</td>
    </tr>
    <tr>
      <th>98</th>
      <td>Gregory N. Roberts</td>
      <td>A-Mark Precious Metals (Santa Monica)</td>
      <td>$0.94</td>
      <td>-11%</td>
      <td>$0.93</td>
      <td>$0.00</td>
      <td>$0.02</td>
      <td>17.00000</td>
      <td>940000.0</td>
      <td>930000.0</td>
      <td>-11</td>
    </tr>
    <tr>
      <th>99</th>
      <td>Jose L. Laparte</td>
      <td>PriceSmart (San Diego)</td>
      <td>$0.81</td>
      <td>-7%</td>
      <td>$0.71</td>
      <td>$0.00</td>
      <td>$0.10</td>
      <td>32.00000</td>
      <td>810000.0</td>
      <td>710000.0</td>
      <td>-7</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Elon R. Musk</td>
      <td>Tesla Motors (Palo Alto)</td>
      <td>$0.04</td>
      <td>6%</td>
      <td>$0.04</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>0.46000</td>
      <td>40000.0</td>
      <td>40000.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>102</th>
      <td>Lawrence Page***</td>
      <td>Alphabet (Mountain View)</td>
      <td>$0.00</td>
      <td>0%</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>0.00001</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>81 rows × 11 columns</p>
</div>



Vamos agora utilizar a relação entre o salário atual (em 2015) e a mudança percentual do salário anterior para o atual (isto é, de 2014 para 2015) para encontrar os salários anteriores (em 2014) dos CEOs do nosso banco de dados!

Primeiramente, a mudança percentual do salário anterior para o atual (a representada em `'% Change'`) é definida por:

\begin{equation*}
    \Delta \text{salário} (\%) := 100 \cdot \left( \frac{\text{salário}_{2015} - \text{salário}_{2014}}{\text{salário}_{2014}}\right) = 100 \cdot \left( \frac{\text{salário}_{2015}}{\text{salário}_{2014}} - 1 \right) 
\end{equation*}

Dessa forma, manipulando a expressão acima, podemos reescrever

\begin{equation*}
    \text{salário}_{2015} = \text{salário}_{2014} \cdot \left( 1 + \frac{\Delta \text{salário} (\%)}{100} \right) 
\end{equation*}

Como um exemplo numérico, suponha que alguém tenha recebido em 2014 um salário de $\$600$. Se nesse caso a mudança percentual de 2014 para 2015 tiver sido de $\$50\%$, então

\begin{align}
    \text{salário}_{2015} &= \$600 \cdot \left( 1 + \frac{50}{100} \right) \\
    %%
    &= \$600 \cdot (1.5) \\
    %%
    &= $900
\end{align}

Finalmente, manipulando uma última vez a expressão acima, temos

\begin{equation*}
    \text{salário}_{2014} = \frac{\text{salário}_{2015}}{\left( 1 + \frac{\Delta \text{salário} (\%)}{100} \right)}, 
\end{equation*}

e, dessa forma, com base nos valores de $\text{salário}_{2015}$ e $\Delta \text{salário} (\%)$, podemos obter o $\text{salário}_{2014}$.

Voltando ao exemplo numérico acima, se tomarmos agora $\text{salário}_{2015} = \$900$ e $\Delta \text{salário} (\%) = 50\%$, temos então

\begin{align}
    \text{salário}_{2014} &= \frac{\$900}{\left( 1 + \frac{50}{100} \right)} \\
    %%
    &= \frac{\$900}{1.5} \\
    %%
    &= $600
\end{align}

#### **Pergunta 3.10.**

Utilize a expressão acima para calcular o pagamento total dos CEOs em 2014 na célula de código abaixo. Adicione o resultado à uma coluna denominada `'Previous_Total_Pay'` no DataFrame `with_previous_compensation`.

*<u>Dica</u>: Para obter um código mais claro, você pode atribuir cada parte do cálculo a um objeto separado. Deixamos abaixo como exemplo um objeto `previous_total_pay` para receber o cálculo do pagamento de 2014, mas você pode dividir o código em ainda mais objetos se preferir.*


```python
previous_total_pay = with_previous_compensation.get('Total_Pay_Dollars') / (1 + ( with_previous_compensation.get('percent_change_numerical') / 100) )
with_previous_compensation = with_previous_compensation.assign(Previous_Total_Pay = previous_total_pay)
with_previous_compensation
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
      <th>Name</th>
      <th>Company (Headquarters)</th>
      <th>Total Pay</th>
      <th>% Change</th>
      <th>Cash Pay</th>
      <th>Equity Pay</th>
      <th>Other Pay</th>
      <th>Ratio of CEO pay to average industry worker pay</th>
      <th>Total_Pay_Dollars</th>
      <th>Cash_Pay_Dollars</th>
      <th>percent_change_numerical</th>
      <th>Previous_Total_Pay</th>
    </tr>
    <tr>
      <th>Rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>Robert A. Iger</td>
      <td>Walt Disney (Burbank)</td>
      <td>$44.91</td>
      <td>-3%</td>
      <td>$24.89</td>
      <td>$17.28</td>
      <td>$2.74</td>
      <td>477.00000</td>
      <td>44910000.0</td>
      <td>24890000.0</td>
      <td>-3</td>
      <td>4.629897e+07</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Marissa A. Mayer</td>
      <td>Yahoo! (Sunnyvale)</td>
      <td>$35.98</td>
      <td>-15%</td>
      <td>$1.00</td>
      <td>$34.43</td>
      <td>$0.55</td>
      <td>342.00000</td>
      <td>35980000.0</td>
      <td>1000000.0</td>
      <td>-15</td>
      <td>4.232941e+07</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Marc Benioff</td>
      <td>salesforce.com (San Francisco)</td>
      <td>$33.36</td>
      <td>-16%</td>
      <td>$4.65</td>
      <td>$27.26</td>
      <td>$1.45</td>
      <td>338.00000</td>
      <td>33360000.0</td>
      <td>4650000.0</td>
      <td>-16</td>
      <td>3.971429e+07</td>
    </tr>
    <tr>
      <th>6</th>
      <td>John H. Hammergren</td>
      <td>McKesson (San Francisco)</td>
      <td>$24.84</td>
      <td>-4%</td>
      <td>$12.10</td>
      <td>$12.37</td>
      <td>$0.37</td>
      <td>222.00000</td>
      <td>24840000.0</td>
      <td>12100000.0</td>
      <td>-4</td>
      <td>2.587500e+07</td>
    </tr>
    <tr>
      <th>7</th>
      <td>John S. Watson</td>
      <td>Chevron (San Ramon)</td>
      <td>$22.04</td>
      <td>-15%</td>
      <td>$4.31</td>
      <td>$14.68</td>
      <td>$3.05</td>
      <td>183.00000</td>
      <td>22040000.0</td>
      <td>4310000.0</td>
      <td>-15</td>
      <td>2.592941e+07</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>97</th>
      <td>David G. Hirz</td>
      <td>Smartæ&amp; Final Stores (Commerce)</td>
      <td>$1.53</td>
      <td>-66%</td>
      <td>$1.50</td>
      <td>$0.00</td>
      <td>$0.04</td>
      <td>26.00000</td>
      <td>1530000.0</td>
      <td>1500000.0</td>
      <td>-66</td>
      <td>4.500000e+06</td>
    </tr>
    <tr>
      <th>98</th>
      <td>Gregory N. Roberts</td>
      <td>A-Mark Precious Metals (Santa Monica)</td>
      <td>$0.94</td>
      <td>-11%</td>
      <td>$0.93</td>
      <td>$0.00</td>
      <td>$0.02</td>
      <td>17.00000</td>
      <td>940000.0</td>
      <td>930000.0</td>
      <td>-11</td>
      <td>1.056180e+06</td>
    </tr>
    <tr>
      <th>99</th>
      <td>Jose L. Laparte</td>
      <td>PriceSmart (San Diego)</td>
      <td>$0.81</td>
      <td>-7%</td>
      <td>$0.71</td>
      <td>$0.00</td>
      <td>$0.10</td>
      <td>32.00000</td>
      <td>810000.0</td>
      <td>710000.0</td>
      <td>-7</td>
      <td>8.709677e+05</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Elon R. Musk</td>
      <td>Tesla Motors (Palo Alto)</td>
      <td>$0.04</td>
      <td>6%</td>
      <td>$0.04</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>0.46000</td>
      <td>40000.0</td>
      <td>40000.0</td>
      <td>6</td>
      <td>3.773585e+04</td>
    </tr>
    <tr>
      <th>102</th>
      <td>Lawrence Page***</td>
      <td>Alphabet (Mountain View)</td>
      <td>$0.00</td>
      <td>0%</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>$0.00</td>
      <td>0.00001</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0</td>
      <td>0.000000e+00</td>
    </tr>
  </tbody>
</table>
<p>81 rows × 12 columns</p>
</div>



Finalmente, vamos agora calcular a média das remunerações totais de 2014. Para comparação, aqui está a média correspondente de 2015:


```python
average_pay_2015 = compensation.get('Total_Pay_Dollars').mean()
average_pay_2015
```




    np.float64(11445294.11764706)



#### **Pergunta 3.11.** 

Calcule na célula abaixo o salário médio dos CEOs em 2014.

*<u>Dica</u>: Se for copiar e colar o código da célula acima, lembre-se de trocar o DataFrame!* 


```python
average_pay_2014 = with_previous_compensation.get('Previous_Total_Pay').mean()
average_pay_2014
```




    np.float64(11649176.115603436)



# 4. Distribuição de Riqueza 💰

Nas nossas análises anteriores, focamos na remuneração média dos 102 CEOs no nosso conjunto de dados. 

Já vimos em alguns dos tópicos dessa disciplina, porém, que a média muitas vezes não é suficiente para caracterizar completamente uma população/amostra. Mesmo entre indivíduos de alta renda, pode existir concentração da maior parte da renda em um número relativamente pequeno de pessoas. 

Caso isso aconteça ([e esse fenômeno é frequente na análise de distribuições de renda](https://en.wikipedia.org/wiki/Income_distribution)), a distribuição será assimétrica à esquerda, e em geral a média será maior que a mediana, e ambas não serão iguais à moda).

Vamos então visualizar abaixo o comportamento da *distribuição* de renda dos nossos 102 CEOs!

#### **Pergunta 4.1.**

Na célula de código abaixo, elabore um histograma da remuneração (lembre-se: coluna `'Total_Pay_Dollars'`) dos CEOs em `compensation`.


```python
compensation.plot(
    kind = 'hist',
    y = 'Total_Pay_Dollars',
    density = True,
    bins = 10,
    ec = 'w'
);
```


    
![png](Laborat%C3%B3rio%202%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados%20%28gabarito%29_files/Laborat%C3%B3rio%202%20%E2%80%93%20Visualiza%C3%A7%C3%A3o%20de%20Dados%20%28gabarito%29_112_0.png)
    


Analisando o histograma acima, vemos que nossas suspeitas estavam corretas: existe concentração de renda até nos salários dos CEOs mais bem pagos!

Aqui, a renda mediana é igual a:


```python
compensation.get('Total_Pay_Dollars').median()
```




    9910000.0



... e a média é:


```python
compensation.get('Total_Pay_Dollars').mean()
```




    np.float64(11445294.11764706)



Conforme mencionado acima, uma diferença positiva entre média e mediana também é evidência de assimetria à direita. 👍

#### **Pergunta 4.2.** 

Na célula de código abaixo, descubra quantos CEOs ganharam mais de 30 milhões de dólares (pouco menos de 3 vezes a média e pouco mais de 3 vezes a mediana) em 2015.


```python
num_ceos_more_than_30_million = compensation[compensation.get('Total_Pay_Dollars') > 1e6 * 30]
num_ceos_more_than_30_million
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
      <th>Name</th>
      <th>Company (Headquarters)</th>
      <th>Total Pay</th>
      <th>% Change</th>
      <th>Cash Pay</th>
      <th>Equity Pay</th>
      <th>Other Pay</th>
      <th>Ratio of CEO pay to average industry worker pay</th>
      <th>Total_Pay_Dollars</th>
      <th>Cash_Pay_Dollars</th>
    </tr>
    <tr>
      <th>Rank</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Mark V. Hurd*</td>
      <td>Oracle (Redwood City)</td>
      <td>$53.25</td>
      <td>(No previous year)</td>
      <td>$0.95</td>
      <td>$52.27</td>
      <td>$0.02</td>
      <td>362.0</td>
      <td>53250000.0</td>
      <td>950000.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Safra A. Catz*</td>
      <td>Oracle (Redwood City)</td>
      <td>$53.24</td>
      <td>(No previous year)</td>
      <td>$0.95</td>
      <td>$52.27</td>
      <td>$0.02</td>
      <td>362.0</td>
      <td>53240000.0</td>
      <td>950000.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Robert A. Iger</td>
      <td>Walt Disney (Burbank)</td>
      <td>$44.91</td>
      <td>-3%</td>
      <td>$24.89</td>
      <td>$17.28</td>
      <td>$2.74</td>
      <td>477.0</td>
      <td>44910000.0</td>
      <td>24890000.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Marissa A. Mayer</td>
      <td>Yahoo! (Sunnyvale)</td>
      <td>$35.98</td>
      <td>-15%</td>
      <td>$1.00</td>
      <td>$34.43</td>
      <td>$0.55</td>
      <td>342.0</td>
      <td>35980000.0</td>
      <td>1000000.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Marc Benioff</td>
      <td>salesforce.com (San Francisco)</td>
      <td>$33.36</td>
      <td>-16%</td>
      <td>$4.65</td>
      <td>$27.26</td>
      <td>$1.45</td>
      <td>338.0</td>
      <td>33360000.0</td>
      <td>4650000.0</td>
    </tr>
  </tbody>
</table>
</div>



# Linha de chegada 🏁

Parabéns! Você concluiu o Laboratório 2 com sucesso 👏👏👏

Para enviar sua tarefa:

1. Selecione `Kernel -> Restart Kernel and Run All Cells` para garantir que você executou todas as células, incluindo as células de teste.
1. Leia o notebook do começo ao fim com cuidado para ter certeza de que está tudo bem e que todos os testes foram aprovados.
1. Baixe seu notebook usando `File -> Save and Export Notebook As -> HTML` e, em seguida, carregue seu notebook para o Moodle.
