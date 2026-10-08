---
layout: default
title: "Laboratório 1 – Arrays e DataFrames"
parent: "Laboratórios"
nav_order: 1
---
# Laboratório 1 – Arrays e DataFrames [<img src="https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames/images/colag_logo.svg" style="float: right; margin-right: 0%; vertical-align: middle; width: 6.5%;">](https://colab.research.google.com/github/urielmoreirasilva/ICX532/blob/main/labs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames.ipynb) [<img src="https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames/images/github_logo.svg" style="float: right; margin-right: 0%; vertical-align: middle; width: 3.25%;">](https://github.com/urielmoreirasilva/ICX532/blob/main/labs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames.ipynb)

Bem-vindo ao Laboratório 1! Nesta tarefa, aprenderemos mais sobre as propriedades e técnicas de manipulação de arrays e DataFrames.

Você deve concluir todo este laboratório e enviá-lo ao Moodle até às 23h59 da data de vencimento.

### Referências
- [BPD: Capítulos 7 a 9](https://notes.dsc10.com/)
- [CIT: Capítulos 5 e 6](https://inferentialthinking.com/)
- Aulas: Tópicos 1, 2 e 3. 

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

# 1. Arrays

## 1.1 Primeiras Definições

#### **Pergunta 1.1.**

Defina um `array` contendo os números 2, 4 e 6, nessa ordem. Nomeie esse array como `numeros_pares`.


```python
numeros_pares = ...
numeros_pares
```




    Ellipsis



#### **Pergunta 1.2.** 

Crie um `array` contendo os números 0, -1, 1, $\pi$ e $e$, nessa ordem. Nomeie esse array como `outros_numeros`.

*<u> Dica</u>: $\pi$ e $e$ estão disponíveis no módulo `np`, que já foi importado. Uma alternativa aqui seria utilizar `math.pi` para obter $\pi$, mas prefira utilizar `np.pi` aqui, e evite carregar uma biblioteca (isto é, `math`) a mais desnecessariamente. Utilize um raciocínio análogo para $e$.*


```python
outros_numeros = ...
outros_numeros
```




    Ellipsis



#### **Pergunta 1.3.** 

Crie um `array` contendo cinco strings: `"Hello"`, `","`, `" "`, `"world"` e `"!"` (note que o terceiro elemento aqui é simplesmente um espaço único entre aspas). Nomeie esse array como `componentes_hello_world`.

*<u> Nota</u>: Dependendo do seu compilador, IDE e plataforma, ao imprimir `componentes_hello_world`, você pode notar algumas informações extras, como por exemplo `dtype='<U5'`. Essa é apenas a maneira do NumPy informar que os elementos do array são strings. Caso você esteja interessado em saber mais, o `U` significa que esta string está codificada em [unicode](https://en.wikipedia.org/wiki/Unicode), e o `<5` significa que todas as strings no array têm 5 caracteres ou menos.*


```python
componentes_hello_world = ...
componentes_hello_world
```




    Ellipsis



Muitas vezes, em Ciência de Dados, queremos trabalhar com muitos números espaçados uniformemente dentro de algum intervalo. A biblioteca NumPy fornece uma função especial para isso, chamada `arange`. A expressão `np.arange(comeco, fim, espaco)` produz um array com todos os números começando em `comeco`, contando de  `espaco` em `espaco`, e parando logo **antes** de `fim` ser alcançado$^1$.

Por exemplo, o valor de `np.arange(1, 8, 2)` é um array com os elementos `1, 3, 5 e 7`, isto é, começando em 1 e contando de 2 em 2, terminando até chegar no último valor menor que 8 (que é 7). Em outras palavras, essa chamada cria o mesmo array que `np.array([1, 3, 5, 7])`.

$^1$*<u> Nota</u>: Esse comportamento é consistente com a indexação do Python, que se inicia em `0`*.

##### **Pergunta 1.1.4.** 

Use `np.arange` para criar um array com todos os múltiplos de 99 de 0 até (**e incluindo**) 9999. Portanto, seus elementos serão 0, 99, 198, 297, etc.


```python
multiplos_de_99 = ...
multiplos_de_99
```




    Ellipsis



### Leituras de temperatura 🌡️

A NOAA (Administração Nacional Oceânica e Atmosférica dos EUA) opera estações meteorológicas que medem as temperaturas da superfície em diferentes locais dos Estados Unidos. As leituras horárias estão [disponíveis publicamente](http://www.ncdc.noaa.gov/qclcd/QCLCD?prior=N).

Suponha que baixemos todos os dados de horários do site de San Diego, Califórnia, para o mês de dezembro de 2021. Para analisar os dados, queremos saber quando cada leitura foi feita, mas descobrimos que os dados não incluem as datas nem o horário das leituras.

No entanto, sabendo que a primeira leitura foi feita no primeiro instante de dezembro de 2021 (meia-noite do dia 1º de dezembro) e que cada leitura subsequente foi feita exatamente 1 hora após a última, podemos criar uma "grade" de datas e horários para utilizar como referência.

#### **Pergunta 1.5.** 

Crie um `array` com o tempo, *em segundos*, desde o início do mês (isto é, meia-noite do dia 1º de dezembro) em que cada leitura foi feita. Nomeie esse array como `registro_de_leituras`.

*<u>Dica #1</u>: Dezembro tem 31 dias, o que equivale a ($31 \times 24$) horas, ou ($31 \times 24 \times 60 \times 60$) segundos.*

*<u>Dica #2</u>: A função `len` também funciona em arrays. Para checar seus resultados, verifique se seu array `registro_de_leituras` tenha $31 \times 24$ elementos, já que as leituras são feitas de hora em hora durante 31 dias.*


```python
registro_de_leituras = ...
registro_de_leituras
```




    Ellipsis



## 1.2. Indexação

Vamos agora voltar a nossa atenção para um conjunto de dados um pouco mais interessante. A célula de código abaixo cria um array denominado `populacao`, que inclui populações mundiais estimadas em cada ano de **1950** a **2022**. (As estimativas vêm da seguinte [base de dados internacional](https://www.census.gov/data-tools/demo/idb/#/country?COUNTRY_YEAR=2022&COUNTRY_YR_ANIM=2022), mantida pelo US Census Bureau, órgão equivalente ao IBGE do Brasil).

Em vez de digitar os dados manualmente, nós os carregamos de um arquivo armazenado na nuvem chamado `world_population_2022.csv`.


```python
## Veremos em detalhes as particularidades desse tipo de chamada mais adiante;
## -- por enquanto, apenas ignore os detalhes específicos e execute a célula
populacao = pd.read_csv("https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames/data/world_population_2022.csv").get("Population").values
populacao
```




    array([2557619597, 2594942227, 2636777090, 2682060684, 2730237675,
           2782111389, 2835315327, 2891368627, 2948159570, 3000742521,
           3043031253, 3084053711, 3140239653, 3210037409, 3281477826,
           3350773176, 3421097064, 3490825940, 3562887008, 3637819236,
           3713457589, 3791172327, 3867519813, 3943132388, 4017779234,
           4089387557, 4159536915, 4230430893, 4301282222, 4374940345,
           4445975606, 4527418598, 4610620221, 4694937687, 4777055423,
           4862317393, 4949951891, 5040273543, 5131575729, 5222662682,
           5315511894, 5403253915, 5490481497, 5568231516, 5650178207,
           5733211108, 5815333785, 5895837672, 5975189305, 6053955779,
           6132455985, 6211328357, 6290282107, 6369186797, 6448262425,
           6527056809, 6607396274, 6689442159, 6773319540, 6857160919,
           6939761510, 7022084781, 7105001721, 7188528811, 7271598780,
           7353476064, 7435151387, 7516769535, 7597066210, 7676686052,
           7756873419, 7831718605, 7905336896])



Veja abaixo como obtemos o primeiro elemento de `populacao`, que é a população mundial no primeiro ano do conjunto de dados, 1950.


```python
populacao[0]
```




    np.int64(2557619597)



Observe atentamente que na expressão acima utilizamos colchetes `[]`. Os colchetes sinalizam que estamos *acessando* um elemento do array. Colchetes em Python são como os subscritos que utilizamos em matemática para denotar os elementos de uma sequência (por exemplo $x_1$, $x_2$, ...).

O valor da expressão acima é o número $2557619597$ (cerca de 2,5 bilhões), porque é o primeiro elemento do array `populacao`.

É importante notar que aqui escrevemos `populacao[0]`, e não `populacao[1]`, para obter o primeiro elemento. Esta é uma convenção do Python, em que `0` é chamado de *índice* do primeiro item. Seguindo essa lógica, então `1` seria o índice do segundo item, `2` seria o índice do terceiro, e assim por diante.

Abaixo seguem mais alguns exemplos de indexação.

Nesses exemplos, demos nomes às saídas que obtemos como elementos de `populacao`.


```python
## O terceiro elemento do array é a população em 1952
populacao_1952 = populacao[2]
populacao_1952
```




    np.int64(2636777090)




```python
## O décimo terceiro elemento do array é a população em 1962 (que é 1950 + 12)
populacao_1962 = populacao[12]
populacao_1962
```




    np.int64(3140239653)




```python
## O 73º elemento do array é a população em 2022
populacao_2022 = populacao[72]
populacao_2022
```




    np.int64(7905336896)



Como o array `populacao` possui 73 elementos, é impossível acessar um índice maior do que `72`. Note que também é impossível acessar elementos que não sejam números inteiros. 


```python
# ## Descomente e execute!
# populacao_2023 = populacao[73]
# populacao_2023
```


```python
# ## Descomente e execute!
# populacao[1.50]
```

Voltaremos a esse ponto novamente adiante, mas tentar acessar índices negativos (por exemplo `-1`) talvez à primeira vista não reproduza o efeito originalmente esperado.


```python
populacao
```




    array([2557619597, 2594942227, 2636777090, 2682060684, 2730237675,
           2782111389, 2835315327, 2891368627, 2948159570, 3000742521,
           3043031253, 3084053711, 3140239653, 3210037409, 3281477826,
           3350773176, 3421097064, 3490825940, 3562887008, 3637819236,
           3713457589, 3791172327, 3867519813, 3943132388, 4017779234,
           4089387557, 4159536915, 4230430893, 4301282222, 4374940345,
           4445975606, 4527418598, 4610620221, 4694937687, 4777055423,
           4862317393, 4949951891, 5040273543, 5131575729, 5222662682,
           5315511894, 5403253915, 5490481497, 5568231516, 5650178207,
           5733211108, 5815333785, 5895837672, 5975189305, 6053955779,
           6132455985, 6211328357, 6290282107, 6369186797, 6448262425,
           6527056809, 6607396274, 6689442159, 6773319540, 6857160919,
           6939761510, 7022084781, 7105001721, 7188528811, 7271598780,
           7353476064, 7435151387, 7516769535, 7597066210, 7676686052,
           7756873419, 7831718605, 7905336896])




```python
## quando o índice é negativo, contamos na ordem inversa!
## -- dessa forma, o índice [-1] é na verdade o **último** elemento do array
populacao[-1]
```




    np.int64(7905336896)



#### **Pergunta 1.6.** 

Defina abaixo a variável `populacao_1998` para receber a população mundial em 1998. Faça essa declaração obtendo o elemento apropriado de `populacao`.


```python
populacao_1998 = populacao[37]
populacao_1998
```




    np.int64(5040273543)



## 1.3. Iterando sobre os elementos de um array

Arrays são muito úteis para realizar uma mesma operação muitas vezes. Com o uso de arrays, podemos acessar (e operar) em múltiplos elementos de uma vez só!

### Logaritmos

Suponha que estamos interessados na seguinta pergunta sobre a população mundial ao longo do tempo:

> Qual é o tamanho da população em *ordens de magnitude* em cada ano?

As *funções logarítmicas* nos dão uma forma de medir a "ordem de magnitude" de um número. Por exemplo, o logaritmo na base 10 de um número aumenta em 1 cada vez que multiplicamos o número por 10. Dessa forma, esse logaritmo funciona como uma medida de "quantos dígitos decimais" o número possui, ou o "quão grande" esse número é (em ordens de magnitude).

Podemos então tentar responder nossa pergunta utilizando a função `log10` do NumPy, e aplicando essa função à cada elemento do array `populacao`:


```python
magnitude_da_populacao_1950 = np.log10(populacao[0])
magnitude_da_populacao_1951 = np.log10(populacao[1])
magnitude_da_populacao_1952 = np.log10(populacao[2])
magnitude_da_populacao_1953 = np.log10(populacao[3])
```

... e assim em diante.

Porém, isso é altamente ineficiente e repetitivo, o que em muitas situações também pode levar a erros. Com certeza existe uma maneira melhor!

Na verdade, funções como a `log10` do NumPy são bastante flexíveis. Elas podem *não apenas receber *um único elemento* (como `populacao[0]`) de um array como entrada, mas também receber um *array inteiro* como argumento, retornando a operação correspondente aplicada *a cada elemento do array*!

<img src="https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames/images/array_logarithm.jpg">

Damos à esse tipo de aplicação o nome de aplicação *elementwise* (elemento-a-elemento) da função, uma vez que a função então opera separadamente em cada elemento do array em que é chamada.

#### **Pergunta 1.7.**

Use a função `log10` do NumPy para calcular os logaritmos da população mundial em cada ano. Dê ao resultado dessa chamada (um array de 73 elementos) o nome `magnitude_da_populacao`. 

*<u>Dica</u>: É possível fazer isso com apenas uma linha de código.*


```python
magnitude_da_populacao = ...
magnitude_da_populacao
```




    Ellipsis



### Operações aritméticas

As operações aritméticas básicas também funcionam de maneira *elementwise* em arrays!

Por exemplo, podemos dividir a população mundial de cada ano por 1 bilhão (para obter a população correspondente em bilhões) de uma maneira muito simples:


```python
populacao_em_bilhoes = populacao / 1000000000
populacao_em_bilhoes
```




    array([2.5576196 , 2.59494223, 2.63677709, 2.68206068, 2.73023768,
           2.78211139, 2.83531533, 2.89136863, 2.94815957, 3.00074252,
           3.04303125, 3.08405371, 3.14023965, 3.21003741, 3.28147783,
           3.35077318, 3.42109706, 3.49082594, 3.56288701, 3.63781924,
           3.71345759, 3.79117233, 3.86751981, 3.94313239, 4.01777923,
           4.08938756, 4.15953692, 4.23043089, 4.30128222, 4.37494034,
           4.44597561, 4.5274186 , 4.61062022, 4.69493769, 4.77705542,
           4.86231739, 4.94995189, 5.04027354, 5.13157573, 5.22266268,
           5.31551189, 5.40325391, 5.4904815 , 5.56823152, 5.65017821,
           5.73321111, 5.81533378, 5.89583767, 5.9751893 , 6.05395578,
           6.13245598, 6.21132836, 6.29028211, 6.3691868 , 6.44826243,
           6.52705681, 6.60739627, 6.68944216, 6.77331954, 6.85716092,
           6.93976151, 7.02208478, 7.10500172, 7.18852881, 7.27159878,
           7.35347606, 7.43515139, 7.51676953, 7.59706621, 7.67668605,
           7.75687342, 7.8317186 , 7.9053369 ])



Analogamente, podemos fazer o mesmo com as operações de adição (`+`), subtração (`-`), multiplicação (`*`) e exponenciação (`**`). 

Por exemplo, podemos calcular uma gorjeta de vinte por cento em várias contas de restaurante de uma só vez:


```python
contas_dos_restaurantes = np.array([20.12, 39.90, 31.01])
print("Conta dos restaurantes:\t", contas_dos_restaurantes)

gorjetas = 0.2 * contas_dos_restaurantes
print("Gorjetas:\t\t", gorjetas)
```

    Conta dos restaurantes:	 [20.12 39.9  31.01]
    Gorjetas:		 [4.024 7.98  6.202]


<img src="https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames/images/array_multiplication.jpg">

#### **Pergunta 1.8.** 

Suponha que a cobrança total em um restaurante seja a conta original acrescida do valor da gorjeta de 20% (isso significa que podemos simplesmente multiplicar a fatura original por 1.2 para obter a cobrança total). Calcule então a cobrança total de cada conta no array `conta_dos_restaurantes` e dê ao array resultante o nome de `cobrancas_totais`.


```python
cobrancas_totais = ...
cobrancas_totais
```




    Ellipsis



Vamos agora carregar alguns dados para utilizar na próxima pergunta:


```python
mais_contas_de_restaurantes = pd.read_csv("https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames/data/more_restaurant_bills.csv").get("Bill").values
```

#### **Pergunta 1.8.** 

O array `mais_contas_de_restaurantes` contém 100.000 contas de restaurantes! Calcule a cobrança total de cada uma, assumindo novamente uma gorjeta de vinte por cento, e dê ao array resultante o nome `mais_cobrancas_totais`.


```python
mais_cobrancas_totais = ...
mais_cobrancas_totais
```




    Ellipsis



Uma função muito útil da biblioteca NumPy é `.sum`, que toma um único array de números como argumento, e retorna a soma de todos os números desse array.

*<u>Nota</u>: `.sum` retorna um único número, não um array.*

#### **Pergunta 1.9.** 

Qual foi a soma de todas as contas em `mais_contas_de_restaurantes`, **incluindo as gorjetas**?


```python
soma_das_contas = ...
soma_das_contas
```




    Ellipsis



### Potências Binárias

As potências de 2 ($2^0 = 1$, $2^1 = 2$, $2^2 = 4$, etc) surgem com frequência na Ciência da Computação. Um exemplo comum é o armazenamento físico de dados, que usualmente vêm em potências binárias como 64 GB, 128 GB ou 256 GB.

#### **Pergunta 1.10.** 

Use `np.arange` e o operador de exponenciação `**` para criar um array contendo as primeiras 40 potências de 2, começando em $2^0=1$.

*<u>Dica 1</u>: Se seu kernel “morrer” enquanto você executava a célula de código abaixo correspondente, reveja sua solução para essa pergunta. Existe uma resposta incorreta comum para esse problema que tenta criar um array com tantas entradas que o Python simplesmente desiste.*


```python
potencias_de_2 = ...
potencias_de_2
```




    Ellipsis



# 2. DataFrames

## 2.1. Introdução

Em muitas situações, os arrays são úteis para descrever um *único* atributo de uma coleção de objetos. Por exemplo, se considerarmos os estados dos EUA, um array poderia descrever a extensão territorial de cada estado. 

As tabelas são uma extensão natural dos arrays, podendo conter *múltiplas* características de uma coleção de objetos. Nesse exemplo dos estados dos EUA, além da extensão territorial, uma tabela poderia armazenar a população, capital, PIB, etc. de cada estado. Em outras palavras, as tabelas nos permitem descrever diferentes entidades (ou **indivíduos**, armazenados como **linhas**) e, para cada uma dessas entidades, múltiplos atributos (**features**, armazenadas como **colunas**).


Na célula abaixo temos dois arrays. O primeiro contém a população mundial em cada ano (conforme estimado pelo US Census Bureau), e o segundo contém os anos correspondentes (em ordem crescente).


```python
anos = np.arange(1950, 2022+1)
quantidade_populacional = pd.read_csv("https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames/data/world_population_2022.csv").get("Population").values

print("Coluna de população:", quantidade_populacional)
print("Coluna dos anos:", anos)
```

    Coluna de população: [2557619597 2594942227 2636777090 2682060684 2730237675 2782111389
     2835315327 2891368627 2948159570 3000742521 3043031253 3084053711
     3140239653 3210037409 3281477826 3350773176 3421097064 3490825940
     3562887008 3637819236 3713457589 3791172327 3867519813 3943132388
     4017779234 4089387557 4159536915 4230430893 4301282222 4374940345
     4445975606 4527418598 4610620221 4694937687 4777055423 4862317393
     4949951891 5040273543 5131575729 5222662682 5315511894 5403253915
     5490481497 5568231516 5650178207 5733211108 5815333785 5895837672
     5975189305 6053955779 6132455985 6211328357 6290282107 6369186797
     6448262425 6527056809 6607396274 6689442159 6773319540 6857160919
     6939761510 7022084781 7105001721 7188528811 7271598780 7353476064
     7435151387 7516769535 7597066210 7676686052 7756873419 7831718605
     7905336896]
    Coluna dos anos: [1950 1951 1952 1953 1954 1955 1956 1957 1958 1959 1960 1961 1962 1963
     1964 1965 1966 1967 1968 1969 1970 1971 1972 1973 1974 1975 1976 1977
     1978 1979 1980 1981 1982 1983 1984 1985 1986 1987 1988 1989 1990 1991
     1992 1993 1994 1995 1996 1997 1998 1999 2000 2001 2002 2003 2004 2005
     2006 2007 2008 2009 2010 2011 2012 2013 2014 2015 2016 2017 2018 2019
     2020 2021 2022]


Suponha agora que desejamos responder a seguinte pergunta:

> Em que ano a população mundial ultrapassou a marca de 7 bilhões de pessoas?

Tecnicamente, podemos responder à essa pergunta apenas comparando os dois arrays: basta contar a posição onde a população ultrapassa pela primeira vez os 7 bilhões e, em seguida, encontrar o elemento correspondente na matriz de anos.

Na prática, porém, isso é muito pouco eficiente (e naturalmente propenso à múltiplas fontes de erro), e esse é um dos principais motivos pelos quais trabalhamos com tabelas.

Assim como `numpy` fornece arrays, o pacote `pandas` define os `DataFrame`s, que é o nome de `pandas` para *tabelas*. `pandas` é a ferramenta mais popular para se trabalhar com Ciência de Dados em Python.

Podemos importar a biblioteca `pandas` através do seguinte comando:


```python
import pandas as pd
```

Vamosa analisar a célula de código abaixo. Nela,

- criamos um DataFrame vazio invocando a expressão `pd.DataFrame()`;
- atribuímos duas colunas ao DataFrame chamando `assign`;
- atribuímos o DataFrame resultante ao objeto `populacao_df`;
- exibimos `populacao_df` para que possamos ver o DataFrame que criamos.

*<u>Nota</u>:"`Populacao`" e "`Ano`" são rótulos arbitrários. Poderíamos aqui ter escolhido qualquer nome, mas na prática é sempre uma boa ideia dar nomes que sejam descritivos e não muito longos às colunas dos nossos DataFrames.*


```python
populacao_df = pd.DataFrame().assign(
    Populacao = quantidade_populacional,
    Ano = anos
)

populacao_df
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
      <th>Populacao</th>
      <th>Ano</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2557619597</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2594942227</td>
      <td>1951</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2636777090</td>
      <td>1952</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2682060684</td>
      <td>1953</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2730237675</td>
      <td>1954</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>68</th>
      <td>7597066210</td>
      <td>2018</td>
    </tr>
    <tr>
      <th>69</th>
      <td>7676686052</td>
      <td>2019</td>
    </tr>
    <tr>
      <th>70</th>
      <td>7756873419</td>
      <td>2020</td>
    </tr>
    <tr>
      <th>71</th>
      <td>7831718605</td>
      <td>2021</td>
    </tr>
    <tr>
      <th>72</th>
      <td>7905336896</td>
      <td>2022</td>
    </tr>
  </tbody>
</table>
<p>73 rows × 2 columns</p>
</div>



Agora os dados estão todos juntos em um único `DataFrame`! É muito mais fácil analisar esses dados lado-a-lado. Se você precisa saber qual era a população em 2011, por exemplo, basta olhar a linha correspondente.

#### **Pergunta 2.1.** 

Na célula abaixo, criamos 2 `array`s: `top_10_avaliacoes` e `top_10_nomes`. Seguindo as mesmas etapas acima, na célula de código seguinte, atribua ao objeto `top_10_filmes` um `DataFrame` com duas colunas, chamadas `Avaliacao` e `Nome`, contendo os arrays `top_10_avaliacoes` e `top_10_nomes`, respectivamente.


```python
top_10_avaliacoes = np.array([9.2, 9.2, 9., 8.9, 8.9, 8.9, 8.9, 8.9, 8.9, 8.8])
top_10_nomes = np.array([
        'The Shawshank Redemption (1994)',
        'The Godfather (1972)',
        'The Godfather: Part II (1974)',
        'Pulp Fiction (1994)',
        "Schindler's List (1993)",
        'The Lord of the Rings: The Return of the King (2003)',
        '12 Angry Men (1957)',
        'The Dark Knight (2008)',
        'Il buono, il brutto, il cattivo (1966)',
        'The Lord of the Rings: The Fellowship of the Ring (2001)'
])
```


```python
top_10_filmes = pd.DataFrame().assign(
    Avaliacao = top_10_avaliacoes,
    Nome = top_10_nomes
)
top_10_filmes
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
      <th>Avaliacao</th>
      <th>Nome</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>9.2</td>
      <td>The Shawshank Redemption (1994)</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9.2</td>
      <td>The Godfather (1972)</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9.0</td>
      <td>The Godfather: Part II (1974)</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8.9</td>
      <td>Pulp Fiction (1994)</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8.9</td>
      <td>Schindler's List (1993)</td>
    </tr>
    <tr>
      <th>5</th>
      <td>8.9</td>
      <td>The Lord of the Rings: The Return of the King ...</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8.9</td>
      <td>12 Angry Men (1957)</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8.9</td>
      <td>The Dark Knight (2008)</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8.9</td>
      <td>Il buono, il brutto, il cattivo (1966)</td>
    </tr>
    <tr>
      <th>9</th>
      <td>8.8</td>
      <td>The Lord of the Rings: The Fellowship of the R...</td>
    </tr>
  </tbody>
</table>
</div>



Suponha agora que você tenha feito suas próprias avaliações dos filmes acima, contidos no array a seguir:


```python
minhas_avaliacoes = [8, 2, 1, 9, 7, 10, 6, 4, 3, 5]
```

Caso você queira adicionar suas avaliações ao DataFrame `top_10_filmes`, basta utilizar o método `assign` para adicionar o array `minhas_avaliacoes` como uma nova coluna nesse DataFrame. Note que essa foi exatamente a maneira que utilizamos até agora para definir colunas nos `DataFrame`s acima – a única diferença é que nos casos anteriores sempre começamos com um DataFrame vazio.

#### **Pergunta 2.2.** 

Na célula de código abaixo, crie um novo DataFrame chamado `top_10_filmes_com_minhas_avaliacoes` adicionando uma coluna chamada `Minhas_Avaliacoes` ao DataFrame `top_10_filmes`.


```python
top_10_filmes_com_minhas_avaliacoes = ...
top_10_filmes_com_minhas_avaliacoes
```




    Ellipsis



## 2.2. Índices

Você provavelmente deve ter notado que os `DataFrame`s acima contém o que parece ser uma coluna extra e sem rótulo à esquerda, com números que começam em `0`. Na verdade, essa "coluna" não é de fato uma coluna, mas o que chamamos de *índice*. 

Em termos simples, o índice contém os *rótulos das linhas*. Enquanto as colunas deste DataFrame são rotuladas como `"Populacao"` e `"Ano"`, as linhas são rotuladas como 0, 1, ... (lembre que a indexação em Python começa em 0, então em geral o índice vai até `n-1`, onde `n` é o número total de linhas do DataFrame).

Embora na maior parte dos casos tomar simplesmente os números de $0$ até $n-1$ como rótulo das linhas seja perfeitamente razoável, em algumas situações temos candidatos naturais (e geralmente melhores) para os índices.

Por exemplo, no dataset `populacao` (que carregamos anteriormente), uma ótima escolha é tomar a coluna `Ano` como índice:


```python
populacao_por_ano = populacao_df.set_index('Ano')
populacao_por_ano
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
      <th>Populacao</th>
    </tr>
    <tr>
      <th>Ano</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1950</th>
      <td>2557619597</td>
    </tr>
    <tr>
      <th>1951</th>
      <td>2594942227</td>
    </tr>
    <tr>
      <th>1952</th>
      <td>2636777090</td>
    </tr>
    <tr>
      <th>1953</th>
      <td>2682060684</td>
    </tr>
    <tr>
      <th>1954</th>
      <td>2730237675</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>7597066210</td>
    </tr>
    <tr>
      <th>2019</th>
      <td>7676686052</td>
    </tr>
    <tr>
      <th>2020</th>
      <td>7756873419</td>
    </tr>
    <tr>
      <th>2021</th>
      <td>7831718605</td>
    </tr>
    <tr>
      <th>2022</th>
      <td>7905336896</td>
    </tr>
  </tbody>
</table>
<p>73 rows × 1 columns</p>
</div>



Como veremos adiante, definir um índice apropriado muitas vezes nos permite fazer mais do que simplesmente deixar o DataFrame mais bonito!

#### **Pergunta 2.3.** 

Na célula de código abaixo, tome o DataFrame `top_10_filmes` definido anteriormente e crie um novo DataFrame, chamado `top_10_filmes_por_nome`, escolhendo para seu índice a coluna `Nome`.


```python
top_10_filmes_por_nome = ...
top_10_filmes_por_nome
```




    Ellipsis



Ao chamar o método `.index` em um DataFrame, seu índice é retornado na forma de um array:


```python
populacao_por_ano.index
```




    Index([1950, 1951, 1952, 1953, 1954, 1955, 1956, 1957, 1958, 1959, 1960, 1961,
           1962, 1963, 1964, 1965, 1966, 1967, 1968, 1969, 1970, 1971, 1972, 1973,
           1974, 1975, 1976, 1977, 1978, 1979, 1980, 1981, 1982, 1983, 1984, 1985,
           1986, 1987, 1988, 1989, 1990, 1991, 1992, 1993, 1994, 1995, 1996, 1997,
           1998, 1999, 2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009,
           2010, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020, 2021,
           2022],
          dtype='int64', name='Ano')



#### **Pergunta 2.4.** 

Na célula de código abaixo, atribua ao objeto `decimo_filme` o nome do décimo filme em `top_10_filmes_por_nome`.

*<u>Dica 1</u>: Como o índice é essencialmente um array, você pode utilizar colchetes para acessar seus elementos.*

*<u>Dica 2</u>: Lembre-se de que a indexação em Python começa em 0! Dessa forma, o elemento 8 corresponde ao 9º elemento de um array, por exemplo*.


```python
decimo_filme = ...
decimo_filme
```




    Ellipsis



## 2.3 Carregando DataFrames de arquivos externos

Na prática de Ciência de Dados, é mais comum podermos aproveitar de bases de dados que já estejam "prontas", isto é, em geral não precisamos digitar nossos dados manualmente. Ao invés disso, podemos utilizar funções fornecidas no `pandas` para ler dados de arquivos externos.

A função `pd.read_csv()` toma um argumento (um caminho para um arquivo de dados – e que logo é uma `string`) e retorna um `DataFrame`.

*<u>Nota</u>: Embora existam muitos formatos de arquivos de dados, CSV (**comma separated values**, ou "valores separados por vírgulas") é o mais comum.*

#### **Pergunta 2.5.** 

O arquivo `data/imdb.csv` contém informações sobre os 250 filmes mais bem avaliados no IMDb. Carregue-o na célula de código abaixo e atribua-o ao objeto `imdb`.

*<u>Dica</u>: Se você não tiver a pasta local "data" em seu diretório de trabalho, você deve carregar os arquivos da pasta "data" armazenada na nuvem, cuja URL é "https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames/data/"*


```python
imdb = ...
imdb
```




    Ellipsis



Observe as reticências (`...`) acima, no meio do DataFrame. Isso significa que algumas (ou muitas) linhas desse DataFrame foram omitidas. 

*<u>Nota</u>: Esse comportamento pode ser customizado com o comando `pd.set_option('display.max_rows', K)`, onde `K` é o número máximo de linhas que se deseja exibir.*

#### **Pergunta 2.6.** 

Como `imdb` é um conjunto de dados de filmes, faz sentido usar o título de cada filme como rótulo da linha correspondente. Crie então na célula de código abaixo um novo DataFrame chamado `imdb_por_nome`, utilizando o título do filme como índice em `imdb`.


```python
imdb_por_nome = ...
imdb_por_nome
```




    Ellipsis



## 2.4. Series

Suponha agora que estejamos interessados principalmente nas classificações dos filmes em `imdb`. Para extrair apenas esta coluna do DataFrame, utilizamos o método `.get`:


```python
# ## Descomente e execute!
# avaliacoes = imdb_por_nome.get('Rating')
# avaliacoes
```

Observe como não apenas as classificações dos filmes foram retornadas, mas também o nome de cada filme! Isto ocorre *exatamente* porque definimos o título do filme como o índice.

Por outro lado, se tivéssemos chamado a coluna `"Rating"` do DataFrame original (`imdb`, sem índice), teríamos:


```python
# ## Descomente e execute!
# imdb.get('Rating')
```

Esta é uma razão pela qual os índices são muito úteis na prática – eles podem nos fornecem rótulos informativos para os dados!

Agora, à primeira vista, pode parecer que invocar uma coluna utilizando `.get` retorna um DataFrame com uma coluna, mas isso não é verdade.

Ao invés disso, `.get` retorna um tipo especial de objeto, denominado de *Series*:


```python
# ## Descomente e execute!
# type(imdb_por_nome.get('Rating'))
```

Você pode pensar em uma `Series` como um `array`, mas com um índice. 

Enquanto os arrays são sequências simples de números sem rótulos, as Series podem ter rótulos. Isso em geral pode ser muito útil!

Voltando ao exemplo acima, `avaliacoes` agora é uma `Series`, contendo a coluna de classificações de cada um dos filmes em `imdb`. Suponha agora que estejamos interessados então na avaliação de um filme específico: _Alien_. Para retornar essa avaliação, utilizaremos o **acessador** `.loc`, que extrai um valor de uma `Series` em um *local* (valor do índice) específico:


```python
# ## Descomente e execute!
# avaliacoes.loc["Alien"]
```

Note aqui que, na chamada acima, colocamos colchetes (`[]`) em torno de `"Alien"`. Isso se deve ao fato de que `.loc` *não é um método*, mas um *acessador*, o que faz com que `.loc` deva obedecer às regras de indexação do Python.

#### **Pergunta 2.7.** 

Encontre na célula de código abaixo a avaliação do filme _3 Idiotas_ (*3 Idiots*).


```python
avaliacao_de_tres_idiotas = ...
avaliacao_de_tres_idiotas
```




    Ellipsis



Suponha agora que estejamos interessados em saber o *ano* em que o filme _Alien_ foi lançado. Podemos fazer isso obtendo primeiro a coluna dos anos:


```python
# ## Descomente e execute!
# anos = imdb_por_nome.get('Year')
# anos
```

... e então usarmos `.loc` para obter a entrada correta:


```python
# ## Descomente e execute!
# anos.loc['Alien']
```

Uma alternativa mais comum na prática (e que deixa o código mais "limpo") é fazer isso em uma única chamada, *encadeando* as operações:


```python
# ## Descomente e execute!
# imdb_por_nome.get('Year').loc['Alien']
```

Isso funciona porque o Python primeiro avalia `imdb_por_nome.get('Year')` para retornar uma `Series` e, em seguida, avalia `.loc['Alien']` sobre essa Series para retornar o ano correspondente!

#### **Pergunta 2.8.** 

Na célula de código abaixo, encontre a década em que o filme _Gone Girl_ foi lançado. Utilize encadeamento para que seu código ocupe apenas uma linha.

*<u>Dica</u>: O DataFrame `imbd_por_nome` possui uma coluna chamada `"Decade"`.*


```python
decada = ...
decada
```




    Ellipsis



# 3. Analisando DataFrames

Veremos agora que, com apenas alguns métodos dos `DataFrame`s de `pandas`, podemos responder algumas questões bem interessantes sobre o conjunto de dados `imdb`.

#### **Pergunta 3.1.** 

Na célula de código abaixo, utilize o método `.max` aplicado à Series `avaliacoes` para encontrar a maior avaliação dos filmes em `imdb`.


```python
maior_avaliacao = ...
maior_avaliacao
```




    Ellipsis



Agora, se estivermos interessados em saber o *nome* do filme cuja avaliação (`maior_avaliacao`) você encontrou acima, basta aplicar o método `.sort_values` à Series `avaliacoes`, de modo a produzir uma `Series` ordenada:


```python
# ## Descomente e execute!
# avaliacoes.sort_values()
```

Ao analisarmos as duas últimas entradas dessa `Series` ordenada, concluímos então que na verdade existem *dois* filmes com essa avaliação no conjunto de dados: *The Shawshank Redemption* e *The Godfather*.

*<u>Nota</u>: aqui estamos ordenando pelas avaliações, e não pelos rótulos! Dessa forma, os rótulos de cada linha também seguem a ordenação conforme a sua avaliação, e esse é exatamente o comportamento que queremos.*

É importante mencionar aqui que, quando utilizamos o método `sort_values`, a `Series` resultante tem os dados ordenados em ordem *crescente*, isto é, com seus elementos ordenados do menor ao maior. Este é o comportamento padrão de `sort_values`, mas podemos mudar isso especificando um **argumento nomeado** (**keyword**) opcional, `ascending`:  


```python
# ## Descomente e execute!
# avaliacoes.sort_values(ascending = False)
```

De maneira análoga, se invocarmos a função `.sort_values` com `ascending = True`, obteremos o mesmo resultado, como se nunca tívessemos atribuído valor algum a `ascending`.

É exatamente isso que queremos dizer quando dizemos que o comportamento padrão de `sort_values` é classificar em ordem crescente, isto é, tomando `ascending = True`. Como esse é o comportamento padrão, o argumento nomeado `asceding` torna-se *opcional*, e produzimos um comportamento diferente apenas quando especificamos `asceding = False`. Repare que as duas células de código seguintes resutam na mesma saída.


```python
# ## Descomente e execute!
# avaliacoes.sort_values(ascending = True)
```


```python
# ## Descomente e execute!
# avaliacoes.sort_values()
```

Em geral, não só podemos ordenar `Series`, mas também `DataFrames` inteiros! Para fazermos isso, basta especificar a coluna pela qual iremos ordenar:


```python
# ## Descomente e execute!
# imdb_por_nome.sort_values('Rating')
```

De maneira análoga ao que fizemos anteriormente, podemos aqui também especificar que a ordenação deve ser em ordem decrescente:


```python
# ## Descomente e execute!
# imdb_por_nome.sort_values('Rating', ascending = False)
```

Alguns detalhes adicionais sobre a ordenação de `DataFrame`s:

1. O primeiro argumento de `sort_values` é o nome da coluna pela qual iremos ordenar;
1. Se a coluna for composta por `string`s, ela será ordenada em ordem alfabética; se for composta por números, ela será ordenada numericamente;
1. `imdb_por_nome.sort_values("Rating")` retorna um *novo DataFrame* – o DataFrame `imdb_por_nome` não é modificado. Para salvar o resultado dessa chamada, você deve atribuí-lo a um novo objeto;
1. Todas as linhas de um DataFrame são reorganizadas de maneira apropriada quando um DataFrame é ordenado. Esse é exatamente o comportamento desejado – não faria sentido ordenar apenas uma coluna e deixar as outras colunas como estão, pois as características (colunas) dos indivíduos (linhas) representadas na tabela (DataFrame) não seriam mais as mesmas.

#### **Pergunta 3.2.**

Na célula de código abaixo, crie uma versão de `imdb_por_nome` que seja ordenada cronologicamente, com os filmes mais antigos primeiro. Nomeie o DataFrame correspondente como `imdb_ordenado`.

*<u>Dica</u>: verifique acima quais colunas estão disponíveis em `imdb_por_nome`!*


```python
imdb_ordenado = ...
imdb_ordenado
```




    Ellipsis



#### **Pergunta 3.3.** 

Com base na resposta à pergunta anterior, atribua na célula de código abaixo o título do filme mais antigo no conjunto de dados ao objeto `titulo_do_filme_mais_antigo`.

*<u>Dica</u>: Utilize o fato de que o índice é um `array`, e que o índice do `DataFrame` acima pode ser retornado simplesmente chamando `imdb_ordenado.index`.*


```python
titulo_do_filme_mais_antigo = ...
titulo_do_filme_mais_antigo
```




    Ellipsis



Suponha agora que estejamos interessados em obter a avaliação do filme mais antigo no nosso conjunto de dados.

Como já encontramos o rótulo do filme mais antigo (`titulo_do_filme_mais_antigo`) acima, basta então extraírmos a coluna de interesse (`Rating`) e usarmos `.loc`!


```python
# ## Descomente e execute!
# imdb_ordenado.get('Rating').loc[titulo_do_filme_mais_antigo]
```

Uma outra maneira alternativa de fazermos a mesma coisa é utilizar o acessador `.iloc`. 

Enquanto `.loc` procura coisas por *rótulo*, `.iloc` procura elementos por *posição*, de maneira que `.iloc[0]` retorna o primeiro elemento de uma `Series`, `.iloc[1]` o segundo, e assim em diante.


```python
# ## Descomente e execute!
# imdb_ordenado.get('Rating').iloc[0]
```

Em ambos os casos, os resultados acima são equivalentes. Se tívessemos analisado o DataFrame `imdb_ordenado` manualmente e verificado que `The Kid` é o filme mais antigo, chamar `imdb_ordenado.get('Rating').loc['The Kid']` também produziria o mesmo resultado.

Por fim, note que tanto `.loc` quanto `.iloc` podem ser aplicados à um `DataFrame` inteiro, produzindo uma `Series` com as colunas correspondentes:


```python
# ## Descomente e execute!
# imdb_ordenado.loc["The Kid"]
```


```python
# ## Descomente e execute!
# imdb_ordenado.iloc[0]
```

... ou produzindo até um novo `DataFrame`, caso os argumentos de `.loc` e `.iloc` sejam `List`s (ou `array`s): 


```python
# ## Descomente e execute!
# imdb_ordenado.loc[["The Kid", "The Gold Rush"]]
```


```python
# ## Descomente e execute!
# imdb_ordenado.iloc[[0, 1]]
```

#### **Pergunta 3.4.** 

Encontre na célula de código abaixo a avaliação do quinto filme mais antigo no conjunto de dados.

*<u>Dica</u> Utilize `.iloc` na posição correspondente do DataFrame `imdb_ordenado`, filtrando antes pela coluna de interesse.*


```python
avaliacao_do_quinto_filme_mais_antigo = ...
avaliacao_do_quinto_filme_mais_antigo
```




    Ellipsis



# 4. Filtrando DataFrames

Ainda no contexto do conjunto de dados dos filmes (`imdb`), suponha agora que você esteja interessado em filmes da década de 1950. Nesse caso, ordenar o `DataFrame` por ano não ajuda muito, porque a década de 1950 está no "meio" do conjunto. 

Uma alternativa muito útil nesse caso é utilizarmos um recurso das `Series` que nos permite verificar facilmente se cada elemento em uma coluna de um `DataFrame` cumpre com uma condição específica.

Primeiramente, lembre-se que podemos usar `.get` para extrair uma única coluna. O resultado não é um `DataFrame`, mas sim uma `Series`:


```python
# ## Descomente e execute!
# imdb_por_nome.get("Decade")
```

Para cumprir nosso objetivo, um primeiro passo é verificar a condição na qual estamos interessados, isto é, se cada filme foi ou não lançado na década de 1950. 

O Python nos dá uma maneira de verificar se duas coisas são iguais: o **operador de comparação** `==`:


```python
3 == 4
```




    False




```python
3 == 3
```




    True



*<u>Nota</u>: O operador `==` é diferente do operador `=`, que é o **operador de atribuição**.*

Os resultados `True` e `False` acima são exemplos de um tipo de variável que ainda não tínhamos visto nesse curso:


```python
type(True)
```




    bool



O tipo `bool` é um diminutivo de "Boolean", em homenagem ao lógico inglês [George Boole](https://en.wikipedia.org/wiki/George_Boole). 

Dizemos que `True` e `False` são valores **Booleanos**.

Voltando às `Series`, se lembrarmos que uma `Series` é essencialmente um `array`, o operador de comparação `==` pode ser facilmente aplicado *elemento-a-elemento* aos seus elementos, da seguinte forma:


```python
# ## Descomente e execute!
# imdb_por_nome.get("Decade") == 1950
```

A operação acima retorna então uma nova `Series`, que têm valores iguais a `True` apenas para os filmes da década de 1950, e `False` para todos os outros. Dizemos que a `Series` resultante é uma Series de *Booleanos*, ou uma *Series Booleana*.

Para fins didáticos, vamos atribuir o resultado acima à uma `Series` que daremos o nome de `e_da_decada_de_1950`. A ideia é que esse nome possa ser então lido como se fosse uma pergunta, isto é: "(o filme) é da década de 1950"?


```python
# ## Descomente e execute!
# e_da_decada_de_1950 = imdb_por_nome.get("Decade") == 1950
# e_da_decada_de_1950
```

Dessa forma, cada linha nessa `Series` é uma resposta à pergunta "(o filme) é da década de 1950?". 

<u>Exemplos</u>: *The Elephant Man* é da década de 1950? `False`. *All About Eve* é da década de 1950? `True`.

Voltando ao nosso objetivo original, podemos agora usar a Series `e_da_decada_de_1950` para selecionar apenas as linhas de `imdb_por_nome` para as quais a resposta é `True`. A sintaxe para isso é:


```python
# ## Descomente e execute!
# imdb_por_nome[e_da_decada_de_1950]
```

Mais precisamente, o que a chamada `imdb_por_nome[e_da_decada_de_1950]` faz é percorrer `imdb_por_nome` linha por linha, **filtrando** o DataFrame pelas linhas cuja condição especificada é `True` (e ignorando, ou "descartando" as linhas para a qual a condição especificada é `False`).

Uma maneira mais "limpa" e direta de obtermos o mesmo resultado é encadeando as operações acima, sem precisar atribuir a `Series` booleana a um objeto:


```python
# ## Descomente e execute!
# imdb_por_nome[imdb_por_nome.get("Decade") == 1950]
```

O ato de criar um novo `DataFrame` através da seleção de certas linhas que satisfaçam alguma condição é chamado de *query*, ou *consulta*. A chamada `imdb_por_nome[imdb_por_nome.get('Decade') == 1950]` é um exemplo de consulta.

#### **Pergunta 4.1.** 

Crie na célula de código abaixo um `DataFrame` chamado `noventa_e_oito`, contendo os filmes em `imdb` lançados em 1998.

*<u>Dica</u>: Lembre mais uma vez da coluna "Year"!*


```python
noventa_e_oito = ...
noventa_e_oito
```




    Ellipsis



Embora tenhamos acima descrito uma situação mais geral, em que as colunas de uma `Series` satisfaçam "alguma condição", o operador `==` nos permite apenas fazer uma comparação de igualdade *exata*. 

Outros operadores de comparação que poderíamos usar são, por exemplo:

|Operador|Resultado|
|-|-|
|`==`| O objeto à esquerda é *exatamente igual* ao objeto à direita |
|`!=`| O objeto à esquerda *não é igual* ao objeto à direita |
|`>`| O objeto à esquerda é *maior que* o objeto à direita |
|`>=`| O objeto à esquerda é *maior ou igual* ao objeto à direita |
|`<`| O objeto à esquerda é *menor que* o objeto à direita |
|`<=`| O objeto à esquerda é *menor ou igual* ao objeto à direita |

As [notas do DSC10](https://notes.dsc10.com/02-data_sets/querying.html#examples) contém alguns outros exemplos de operadores de comparação.

#### **Pergunta 4.2.** 

Utilizando os operadores da tabela acima, encontre na célula de código abaixo todos os filmes com avaliação superior a 8,6. Atribua o `DataFrame` com os filmes correspondentes ao objeto `realmente_bem_avaliados`.


```python
realmente_bem_avaliados = ...
realmente_bem_avaliados
```




    Ellipsis



Com base em tudo o que vimos acima, podemos agora responder a perguntas mais elaboradas, como: "Qual é a maior avaliação que um filme teve década de 1990?"

Primeiramente, verificamos quais filmes são da década de 1990:


```python
# ## Descomente e execute!
# e_da_decada_de_1990 = imdb_por_nome.get("Decade") == 1990
# e_da_decada_de_1990
```

Em seguida, filtramos apenas por estes filmes em nosso `DataFrame`:


```python
# ## Descomente e execute!
# filmes_da_decada_de_1990 = imdb_por_nome[e_da_decada_de_1990]
# filmes_da_decada_de_1990
```

Encontramos então a maior avaliação apenas entre esses filmes:


```python
# ## Descomente e execute!
# filmes_da_decada_de_1990.get('Rating').max()
```

Finalmente, podemos fazer tudo isso de forma mais concisa utilizando encadeamento:


```python
# ## Descomente e execute!
# imdb_por_nome[imdb_por_nome.get('Decade') == 1990].get('Rating').max()
```

Outro exemplo interessante é se lembrarmos da nossa pergunta anterior de qual é o filme mais antigo em `imdb`. Podemos responder à essa pergunta também com uma linha, mas agora utilizando o método `.min()`:


```python
# ## Descomente e execute!
# imdb_por_nome[imdb_por_nome.get("Year") == imdb_por_nome.get("Year").min()]
```

#### **Pergunta 4.3.**

Nas células de códigos abaixo, utilize o método `.mean()` para encontrar a avaliação média para filmes lançados no século 20 e a avaliação média para filmes lançados no século 21 para os filmes em `imdb`.

*<u>Dica</u>: Lembre que o ano 2000 faz parte do século 20, e que o filme mais antigo do conjunto de dados é de 1921!*


```python
avaliacao_media_do_seculo_20 = ...
avaliacao_media_do_seculo_20
```




    Ellipsis




```python
avaliacao_media_do_seculo_21 = ...
avaliacao_media_do_seculo_21
```




    Ellipsis



Uma outra quantidade interessante nesse contexto é a propriedade `shape`, que nos informa *quantas linhas* e *quantas colunas* existem em um `DataFrame`. 


```python
# ## Descomente e execute!
# imdb_por_nome.shape
```

Tecnicamente, uma *propriedade* é similar à um método que não precisa ser chamado adicionando parênteses, e seu tipo é `tuple` (*tuple*, ou *tupla*):


```python
# ## Descomente e execute!
# type(imdb_por_nome.shape)
```

Assim como um array, você pode obter o primeiro elemento da tupla `shape` utilizando `[0]` e o segundo elemento usando `[1]`. 

*<u>Nota</u>: Os `DataFrames` possuem apenas linhas e colunas, mas existem `array`s com mais de duas dimensões. Nesses casos, `.shape` terá um número de elementos igual ao número de dimensões do objeto correspondente.*

Por exemplo, podemos obter o número de linhas em `imdb_por_nome` acessando:


```python
# ## Descomente e execute!
# imdb_por_nome.shape[0]
```

Naturalmente, podemos utilizar esse artifício para descobrir *quantos elementos* (ou, mais precisamente, *quantas linhas*) de um `DataFrame` satisfazem uma certa condição!

Por exemplo, em `imdb`, "Quantos filmes são do século 20?":


```python
# ## Descomente e execute!
# imdb_por_nome[imdb_por_nome.get("Year") <= 2000].shape[0]
```

*<u>Nota</u>: Um erro comum nesse contexto é **esquecer de filtrar o `DataFrame` antes de avaliar seu shape**. Nesse caso, se aplicarmos `.shape` à `Series` booleana, teremos o mesmo número de linhas do DataFrame original!*


```python
# ## Descomente e execute!
# series_bool = imdb_por_nome.get("Year") <= 2000
# series_bool
```


```python
# ## Descomente e execute!
# series_bool.shape[0]
```

#### **Pergunta 4.4.** 

Nas células de código abaixo, utilize `.shape` (e um pouco de aritmética) para encontrar a *proporção* de filmes no conjunto de dados que foram lançados no século 20, e a proporção análoga no século 21.

*<u>Dica 1</u>: A proporção de filmes lançados no século 20 é igual ao número de filmes lançados no século 20, dividido pelo *número total* de filmes no conjunto de dados.*

*<u>Dica 2</u>: Como só existem essas duas possibilidades (século 20 e 21) em `imdb`, a soma de ambas as proporções deve ser igual a 1!*


```python
proporcao_do_seculo_20 = ...
proporcao_do_seculo_20
```




    Ellipsis




```python
proporcao_do_seculo_21 = ...
proporcao_do_seculo_21
```




    Ellipsis



#### **Pergunta 4.5.**

Finalmente, vamos revisitar o DataFrame `populacao_por_ano`, que analisamos no início do laboratório! Na célula de código abaixo, encontre o ano em que a população mundial ultrapassou pela primeira vez os 7 bilhões.

*<u>Dica 1</u>: O índice de `populacao_por_ano` é o ano correspondente, então ao filtrarmos a coluna `Populacao` pela condição de interesse, você pode acessar o índice com `.index`.*

*<u>Dica 2</u>: Tanto a coluna `Populacao` quanto o índice `Ano` já estão ordenados em ordem crescente, então você pode fazer o que se pede utilizando o método `.min()` na Series filtrada.*

*<u>Dica 3</u>: Para evitar escrever o número `7` com nove `0`s, você pode utilizar a notação científica `7e9` para representar 7 bilhões. Embora tecnicamente `7e9` seja um `float` e não um `int`, a comparação produz o mesmo resultado em ambos os casos.*


```python
ano_que_a_populacao_ultrapassou_7_bilhoes = ...
ano_que_a_populacao_ultrapassou_7_bilhoes
```




    Ellipsis



# Linha de chegada 🏁

Parabéns! Você concluiu o Laboratório 1 com sucesso 👏👏👏

Para enviar sua tarefa:

1. Selecione `Kernel -> Restart Kernel and Run All Cells` para garantir que você executou todas as células, incluindo as células de teste.
1. Leia o notebook do começo ao fim com cuidado para ter certeza de que está tudo bem e que todos os testes foram aprovados.
1. Baixe seu notebook usando `File -> Save and Export Notebook As -> HTML` e, em seguida, carregue seu notebook para o Moodle.
