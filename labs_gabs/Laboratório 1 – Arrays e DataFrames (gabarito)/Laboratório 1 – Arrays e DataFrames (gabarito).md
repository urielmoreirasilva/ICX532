---
layout: default
title: "Laboratório 1 – Arrays e DataFrames"
parent: "Gabaritos"
nav_order: 1
---
# Laboratório 1 – Arrays e DataFrames (gabarito) [<img src="https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs_gabs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames%20%28gabarito%29/images/colag_logo.svg" style="float: right; margin-right: 0%; vertical-align: middle; width: 6.5%;">](https://colab.research.google.com/github/urielmoreirasilva/ICX532/blob/main/labs_gabs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames%20%28gabarito%29/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames%20%28gabarito%29.ipynb) [<img src="https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs_gabs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames%20%28gabarito%29/images/github_logo.svg" style="float: right; margin-right: 0%; vertical-align: middle; width: 3.25%;">](https://github.com/urielmoreirasilva/ICX532/blob/main/labs_gabs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames%20%28gabarito%29/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames%20%28gabarito%29.ipynb)

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
numeros_pares = [2, 4, 6]
numeros_pares
```




    [2, 4, 6]



#### **Pergunta 1.2.** 

Crie um `array` contendo os números 0, -1, 1, $\pi$ e $e$, nessa ordem. Nomeie esse array como `outros_numeros`.

*<u> Dica</u>: $\pi$ e $e$ estão disponíveis no módulo `np`, que já foi importado. Uma alternativa aqui seria utilizar `math.pi` para obter $\pi$, mas prefira utilizar `np.pi` aqui, e evite carregar uma biblioteca (isto é, `math`) a mais desnecessariamente. Utilize um raciocínio análogo para $e$.*


```python
outros_numeros = [0, -1, 1, np.pi, np.e]
outros_numeros
```




    [0, -1, 1, 3.141592653589793, 2.718281828459045]



#### **Pergunta 1.3.** 

Crie um `array` contendo cinco strings: `"Hello"`, `","`, `" "`, `"world"` e `"!"` (note que o terceiro elemento aqui é simplesmente um espaço único entre aspas). Nomeie esse array como `componentes_hello_world`.

*<u> Nota</u>: Dependendo do seu compilador, IDE e plataforma, ao imprimir `componentes_hello_world`, você pode notar algumas informações extras, como por exemplo `dtype='<U5'`. Essa é apenas a maneira do NumPy informar que os elementos do array são strings. Caso você esteja interessado em saber mais, o `U` significa que esta string está codificada em [unicode](https://en.wikipedia.org/wiki/Unicode), e o `<5` significa que todas as strings no array têm 5 caracteres ou menos.*


```python
componentes_hello_world = ["Hello", ",", " ", "world", "!"]
componentes_hello_world
```




    ['Hello', ',', ' ', 'world', '!']



Muitas vezes, em Ciência de Dados, queremos trabalhar com muitos números espaçados uniformemente dentro de algum intervalo. A biblioteca NumPy fornece uma função especial para isso, chamada `arange`. A expressão `np.arange(comeco, fim, espaco)` produz um array com todos os números começando em `comeco`, contando de  `espaco` em `espaco`, e parando logo **antes** de `fim` ser alcançado$^1$.

Por exemplo, o valor de `np.arange(1, 8, 2)` é um array com os elementos `1, 3, 5 e 7`, isto é, começando em 1 e contando de 2 em 2, terminando até chegar no último valor menor que 8 (que é 7). Em outras palavras, essa chamada cria o mesmo array que `np.array([1, 3, 5, 7])`.

$^1$*<u> Nota</u>: Esse comportamento é consistente com a indexação do Python, que se inicia em `0`*.

##### **Pergunta 1.1.4.** 

Use `np.arange` para criar um array com todos os múltiplos de 99 de 0 até (**e incluindo**) 9999. Portanto, seus elementos serão 0, 99, 198, 297, etc.


```python
## Resposta usual (calcula-se antes 9999 + 99 = 10098, e coloca-se esse número no final)
multiplos_de_99 = np.arange(0, 10098, 99)
multiplos_de_99
```




    array([   0,   99,  198,  297,  396,  495,  594,  693,  792,  891,  990,
           1089, 1188, 1287, 1386, 1485, 1584, 1683, 1782, 1881, 1980, 2079,
           2178, 2277, 2376, 2475, 2574, 2673, 2772, 2871, 2970, 3069, 3168,
           3267, 3366, 3465, 3564, 3663, 3762, 3861, 3960, 4059, 4158, 4257,
           4356, 4455, 4554, 4653, 4752, 4851, 4950, 5049, 5148, 5247, 5346,
           5445, 5544, 5643, 5742, 5841, 5940, 6039, 6138, 6237, 6336, 6435,
           6534, 6633, 6732, 6831, 6930, 7029, 7128, 7227, 7326, 7425, 7524,
           7623, 7722, 7821, 7920, 8019, 8118, 8217, 8316, 8415, 8514, 8613,
           8712, 8811, 8910, 9009, 9108, 9207, 9306, 9405, 9504, 9603, 9702,
           9801, 9900, 9999])




```python
## Resposta alternativa #1 (mais simples)
multiplos_de_99 = np.arange(0, 9999 + 99, 99)
multiplos_de_99
```




    array([   0,   99,  198,  297,  396,  495,  594,  693,  792,  891,  990,
           1089, 1188, 1287, 1386, 1485, 1584, 1683, 1782, 1881, 1980, 2079,
           2178, 2277, 2376, 2475, 2574, 2673, 2772, 2871, 2970, 3069, 3168,
           3267, 3366, 3465, 3564, 3663, 3762, 3861, 3960, 4059, 4158, 4257,
           4356, 4455, 4554, 4653, 4752, 4851, 4950, 5049, 5148, 5247, 5346,
           5445, 5544, 5643, 5742, 5841, 5940, 6039, 6138, 6237, 6336, 6435,
           6534, 6633, 6732, 6831, 6930, 7029, 7128, 7227, 7326, 7425, 7524,
           7623, 7722, 7821, 7920, 8019, 8118, 8217, 8316, 8415, 8514, 8613,
           8712, 8811, 8910, 9009, 9108, 9207, 9306, 9405, 9504, 9603, 9702,
           9801, 9900, 9999])




```python
## Resposta alternativa #2 (mais comum na prática)
multiplos_de_99 = np.arange(0, 9999 + 1, 99)
multiplos_de_99
```




    array([   0,   99,  198,  297,  396,  495,  594,  693,  792,  891,  990,
           1089, 1188, 1287, 1386, 1485, 1584, 1683, 1782, 1881, 1980, 2079,
           2178, 2277, 2376, 2475, 2574, 2673, 2772, 2871, 2970, 3069, 3168,
           3267, 3366, 3465, 3564, 3663, 3762, 3861, 3960, 4059, 4158, 4257,
           4356, 4455, 4554, 4653, 4752, 4851, 4950, 5049, 5148, 5247, 5346,
           5445, 5544, 5643, 5742, 5841, 5940, 6039, 6138, 6237, 6336, 6435,
           6534, 6633, 6732, 6831, 6930, 7029, 7128, 7227, 7326, 7425, 7524,
           7623, 7722, 7821, 7920, 8019, 8118, 8217, 8316, 8415, 8514, 8613,
           8712, 8811, 8910, 9009, 9108, 9207, 9306, 9405, 9504, 9603, 9702,
           9801, 9900, 9999])



### Leituras de temperatura 🌡️

A NOAA (Administração Nacional Oceânica e Atmosférica dos EUA) opera estações meteorológicas que medem as temperaturas da superfície em diferentes locais dos Estados Unidos. As leituras horárias estão [disponíveis publicamente](http://www.ncdc.noaa.gov/qclcd/QCLCD?prior=N).

Suponha que baixemos todos os dados de horários do site de San Diego, Califórnia, para o mês de dezembro de 2021. Para analisar os dados, queremos saber quando cada leitura foi feita, mas descobrimos que os dados não incluem as datas nem o horário das leituras.

No entanto, sabendo que a primeira leitura foi feita no primeiro instante de dezembro de 2021 (meia-noite do dia 1º de dezembro) e que cada leitura subsequente foi feita exatamente 1 hora após a última, podemos criar uma "grade" de datas e horários para utilizar como referência.

#### **Pergunta 1.5.** 

Crie um `array` com o tempo, *em segundos*, desde o início do mês (isto é, meia-noite do dia 1º de dezembro) em que cada leitura foi feita. Nomeie esse array como `registro_de_leituras`.

*<u>Dica #1</u>: Dezembro tem 31 dias, o que equivale a ($31 \times 24$) horas, ou ($31 \times 24 \times 60 \times 60$) segundos.*

*<u>Dica #2</u>: A função `len` também funciona em arrays. Para checar seus resultados, verifique se seu array `registro_de_leituras` tenha $31 \times 24$ elementos, já que as leituras são feitas de hora em hora durante 31 dias.*


```python
## Uma solução possível: cada hora tem 3600 segundos
registro_de_leituras = np.arange(0, 31 * 24 * 3600, 3600)
registro_de_leituras
```




    array([      0,    3600,    7200,   10800,   14400,   18000,   21600,
             25200,   28800,   32400,   36000,   39600,   43200,   46800,
             50400,   54000,   57600,   61200,   64800,   68400,   72000,
             75600,   79200,   82800,   86400,   90000,   93600,   97200,
            100800,  104400,  108000,  111600,  115200,  118800,  122400,
            126000,  129600,  133200,  136800,  140400,  144000,  147600,
            151200,  154800,  158400,  162000,  165600,  169200,  172800,
            176400,  180000,  183600,  187200,  190800,  194400,  198000,
            201600,  205200,  208800,  212400,  216000,  219600,  223200,
            226800,  230400,  234000,  237600,  241200,  244800,  248400,
            252000,  255600,  259200,  262800,  266400,  270000,  273600,
            277200,  280800,  284400,  288000,  291600,  295200,  298800,
            302400,  306000,  309600,  313200,  316800,  320400,  324000,
            327600,  331200,  334800,  338400,  342000,  345600,  349200,
            352800,  356400,  360000,  363600,  367200,  370800,  374400,
            378000,  381600,  385200,  388800,  392400,  396000,  399600,
            403200,  406800,  410400,  414000,  417600,  421200,  424800,
            428400,  432000,  435600,  439200,  442800,  446400,  450000,
            453600,  457200,  460800,  464400,  468000,  471600,  475200,
            478800,  482400,  486000,  489600,  493200,  496800,  500400,
            504000,  507600,  511200,  514800,  518400,  522000,  525600,
            529200,  532800,  536400,  540000,  543600,  547200,  550800,
            554400,  558000,  561600,  565200,  568800,  572400,  576000,
            579600,  583200,  586800,  590400,  594000,  597600,  601200,
            604800,  608400,  612000,  615600,  619200,  622800,  626400,
            630000,  633600,  637200,  640800,  644400,  648000,  651600,
            655200,  658800,  662400,  666000,  669600,  673200,  676800,
            680400,  684000,  687600,  691200,  694800,  698400,  702000,
            705600,  709200,  712800,  716400,  720000,  723600,  727200,
            730800,  734400,  738000,  741600,  745200,  748800,  752400,
            756000,  759600,  763200,  766800,  770400,  774000,  777600,
            781200,  784800,  788400,  792000,  795600,  799200,  802800,
            806400,  810000,  813600,  817200,  820800,  824400,  828000,
            831600,  835200,  838800,  842400,  846000,  849600,  853200,
            856800,  860400,  864000,  867600,  871200,  874800,  878400,
            882000,  885600,  889200,  892800,  896400,  900000,  903600,
            907200,  910800,  914400,  918000,  921600,  925200,  928800,
            932400,  936000,  939600,  943200,  946800,  950400,  954000,
            957600,  961200,  964800,  968400,  972000,  975600,  979200,
            982800,  986400,  990000,  993600,  997200, 1000800, 1004400,
           1008000, 1011600, 1015200, 1018800, 1022400, 1026000, 1029600,
           1033200, 1036800, 1040400, 1044000, 1047600, 1051200, 1054800,
           1058400, 1062000, 1065600, 1069200, 1072800, 1076400, 1080000,
           1083600, 1087200, 1090800, 1094400, 1098000, 1101600, 1105200,
           1108800, 1112400, 1116000, 1119600, 1123200, 1126800, 1130400,
           1134000, 1137600, 1141200, 1144800, 1148400, 1152000, 1155600,
           1159200, 1162800, 1166400, 1170000, 1173600, 1177200, 1180800,
           1184400, 1188000, 1191600, 1195200, 1198800, 1202400, 1206000,
           1209600, 1213200, 1216800, 1220400, 1224000, 1227600, 1231200,
           1234800, 1238400, 1242000, 1245600, 1249200, 1252800, 1256400,
           1260000, 1263600, 1267200, 1270800, 1274400, 1278000, 1281600,
           1285200, 1288800, 1292400, 1296000, 1299600, 1303200, 1306800,
           1310400, 1314000, 1317600, 1321200, 1324800, 1328400, 1332000,
           1335600, 1339200, 1342800, 1346400, 1350000, 1353600, 1357200,
           1360800, 1364400, 1368000, 1371600, 1375200, 1378800, 1382400,
           1386000, 1389600, 1393200, 1396800, 1400400, 1404000, 1407600,
           1411200, 1414800, 1418400, 1422000, 1425600, 1429200, 1432800,
           1436400, 1440000, 1443600, 1447200, 1450800, 1454400, 1458000,
           1461600, 1465200, 1468800, 1472400, 1476000, 1479600, 1483200,
           1486800, 1490400, 1494000, 1497600, 1501200, 1504800, 1508400,
           1512000, 1515600, 1519200, 1522800, 1526400, 1530000, 1533600,
           1537200, 1540800, 1544400, 1548000, 1551600, 1555200, 1558800,
           1562400, 1566000, 1569600, 1573200, 1576800, 1580400, 1584000,
           1587600, 1591200, 1594800, 1598400, 1602000, 1605600, 1609200,
           1612800, 1616400, 1620000, 1623600, 1627200, 1630800, 1634400,
           1638000, 1641600, 1645200, 1648800, 1652400, 1656000, 1659600,
           1663200, 1666800, 1670400, 1674000, 1677600, 1681200, 1684800,
           1688400, 1692000, 1695600, 1699200, 1702800, 1706400, 1710000,
           1713600, 1717200, 1720800, 1724400, 1728000, 1731600, 1735200,
           1738800, 1742400, 1746000, 1749600, 1753200, 1756800, 1760400,
           1764000, 1767600, 1771200, 1774800, 1778400, 1782000, 1785600,
           1789200, 1792800, 1796400, 1800000, 1803600, 1807200, 1810800,
           1814400, 1818000, 1821600, 1825200, 1828800, 1832400, 1836000,
           1839600, 1843200, 1846800, 1850400, 1854000, 1857600, 1861200,
           1864800, 1868400, 1872000, 1875600, 1879200, 1882800, 1886400,
           1890000, 1893600, 1897200, 1900800, 1904400, 1908000, 1911600,
           1915200, 1918800, 1922400, 1926000, 1929600, 1933200, 1936800,
           1940400, 1944000, 1947600, 1951200, 1954800, 1958400, 1962000,
           1965600, 1969200, 1972800, 1976400, 1980000, 1983600, 1987200,
           1990800, 1994400, 1998000, 2001600, 2005200, 2008800, 2012400,
           2016000, 2019600, 2023200, 2026800, 2030400, 2034000, 2037600,
           2041200, 2044800, 2048400, 2052000, 2055600, 2059200, 2062800,
           2066400, 2070000, 2073600, 2077200, 2080800, 2084400, 2088000,
           2091600, 2095200, 2098800, 2102400, 2106000, 2109600, 2113200,
           2116800, 2120400, 2124000, 2127600, 2131200, 2134800, 2138400,
           2142000, 2145600, 2149200, 2152800, 2156400, 2160000, 2163600,
           2167200, 2170800, 2174400, 2178000, 2181600, 2185200, 2188800,
           2192400, 2196000, 2199600, 2203200, 2206800, 2210400, 2214000,
           2217600, 2221200, 2224800, 2228400, 2232000, 2235600, 2239200,
           2242800, 2246400, 2250000, 2253600, 2257200, 2260800, 2264400,
           2268000, 2271600, 2275200, 2278800, 2282400, 2286000, 2289600,
           2293200, 2296800, 2300400, 2304000, 2307600, 2311200, 2314800,
           2318400, 2322000, 2325600, 2329200, 2332800, 2336400, 2340000,
           2343600, 2347200, 2350800, 2354400, 2358000, 2361600, 2365200,
           2368800, 2372400, 2376000, 2379600, 2383200, 2386800, 2390400,
           2394000, 2397600, 2401200, 2404800, 2408400, 2412000, 2415600,
           2419200, 2422800, 2426400, 2430000, 2433600, 2437200, 2440800,
           2444400, 2448000, 2451600, 2455200, 2458800, 2462400, 2466000,
           2469600, 2473200, 2476800, 2480400, 2484000, 2487600, 2491200,
           2494800, 2498400, 2502000, 2505600, 2509200, 2512800, 2516400,
           2520000, 2523600, 2527200, 2530800, 2534400, 2538000, 2541600,
           2545200, 2548800, 2552400, 2556000, 2559600, 2563200, 2566800,
           2570400, 2574000, 2577600, 2581200, 2584800, 2588400, 2592000,
           2595600, 2599200, 2602800, 2606400, 2610000, 2613600, 2617200,
           2620800, 2624400, 2628000, 2631600, 2635200, 2638800, 2642400,
           2646000, 2649600, 2653200, 2656800, 2660400, 2664000, 2667600,
           2671200, 2674800])




```python
## checando os resultados com a função len (31 * 24 = 744)
len(registro_de_leituras)
```




    744



## 1.2. Indexação

Vamos agora voltar a nossa atenção para um conjunto de dados um pouco mais interessante. A célula de código abaixo cria um array denominado `populacao`, que inclui populações mundiais estimadas em cada ano de **1950** a **2022**. (As estimativas vêm da seguinte [base de dados internacional](https://www.census.gov/data-tools/demo/idb/#/country?COUNTRY_YEAR=2022&COUNTRY_YR_ANIM=2022), mantida pelo US Census Bureau, órgão equivalente ao IBGE do Brasil).

Em vez de digitar os dados manualmente, nós os carregamos de um arquivo armazenado na nuvem chamado `world_population_2022.csv`.


```python
## Veremos em detalhes as particularidades desse tipo de chamada mais adiante;
## -- por enquanto, apenas ignore os detalhes específicos e execute a célula
populacao = pd.read_csv("https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs_gabs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames%20%28gabarito%29/data/world_population_2022.csv").get("Population").values
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

<img src="https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs_gabs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames%20%28gabarito%29/images/array_logarithm.jpg">

Damos à esse tipo de aplicação o nome de aplicação *elementwise* (elemento-a-elemento) da função, uma vez que a função então opera separadamente em cada elemento do array em que é chamada.

#### **Pergunta 1.7.**

Use a função `log10` do NumPy para calcular os logaritmos da população mundial em cada ano. Dê ao resultado dessa chamada (um array de 73 elementos) o nome `magnitude_da_populacao`. 

*<u>Dica</u>: É possível fazer isso com apenas uma linha de código.*


```python
magnitude_da_populacao = np.log10(populacao)
magnitude_da_populacao
```




    array([9.40783595, 9.41412769, 9.42107342, 9.4284686 , 9.43620046,
           9.44437451, 9.45260137, 9.46110346, 9.46955099, 9.47722873,
           9.48330641, 9.48912193, 9.49696279, 9.50651009, 9.51606947,
           9.52514503, 9.5341654 , 9.54292819, 9.55180205, 9.56084112,
           9.56977847, 9.57877353, 9.58743255, 9.59584136, 9.60398607,
           9.61165827, 9.61904498, 9.6263846 , 9.63359794, 9.64097214,
           9.64796708, 9.65585065, 9.66375935, 9.67162983, 9.67916028,
           9.6868433 , 9.69460098, 9.70245411, 9.71025074, 9.71789198,
           9.72554509, 9.73265538, 9.73961043, 9.74571728, 9.75206215,
           9.75839793, 9.76457465, 9.77054552, 9.77635167, 9.78203924,
           9.78763444, 9.79318449, 9.79867012, 9.80408399, 9.8094427 ,
           9.81471739, 9.82003035, 9.8253899 , 9.83080156, 9.83614434,
           9.84134455, 9.84646607, 9.85156419, 9.85664002, 9.86162991,
           9.86649268, 9.87128982, 9.87603123, 9.88064591, 9.88517378,
           9.8896867 , 9.89385707, 9.89792038])



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


<img src="https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs_gabs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames%20%28gabarito%29/images/array_multiplication.jpg">

#### **Pergunta 1.8.** 

Suponha que a cobrança total em um restaurante seja a conta original acrescida do valor da gorjeta de 20% (isso significa que podemos simplesmente multiplicar a fatura original por 1.2 para obter a cobrança total). Calcule então a cobrança total de cada conta no array `conta_dos_restaurantes` e dê ao array resultante o nome de `cobrancas_totais`.


```python
cobrancas_totais = 1.2 * contas_dos_restaurantes
cobrancas_totais
```




    array([24.144, 47.88 , 37.212])



Vamos agora carregar alguns dados para utilizar na próxima pergunta:


```python
mais_contas_de_restaurantes = pd.read_csv("https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs_gabs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames%20%28gabarito%29/data/more_restaurant_bills.csv").get("Bill").values
```

#### **Pergunta 1.8.** 

O array `mais_contas_de_restaurantes` contém 100.000 contas de restaurantes! Calcule a cobrança total de cada uma, assumindo novamente uma gorjeta de vinte por cento, e dê ao array resultante o nome `mais_cobrancas_totais`.


```python
mais_cobrancas_totais = 1.2 * mais_contas_de_restaurantes
mais_cobrancas_totais
```




    array([20.244, 20.892, 12.216, ..., 19.308, 18.336, 35.664],
          shape=(100000,))



Uma função muito útil da biblioteca NumPy é `.sum`, que toma um único array de números como argumento, e retorna a soma de todos os números desse array.

*<u>Nota</u>: `.sum` retorna um único número, não um array.*

#### **Pergunta 1.9.** 

Qual foi a soma de todas as contas em `mais_contas_de_restaurantes`, **incluindo as gorjetas**?


```python
## Resposta utilizando o resultado da Pergunta 1.8.
soma_das_contas = np.sum(mais_cobrancas_totais)
soma_das_contas
```




    np.float64(1795730.0639999998)




```python
## Resposta utilizando apenas o array `mais_contas_de_restaurantes`
soma_das_contas = np.sum(1.2 * mais_contas_de_restaurantes)
soma_das_contas
```




    np.float64(1795730.0639999998)



### Potências Binárias

As potências de 2 ($2^0 = 1$, $2^1 = 2$, $2^2 = 4$, etc) surgem com frequência na Ciência da Computação. Um exemplo comum é o armazenamento físico de dados, que usualmente vêm em potências binárias como 64 GB, 128 GB ou 256 GB.

#### **Pergunta 1.10.** 

Use `np.arange` e o operador de exponenciação `**` para criar um array contendo as primeiras 40 potências de 2, começando em $2^0=1$.

*<u>Dica 1</u>: Se seu kernel “morrer” enquanto você executava a célula de código abaixo correspondente, reveja sua solução para essa pergunta. Existe uma resposta incorreta comum para esse problema que tenta criar um array com tantas entradas que o Python simplesmente desiste.*


```python
potencias_de_2 = 2 ** (np.arange(0, 40, 1))
potencias_de_2
```




    array([           1,            2,            4,            8,
                     16,           32,           64,          128,
                    256,          512,         1024,         2048,
                   4096,         8192,        16384,        32768,
                  65536,       131072,       262144,       524288,
                1048576,      2097152,      4194304,      8388608,
               16777216,     33554432,     67108864,    134217728,
              268435456,    536870912,   1073741824,   2147483648,
             4294967296,   8589934592,  17179869184,  34359738368,
            68719476736, 137438953472, 274877906944, 549755813888])



# 2. DataFrames

## 2.1. Introdução

Em muitas situações, os arrays são úteis para descrever um *único* atributo de uma coleção de objetos. Por exemplo, se considerarmos os estados dos EUA, um array poderia descrever a extensão territorial de cada estado. 

As tabelas são uma extensão natural dos arrays, podendo conter *múltiplas* características de uma coleção de objetos. Nesse exemplo dos estados dos EUA, além da extensão territorial, uma tabela poderia armazenar a população, capital, PIB, etc. de cada estado. Em outras palavras, as tabelas nos permitem descrever diferentes entidades (ou **indivíduos**, armazenados como **linhas**) e, para cada uma dessas entidades, múltiplos atributos (**features**, armazenadas como **colunas**).


Na célula abaixo temos dois arrays. O primeiro contém a população mundial em cada ano (conforme estimado pelo US Census Bureau), e o segundo contém os anos correspondentes (em ordem crescente).


```python
anos = np.arange(1950, 2022+1)
quantidade_populacional = pd.read_csv("https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs_gabs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames%20%28gabarito%29/data/world_population_2022.csv").get("Population").values

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
top_10_filmes_com_minhas_avaliacoes = top_10_filmes.assign(Minhas_Avaliacoes = minhas_avaliacoes)
top_10_filmes_com_minhas_avaliacoes
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
      <th>Minhas_Avaliacoes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>9.2</td>
      <td>The Shawshank Redemption (1994)</td>
      <td>8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9.2</td>
      <td>The Godfather (1972)</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>9.0</td>
      <td>The Godfather: Part II (1974)</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>8.9</td>
      <td>Pulp Fiction (1994)</td>
      <td>9</td>
    </tr>
    <tr>
      <th>4</th>
      <td>8.9</td>
      <td>Schindler's List (1993)</td>
      <td>7</td>
    </tr>
    <tr>
      <th>5</th>
      <td>8.9</td>
      <td>The Lord of the Rings: The Return of the King ...</td>
      <td>10</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8.9</td>
      <td>12 Angry Men (1957)</td>
      <td>6</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8.9</td>
      <td>The Dark Knight (2008)</td>
      <td>4</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8.9</td>
      <td>Il buono, il brutto, il cattivo (1966)</td>
      <td>3</td>
    </tr>
    <tr>
      <th>9</th>
      <td>8.8</td>
      <td>The Lord of the Rings: The Fellowship of the R...</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



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
top_10_filmes_por_nome = top_10_filmes.set_index('Nome')
top_10_filmes_por_nome
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
    </tr>
    <tr>
      <th>Nome</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>The Shawshank Redemption (1994)</th>
      <td>9.2</td>
    </tr>
    <tr>
      <th>The Godfather (1972)</th>
      <td>9.2</td>
    </tr>
    <tr>
      <th>The Godfather: Part II (1974)</th>
      <td>9.0</td>
    </tr>
    <tr>
      <th>Pulp Fiction (1994)</th>
      <td>8.9</td>
    </tr>
    <tr>
      <th>Schindler's List (1993)</th>
      <td>8.9</td>
    </tr>
    <tr>
      <th>The Lord of the Rings: The Return of the King (2003)</th>
      <td>8.9</td>
    </tr>
    <tr>
      <th>12 Angry Men (1957)</th>
      <td>8.9</td>
    </tr>
    <tr>
      <th>The Dark Knight (2008)</th>
      <td>8.9</td>
    </tr>
    <tr>
      <th>Il buono, il brutto, il cattivo (1966)</th>
      <td>8.9</td>
    </tr>
    <tr>
      <th>The Lord of the Rings: The Fellowship of the Ring (2001)</th>
      <td>8.8</td>
    </tr>
  </tbody>
</table>
</div>



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
decimo_filme = top_10_filmes_por_nome.index[9]
decimo_filme
```




    'The Lord of the Rings: The Fellowship of the Ring (2001)'



## 2.3 Carregando DataFrames de arquivos externos

Na prática de Ciência de Dados, é mais comum podermos aproveitar de bases de dados que já estejam "prontas", isto é, em geral não precisamos digitar nossos dados manualmente. Ao invés disso, podemos utilizar funções fornecidas no `pandas` para ler dados de arquivos externos.

A função `pd.read_csv()` toma um argumento (um caminho para um arquivo de dados – e que logo é uma `string`) e retorna um `DataFrame`.

*<u>Nota</u>: Embora existam muitos formatos de arquivos de dados, CSV (**comma separated values**, ou "valores separados por vírgulas") é o mais comum.*

#### **Pergunta 2.5.** 

O arquivo `data/imdb.csv` contém informações sobre os 250 filmes mais bem avaliados no IMDb. Carregue-o na célula de código abaixo e atribua-o ao objeto `imdb`.

*<u>Dica</u>: Se você não tiver a pasta local "data" em seu diretório de trabalho, você deve carregar os arquivos da pasta "data" armazenada na nuvem, cuja URL é "https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs_gabs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames%20%28gabarito%29/data/"*


```python
imdb = pd.read_csv("https://raw.githubusercontent.com/urielmoreirasilva/ICX532/main/labs_gabs/Laborat%C3%B3rio%201%20%E2%80%93%20Arrays%20e%20DataFrames%20%28gabarito%29/data/imdb.csv")
imdb
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
      <th>Votes</th>
      <th>Rating</th>
      <th>Title</th>
      <th>Year</th>
      <th>Decade</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>88355</td>
      <td>8.4</td>
      <td>M</td>
      <td>1931</td>
      <td>1930</td>
    </tr>
    <tr>
      <th>1</th>
      <td>132823</td>
      <td>8.3</td>
      <td>Singin' in the Rain</td>
      <td>1952</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>2</th>
      <td>74178</td>
      <td>8.3</td>
      <td>All About Eve</td>
      <td>1950</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>3</th>
      <td>635139</td>
      <td>8.6</td>
      <td>Léon</td>
      <td>1994</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>4</th>
      <td>145514</td>
      <td>8.2</td>
      <td>The Elephant Man</td>
      <td>1980</td>
      <td>1980</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>245</th>
      <td>1078416</td>
      <td>8.7</td>
      <td>Forrest Gump</td>
      <td>1994</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>246</th>
      <td>31003</td>
      <td>8.1</td>
      <td>Le salaire de la peur</td>
      <td>1953</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>247</th>
      <td>167076</td>
      <td>8.2</td>
      <td>3 Idiots</td>
      <td>2009</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>248</th>
      <td>91689</td>
      <td>8.1</td>
      <td>Network</td>
      <td>1976</td>
      <td>1970</td>
    </tr>
    <tr>
      <th>249</th>
      <td>589477</td>
      <td>8.3</td>
      <td>Eternal Sunshine of the Spotless Mind</td>
      <td>2004</td>
      <td>2000</td>
    </tr>
  </tbody>
</table>
<p>250 rows × 5 columns</p>
</div>



Observe as reticências (`...`) acima, no meio do DataFrame. Isso significa que algumas (ou muitas) linhas desse DataFrame foram omitidas. 

*<u>Nota</u>: Esse comportamento pode ser customizado com o comando `pd.set_option('display.max_rows', K)`, onde `K` é o número máximo de linhas que se deseja exibir.*

#### **Pergunta 2.6.** 

Como `imdb` é um conjunto de dados de filmes, faz sentido usar o título de cada filme como rótulo da linha correspondente. Crie então na célula de código abaixo um novo DataFrame chamado `imdb_por_nome`, utilizando o título do filme como índice em `imdb`.


```python
imdb_por_nome = imdb.set_index("Title")
imdb_por_nome
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
      <th>Votes</th>
      <th>Rating</th>
      <th>Year</th>
      <th>Decade</th>
    </tr>
    <tr>
      <th>Title</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>M</th>
      <td>88355</td>
      <td>8.4</td>
      <td>1931</td>
      <td>1930</td>
    </tr>
    <tr>
      <th>Singin' in the Rain</th>
      <td>132823</td>
      <td>8.3</td>
      <td>1952</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>All About Eve</th>
      <td>74178</td>
      <td>8.3</td>
      <td>1950</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Léon</th>
      <td>635139</td>
      <td>8.6</td>
      <td>1994</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>The Elephant Man</th>
      <td>145514</td>
      <td>8.2</td>
      <td>1980</td>
      <td>1980</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Forrest Gump</th>
      <td>1078416</td>
      <td>8.7</td>
      <td>1994</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Le salaire de la peur</th>
      <td>31003</td>
      <td>8.1</td>
      <td>1953</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>3 Idiots</th>
      <td>167076</td>
      <td>8.2</td>
      <td>2009</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>Network</th>
      <td>91689</td>
      <td>8.1</td>
      <td>1976</td>
      <td>1970</td>
    </tr>
    <tr>
      <th>Eternal Sunshine of the Spotless Mind</th>
      <td>589477</td>
      <td>8.3</td>
      <td>2004</td>
      <td>2000</td>
    </tr>
  </tbody>
</table>
<p>250 rows × 4 columns</p>
</div>



## 2.4. Series

Suponha agora que estejamos interessados principalmente nas classificações dos filmes em `imdb`. Para extrair apenas esta coluna do DataFrame, utilizamos o método `.get`:


```python
avaliacoes = imdb_por_nome.get('Rating')
avaliacoes
```




    Title
    M                                        8.4
    Singin' in the Rain                      8.3
    All About Eve                            8.3
    Léon                                     8.6
    The Elephant Man                         8.2
                                            ... 
    Forrest Gump                             8.7
    Le salaire de la peur                    8.1
    3 Idiots                                 8.2
    Network                                  8.1
    Eternal Sunshine of the Spotless Mind    8.3
    Name: Rating, Length: 250, dtype: float64



Observe como não apenas as classificações dos filmes foram retornadas, mas também o nome de cada filme! Isto ocorre *exatamente* porque definimos o título do filme como o índice.

Por outro lado, se tivéssemos chamado a coluna `"Rating"` do DataFrame original (`imdb`, sem índice), teríamos:


```python
imdb.get('Rating')
```




    0      8.4
    1      8.3
    2      8.3
    3      8.6
    4      8.2
          ... 
    245    8.7
    246    8.1
    247    8.2
    248    8.1
    249    8.3
    Name: Rating, Length: 250, dtype: float64



Esta é uma razão pela qual os índices são muito úteis na prática – eles podem nos fornecem rótulos informativos para os dados!

Agora, à primeira vista, pode parecer que invocar uma coluna utilizando `.get` retorna um DataFrame com uma coluna, mas isso não é verdade.

Ao invés disso, `.get` retorna um tipo especial de objeto, denominado de *Series*:


```python
type(imdb_por_nome.get('Rating'))
```




    pandas.core.series.Series



Você pode pensar em uma `Series` como um `array`, mas com um índice. 

Enquanto os arrays são sequências simples de números sem rótulos, as Series podem ter rótulos. Isso em geral pode ser muito útil!

Voltando ao exemplo acima, `avaliacoes` agora é uma `Series`, contendo a coluna de classificações de cada um dos filmes em `imdb`. Suponha agora que estejamos interessados então na avaliação de um filme específico: _Alien_. Para retornar essa avaliação, utilizaremos o **acessador** `.loc`, que extrai um valor de uma `Series` em um *local* (valor do índice) específico:


```python
avaliacoes.loc["Alien"]
```




    np.float64(8.5)



Note aqui que, na chamada acima, colocamos colchetes (`[]`) em torno de `"Alien"`. Isso se deve ao fato de que `.loc` *não é um método*, mas um *acessador*, o que faz com que `.loc` deva obedecer às regras de indexação do Python.

#### **Pergunta 2.7.** 

Encontre na célula de código abaixo a avaliação do filme _3 Idiotas_ (*3 Idiots*).


```python
avaliacao_de_tres_idiotas = avaliacoes.loc["3 Idiots"]
avaliacao_de_tres_idiotas
```




    np.float64(8.2)



Suponha agora que estejamos interessados em saber o *ano* em que o filme _Alien_ foi lançado. Podemos fazer isso obtendo primeiro a coluna dos anos:


```python
anos = imdb_por_nome.get('Year')
anos
```




    Title
    M                                        1931
    Singin' in the Rain                      1952
    All About Eve                            1950
    Léon                                     1994
    The Elephant Man                         1980
                                             ... 
    Forrest Gump                             1994
    Le salaire de la peur                    1953
    3 Idiots                                 2009
    Network                                  1976
    Eternal Sunshine of the Spotless Mind    2004
    Name: Year, Length: 250, dtype: int64



... e então usarmos `.loc` para obter a entrada correta:


```python
anos.loc['Alien']
```




    np.int64(1979)



Uma alternativa mais comum na prática (e que deixa o código mais "limpo") é fazer isso em uma única chamada, *encadeando* as operações:


```python
imdb_por_nome.get('Year').loc['Alien']
```




    np.int64(1979)



Isso funciona porque o Python primeiro avalia `imdb_por_nome.get('Year')` para retornar uma `Series` e, em seguida, avalia `.loc['Alien']` sobre essa Series para retornar o ano correspondente!

#### **Pergunta 2.8.** 

Na célula de código abaixo, encontre a década em que o filme _Gone Girl_ foi lançado. Utilize encadeamento para que seu código ocupe apenas uma linha.

*<u>Dica</u>: O DataFrame `imbd_por_nome` possui uma coluna chamada `"Decade"`.*


```python
decada = imdb_por_nome.get('Decade').loc['Gone Girl']
decada
```




    np.int64(2010)



# 3. Analisando DataFrames

Veremos agora que, com apenas alguns métodos dos `DataFrame`s de `pandas`, podemos responder algumas questões bem interessantes sobre o conjunto de dados `imdb`.

#### **Pergunta 3.1.** 

Na célula de código abaixo, utilize o método `.max` aplicado à Series `avaliacoes` para encontrar a maior avaliação dos filmes em `imdb`.


```python
maior_avaliacao = avaliacoes.max()
maior_avaliacao
```




    9.2



Agora, se estivermos interessados em saber o *nome* do filme cuja avaliação (`maior_avaliacao`) você encontrou acima, basta aplicar o método `.sort_values` à Series `avaliacoes`, de modo a produzir uma `Series` ordenada:


```python
avaliacoes.sort_values()
```




    Title
    Akira                               8.0
    Per un pugno di dollari             8.0
    Guardians of the Galaxy             8.0
    The Man Who Shot Liberty Valance    8.0
    Underground                         8.0
                                       ... 
    Schindler's List                    8.9
    12 Angry Men                        8.9
    The Godfather: Part II              9.0
    The Shawshank Redemption            9.2
    The Godfather                       9.2
    Name: Rating, Length: 250, dtype: float64



Ao analisarmos as duas últimas entradas dessa `Series` ordenada, concluímos então que na verdade existem *dois* filmes com essa avaliação no conjunto de dados: *The Shawshank Redemption* e *The Godfather*.

*<u>Nota</u>: aqui estamos ordenando pelas avaliações, e não pelos rótulos! Dessa forma, os rótulos de cada linha também seguem a ordenação conforme a sua avaliação, e esse é exatamente o comportamento que queremos.*

É importante mencionar aqui que, quando utilizamos o método `sort_values`, a `Series` resultante tem os dados ordenados em ordem *crescente*, isto é, com seus elementos ordenados do menor ao maior. Este é o comportamento padrão de `sort_values`, mas podemos mudar isso especificando um **argumento nomeado** (**keyword**) opcional, `ascending`:  


```python
avaliacoes.sort_values(ascending = False)
```




    Title
    The Godfather                             9.2
    The Shawshank Redemption                  9.2
    The Godfather: Part II                    9.0
    12 Angry Men                              8.9
    Il buono, il brutto, il cattivo (1966)    8.9
                                             ... 
    Monsters, Inc. (2001)                     8.0
    The Big Sleep                             8.0
    X-Men: Days of Future Past                8.0
    Roman Holiday                             8.0
    Kumonosu-jô                               8.0
    Name: Rating, Length: 250, dtype: float64



De maneira análoga, se invocarmos a função `.sort_values` com `ascending = True`, obteremos o mesmo resultado, como se nunca tívessemos atribuído valor algum a `ascending`.

É exatamente isso que queremos dizer quando dizemos que o comportamento padrão de `sort_values` é classificar em ordem crescente, isto é, tomando `ascending = True`. Como esse é o comportamento padrão, o argumento nomeado `asceding` torna-se *opcional*, e produzimos um comportamento diferente apenas quando especificamos `asceding = False`. Repare que as duas células de código seguintes resutam na mesma saída.


```python
avaliacoes.sort_values(ascending = True)
```




    Title
    Akira                               8.0
    Per un pugno di dollari             8.0
    Guardians of the Galaxy             8.0
    The Man Who Shot Liberty Valance    8.0
    Underground                         8.0
                                       ... 
    Schindler's List                    8.9
    12 Angry Men                        8.9
    The Godfather: Part II              9.0
    The Shawshank Redemption            9.2
    The Godfather                       9.2
    Name: Rating, Length: 250, dtype: float64




```python
avaliacoes.sort_values()
```




    Title
    Akira                               8.0
    Per un pugno di dollari             8.0
    Guardians of the Galaxy             8.0
    The Man Who Shot Liberty Valance    8.0
    Underground                         8.0
                                       ... 
    Schindler's List                    8.9
    12 Angry Men                        8.9
    The Godfather: Part II              9.0
    The Shawshank Redemption            9.2
    The Godfather                       9.2
    Name: Rating, Length: 250, dtype: float64



Em geral, não só podemos ordenar `Series`, mas também `DataFrames` inteiros! Para fazermos isso, basta especificar a coluna pela qual iremos ordenar:


```python
imdb_por_nome.sort_values('Rating')
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
      <th>Votes</th>
      <th>Rating</th>
      <th>Year</th>
      <th>Decade</th>
    </tr>
    <tr>
      <th>Title</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Akira</th>
      <td>91652</td>
      <td>8.0</td>
      <td>1988</td>
      <td>1980</td>
    </tr>
    <tr>
      <th>Per un pugno di dollari</th>
      <td>124671</td>
      <td>8.0</td>
      <td>1964</td>
      <td>1960</td>
    </tr>
    <tr>
      <th>Guardians of the Galaxy</th>
      <td>527349</td>
      <td>8.0</td>
      <td>2014</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>The Man Who Shot Liberty Valance</th>
      <td>49135</td>
      <td>8.0</td>
      <td>1962</td>
      <td>1960</td>
    </tr>
    <tr>
      <th>Underground</th>
      <td>39447</td>
      <td>8.0</td>
      <td>1995</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Schindler's List</th>
      <td>761224</td>
      <td>8.9</td>
      <td>1993</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>12 Angry Men</th>
      <td>384187</td>
      <td>8.9</td>
      <td>1957</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>The Godfather: Part II</th>
      <td>692753</td>
      <td>9.0</td>
      <td>1974</td>
      <td>1970</td>
    </tr>
    <tr>
      <th>The Shawshank Redemption</th>
      <td>1498733</td>
      <td>9.2</td>
      <td>1994</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>The Godfather</th>
      <td>1027398</td>
      <td>9.2</td>
      <td>1972</td>
      <td>1970</td>
    </tr>
  </tbody>
</table>
<p>250 rows × 4 columns</p>
</div>



De maneira análoga ao que fizemos anteriormente, podemos aqui também especificar que a ordenação deve ser em ordem decrescente:


```python
imdb_por_nome.sort_values('Rating', ascending = False)
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
      <th>Votes</th>
      <th>Rating</th>
      <th>Year</th>
      <th>Decade</th>
    </tr>
    <tr>
      <th>Title</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>The Godfather</th>
      <td>1027398</td>
      <td>9.2</td>
      <td>1972</td>
      <td>1970</td>
    </tr>
    <tr>
      <th>The Shawshank Redemption</th>
      <td>1498733</td>
      <td>9.2</td>
      <td>1994</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>The Godfather: Part II</th>
      <td>692753</td>
      <td>9.0</td>
      <td>1974</td>
      <td>1970</td>
    </tr>
    <tr>
      <th>12 Angry Men</th>
      <td>384187</td>
      <td>8.9</td>
      <td>1957</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Il buono, il brutto, il cattivo (1966)</th>
      <td>447875</td>
      <td>8.9</td>
      <td>1966</td>
      <td>1960</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Monsters, Inc. (2001)</th>
      <td>500576</td>
      <td>8.0</td>
      <td>2001</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>The Big Sleep</th>
      <td>59578</td>
      <td>8.0</td>
      <td>1946</td>
      <td>1940</td>
    </tr>
    <tr>
      <th>X-Men: Days of Future Past</th>
      <td>427099</td>
      <td>8.0</td>
      <td>2014</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>Roman Holiday</th>
      <td>87437</td>
      <td>8.0</td>
      <td>1953</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Kumonosu-jô</th>
      <td>26012</td>
      <td>8.0</td>
      <td>1957</td>
      <td>1950</td>
    </tr>
  </tbody>
</table>
<p>250 rows × 4 columns</p>
</div>



Alguns detalhes adicionais sobre a ordenação de `DataFrame`s:

1. O primeiro argumento de `sort_values` é o nome da coluna pela qual iremos ordenar;
1. Se a coluna for composta por `string`s, ela será ordenada em ordem alfabética; se for composta por números, ela será ordenada numericamente;
1. `imdb_por_nome.sort_values("Rating")` retorna um *novo DataFrame* – o DataFrame `imdb_por_nome` não é modificado. Para salvar o resultado dessa chamada, você deve atribuí-lo a um novo objeto;
1. Todas as linhas de um DataFrame são reorganizadas de maneira apropriada quando um DataFrame é ordenado. Esse é exatamente o comportamento desejado – não faria sentido ordenar apenas uma coluna e deixar as outras colunas como estão, pois as características (colunas) dos indivíduos (linhas) representadas na tabela (DataFrame) não seriam mais as mesmas.

#### **Pergunta 3.2.**

Na célula de código abaixo, crie uma versão de `imdb_por_nome` que seja ordenada cronologicamente, com os filmes mais antigos primeiro. Nomeie o DataFrame correspondente como `imdb_ordenado`.

*<u>Dica</u>: verifique acima quais colunas estão disponíveis em `imdb_por_nome`!*


```python
imdb_ordenado = imdb_por_nome.sort_values("Year")
imdb_ordenado
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
      <th>Votes</th>
      <th>Rating</th>
      <th>Year</th>
      <th>Decade</th>
    </tr>
    <tr>
      <th>Title</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>The Kid</th>
      <td>55784</td>
      <td>8.3</td>
      <td>1921</td>
      <td>1920</td>
    </tr>
    <tr>
      <th>The Gold Rush</th>
      <td>58506</td>
      <td>8.2</td>
      <td>1925</td>
      <td>1920</td>
    </tr>
    <tr>
      <th>The General</th>
      <td>46332</td>
      <td>8.2</td>
      <td>1926</td>
      <td>1920</td>
    </tr>
    <tr>
      <th>Metropolis</th>
      <td>98794</td>
      <td>8.3</td>
      <td>1927</td>
      <td>1920</td>
    </tr>
    <tr>
      <th>M</th>
      <td>88355</td>
      <td>8.4</td>
      <td>1931</td>
      <td>1930</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>The Grand Budapest Hotel</th>
      <td>369141</td>
      <td>8.1</td>
      <td>2014</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>Relatos salvajes</th>
      <td>46987</td>
      <td>8.0</td>
      <td>2014</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>Interstellar</th>
      <td>689541</td>
      <td>8.6</td>
      <td>2014</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>Mad Max: Fury Road</th>
      <td>262425</td>
      <td>8.3</td>
      <td>2015</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>Inside Out (2015/I)</th>
      <td>79615</td>
      <td>8.5</td>
      <td>2015</td>
      <td>2010</td>
    </tr>
  </tbody>
</table>
<p>250 rows × 4 columns</p>
</div>



#### **Pergunta 3.3.** 

Com base na resposta à pergunta anterior, atribua na célula de código abaixo o título do filme mais antigo no conjunto de dados ao objeto `titulo_do_filme_mais_antigo`.

*<u>Dica</u>: Utilize o fato de que o índice é um `array`, e que o índice do `DataFrame` acima pode ser retornado simplesmente chamando `imdb_ordenado.index`.*


```python
titulo_do_filme_mais_antigo = imdb_ordenado.index[0]
titulo_do_filme_mais_antigo
```




    'The Kid'



Suponha agora que estejamos interessados em obter a avaliação do filme mais antigo no nosso conjunto de dados.

Como já encontramos o rótulo do filme mais antigo (`titulo_do_filme_mais_antigo`) acima, basta então extraírmos a coluna de interesse (`Rating`) e usarmos `.loc`!


```python
imdb_ordenado.get('Rating').loc[titulo_do_filme_mais_antigo]
```




    np.float64(8.3)



Uma outra maneira alternativa de fazermos a mesma coisa é utilizar o acessador `.iloc`. 

Enquanto `.loc` procura coisas por *rótulo*, `.iloc` procura elementos por *posição*, de maneira que `.iloc[0]` retorna o primeiro elemento de uma `Series`, `.iloc[1]` o segundo, e assim em diante.


```python
imdb_ordenado.get('Rating').iloc[0]
```




    np.float64(8.3)



Em ambos os casos, os resultados acima são equivalentes. Se tívessemos analisado o DataFrame `imdb_ordenado` manualmente e verificado que `The Kid` é o filme mais antigo, chamar `imdb_ordenado.get('Rating').loc['The Kid']` também produziria o mesmo resultado.

Por fim, note que tanto `.loc` quanto `.iloc` podem ser aplicados à um `DataFrame` inteiro, produzindo uma `Series` com as colunas correspondentes:


```python
imdb_ordenado.loc["The Kid"]
```




    Votes     55784.0
    Rating        8.3
    Year       1921.0
    Decade     1920.0
    Name: The Kid, dtype: float64




```python
imdb_ordenado.iloc[0]
```




    Votes     55784.0
    Rating        8.3
    Year       1921.0
    Decade     1920.0
    Name: The Kid, dtype: float64



... ou produzindo até um novo `DataFrame`, caso os argumentos de `.loc` e `.iloc` sejam `List`s (ou `array`s): 


```python
imdb_ordenado.loc[["The Kid", "The Gold Rush"]]
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
      <th>Votes</th>
      <th>Rating</th>
      <th>Year</th>
      <th>Decade</th>
    </tr>
    <tr>
      <th>Title</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>The Kid</th>
      <td>55784</td>
      <td>8.3</td>
      <td>1921</td>
      <td>1920</td>
    </tr>
    <tr>
      <th>The Gold Rush</th>
      <td>58506</td>
      <td>8.2</td>
      <td>1925</td>
      <td>1920</td>
    </tr>
  </tbody>
</table>
</div>




```python
imdb_ordenado.iloc[[0, 1]]
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
      <th>Votes</th>
      <th>Rating</th>
      <th>Year</th>
      <th>Decade</th>
    </tr>
    <tr>
      <th>Title</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>The Kid</th>
      <td>55784</td>
      <td>8.3</td>
      <td>1921</td>
      <td>1920</td>
    </tr>
    <tr>
      <th>The Gold Rush</th>
      <td>58506</td>
      <td>8.2</td>
      <td>1925</td>
      <td>1920</td>
    </tr>
  </tbody>
</table>
</div>



#### **Pergunta 3.4.** 

Encontre na célula de código abaixo a avaliação do quinto filme mais antigo no conjunto de dados.

*<u>Dica</u> Utilize `.iloc` na posição correspondente do DataFrame `imdb_ordenado`, filtrando antes pela coluna de interesse.*


```python
avaliacao_do_quinto_filme_mais_antigo = imdb_ordenado.get("Rating").iloc[4]
avaliacao_do_quinto_filme_mais_antigo
```




    np.float64(8.4)



# 4. Filtrando DataFrames

Ainda no contexto do conjunto de dados dos filmes (`imdb`), suponha agora que você esteja interessado em filmes da década de 1950. Nesse caso, ordenar o `DataFrame` por ano não ajuda muito, porque a década de 1950 está no "meio" do conjunto. 

Uma alternativa muito útil nesse caso é utilizarmos um recurso das `Series` que nos permite verificar facilmente se cada elemento em uma coluna de um `DataFrame` cumpre com uma condição específica.

Primeiramente, lembre-se que podemos usar `.get` para extrair uma única coluna. O resultado não é um `DataFrame`, mas sim uma `Series`:


```python
imdb_por_nome.get("Decade")
```




    Title
    M                                        1930
    Singin' in the Rain                      1950
    All About Eve                            1950
    Léon                                     1990
    The Elephant Man                         1980
                                             ... 
    Forrest Gump                             1990
    Le salaire de la peur                    1950
    3 Idiots                                 2000
    Network                                  1970
    Eternal Sunshine of the Spotless Mind    2000
    Name: Decade, Length: 250, dtype: int64



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
imdb_por_nome.get("Decade") == 1950
```




    Title
    M                                        False
    Singin' in the Rain                       True
    All About Eve                             True
    Léon                                     False
    The Elephant Man                         False
                                             ...  
    Forrest Gump                             False
    Le salaire de la peur                     True
    3 Idiots                                 False
    Network                                  False
    Eternal Sunshine of the Spotless Mind    False
    Name: Decade, Length: 250, dtype: bool



A operação acima retorna então uma nova `Series`, que têm valores iguais a `True` apenas para os filmes da década de 1950, e `False` para todos os outros. Dizemos que a `Series` resultante é uma Series de *Booleanos*, ou uma *Series Booleana*.

Para fins didáticos, vamos atribuir o resultado acima à uma `Series` que daremos o nome de `e_da_decada_de_1950`. A ideia é que esse nome possa ser então lido como se fosse uma pergunta, isto é: "(o filme) é da década de 1950"?


```python
e_da_decada_de_1950 = imdb_por_nome.get("Decade") == 1950
e_da_decada_de_1950
```




    Title
    M                                        False
    Singin' in the Rain                       True
    All About Eve                             True
    Léon                                     False
    The Elephant Man                         False
                                             ...  
    Forrest Gump                             False
    Le salaire de la peur                     True
    3 Idiots                                 False
    Network                                  False
    Eternal Sunshine of the Spotless Mind    False
    Name: Decade, Length: 250, dtype: bool



Dessa forma, cada linha nessa `Series` é uma resposta à pergunta "(o filme) é da década de 1950?". 

<u>Exemplos</u>: *The Elephant Man* é da década de 1950? `False`. *All About Eve* é da década de 1950? `True`.

Voltando ao nosso objetivo original, podemos agora usar a Series `e_da_decada_de_1950` para selecionar apenas as linhas de `imdb_por_nome` para as quais a resposta é `True`. A sintaxe para isso é:


```python
imdb_por_nome[e_da_decada_de_1950]
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
      <th>Votes</th>
      <th>Rating</th>
      <th>Year</th>
      <th>Decade</th>
    </tr>
    <tr>
      <th>Title</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Singin' in the Rain</th>
      <td>132823</td>
      <td>8.3</td>
      <td>1952</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>All About Eve</th>
      <td>74178</td>
      <td>8.3</td>
      <td>1950</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Some Like It Hot</th>
      <td>156432</td>
      <td>8.3</td>
      <td>1959</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>The Killing</th>
      <td>56671</td>
      <td>8.0</td>
      <td>1956</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Roman Holiday</th>
      <td>87437</td>
      <td>8.0</td>
      <td>1953</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Touch of Evil</th>
      <td>65408</td>
      <td>8.1</td>
      <td>1958</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Rashômon</th>
      <td>90434</td>
      <td>8.3</td>
      <td>1950</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>La strada</th>
      <td>42446</td>
      <td>8.0</td>
      <td>1954</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>North by Northwest</th>
      <td>198795</td>
      <td>8.4</td>
      <td>1959</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Sunset Blvd.</th>
      <td>123879</td>
      <td>8.5</td>
      <td>1950</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Shichinin no samurai</th>
      <td>206216</td>
      <td>8.7</td>
      <td>1954</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>12 Angry Men</th>
      <td>384187</td>
      <td>8.9</td>
      <td>1957</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Les diaboliques</th>
      <td>36725</td>
      <td>8.1</td>
      <td>1955</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Kumonosu-jô</th>
      <td>26012</td>
      <td>8.0</td>
      <td>1957</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Ben-Hur</th>
      <td>141768</td>
      <td>8.1</td>
      <td>1959</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Witness for the Prosecution</th>
      <td>53186</td>
      <td>8.3</td>
      <td>1957</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Dial M for Murder</th>
      <td>92244</td>
      <td>8.1</td>
      <td>1954</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Ikiru</th>
      <td>36638</td>
      <td>8.2</td>
      <td>1952</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>On the Waterfront</th>
      <td>89233</td>
      <td>8.2</td>
      <td>1954</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Les quatre cents coups</th>
      <td>61776</td>
      <td>8.1</td>
      <td>1959</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Paths of Glory</th>
      <td>106038</td>
      <td>8.4</td>
      <td>1957</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>High Noon</th>
      <td>72007</td>
      <td>8.0</td>
      <td>1952</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Vertigo</th>
      <td>218430</td>
      <td>8.4</td>
      <td>1958</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>The Bridge on the River Kwai</th>
      <td>132677</td>
      <td>8.2</td>
      <td>1957</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Rear Window</th>
      <td>280432</td>
      <td>8.5</td>
      <td>1954</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Det sjunde inseglet</th>
      <td>98949</td>
      <td>8.2</td>
      <td>1957</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>The Night of the Hunter</th>
      <td>57974</td>
      <td>8.0</td>
      <td>1955</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Smultronstället</th>
      <td>55861</td>
      <td>8.2</td>
      <td>1957</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Strangers on a Train</th>
      <td>85012</td>
      <td>8.1</td>
      <td>1951</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Le salaire de la peur</th>
      <td>31003</td>
      <td>8.1</td>
      <td>1953</td>
      <td>1950</td>
    </tr>
  </tbody>
</table>
</div>



Mais precisamente, o que a chamada `imdb_por_nome[e_da_decada_de_1950]` faz é percorrer `imdb_por_nome` linha por linha, **filtrando** o DataFrame pelas linhas cuja condição especificada é `True` (e ignorando, ou "descartando" as linhas para a qual a condição especificada é `False`).

Uma maneira mais "limpa" e direta de obtermos o mesmo resultado é encadeando as operações acima, sem precisar atribuir a `Series` booleana a um objeto:


```python
imdb_por_nome[imdb_por_nome.get("Decade") == 1950]
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
      <th>Votes</th>
      <th>Rating</th>
      <th>Year</th>
      <th>Decade</th>
    </tr>
    <tr>
      <th>Title</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Singin' in the Rain</th>
      <td>132823</td>
      <td>8.3</td>
      <td>1952</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>All About Eve</th>
      <td>74178</td>
      <td>8.3</td>
      <td>1950</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Some Like It Hot</th>
      <td>156432</td>
      <td>8.3</td>
      <td>1959</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>The Killing</th>
      <td>56671</td>
      <td>8.0</td>
      <td>1956</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Roman Holiday</th>
      <td>87437</td>
      <td>8.0</td>
      <td>1953</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Touch of Evil</th>
      <td>65408</td>
      <td>8.1</td>
      <td>1958</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Rashômon</th>
      <td>90434</td>
      <td>8.3</td>
      <td>1950</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>La strada</th>
      <td>42446</td>
      <td>8.0</td>
      <td>1954</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>North by Northwest</th>
      <td>198795</td>
      <td>8.4</td>
      <td>1959</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Sunset Blvd.</th>
      <td>123879</td>
      <td>8.5</td>
      <td>1950</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Shichinin no samurai</th>
      <td>206216</td>
      <td>8.7</td>
      <td>1954</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>12 Angry Men</th>
      <td>384187</td>
      <td>8.9</td>
      <td>1957</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Les diaboliques</th>
      <td>36725</td>
      <td>8.1</td>
      <td>1955</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Kumonosu-jô</th>
      <td>26012</td>
      <td>8.0</td>
      <td>1957</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Ben-Hur</th>
      <td>141768</td>
      <td>8.1</td>
      <td>1959</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Witness for the Prosecution</th>
      <td>53186</td>
      <td>8.3</td>
      <td>1957</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Dial M for Murder</th>
      <td>92244</td>
      <td>8.1</td>
      <td>1954</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Ikiru</th>
      <td>36638</td>
      <td>8.2</td>
      <td>1952</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>On the Waterfront</th>
      <td>89233</td>
      <td>8.2</td>
      <td>1954</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Les quatre cents coups</th>
      <td>61776</td>
      <td>8.1</td>
      <td>1959</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Paths of Glory</th>
      <td>106038</td>
      <td>8.4</td>
      <td>1957</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>High Noon</th>
      <td>72007</td>
      <td>8.0</td>
      <td>1952</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Vertigo</th>
      <td>218430</td>
      <td>8.4</td>
      <td>1958</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>The Bridge on the River Kwai</th>
      <td>132677</td>
      <td>8.2</td>
      <td>1957</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Rear Window</th>
      <td>280432</td>
      <td>8.5</td>
      <td>1954</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Det sjunde inseglet</th>
      <td>98949</td>
      <td>8.2</td>
      <td>1957</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>The Night of the Hunter</th>
      <td>57974</td>
      <td>8.0</td>
      <td>1955</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Smultronstället</th>
      <td>55861</td>
      <td>8.2</td>
      <td>1957</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Strangers on a Train</th>
      <td>85012</td>
      <td>8.1</td>
      <td>1951</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Le salaire de la peur</th>
      <td>31003</td>
      <td>8.1</td>
      <td>1953</td>
      <td>1950</td>
    </tr>
  </tbody>
</table>
</div>



O ato de criar um novo `DataFrame` através da seleção de certas linhas que satisfaçam alguma condição é chamado de *query*, ou *consulta*. A chamada `imdb_por_nome[imdb_por_nome.get('Decade') == 1950]` é um exemplo de consulta.

#### **Pergunta 4.1.** 

Crie na célula de código abaixo um `DataFrame` chamado `noventa_e_oito`, contendo os filmes em `imdb` lançados em 1998.

*<u>Dica</u>: Lembre mais uma vez da coluna "Year"!*


```python
noventa_e_oito = imdb_por_nome[imdb_por_nome.get("Year") == 1998]
noventa_e_oito
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
      <th>Votes</th>
      <th>Rating</th>
      <th>Year</th>
      <th>Decade</th>
    </tr>
    <tr>
      <th>Title</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Saving Private Ryan</th>
      <td>769893</td>
      <td>8.5</td>
      <td>1998</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>American History X</th>
      <td>694602</td>
      <td>8.5</td>
      <td>1998</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Lock, Stock and Two Smoking Barrels (1998)</th>
      <td>372863</td>
      <td>8.2</td>
      <td>1998</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>The Big Lebowski</th>
      <td>473988</td>
      <td>8.2</td>
      <td>1998</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>The Truman Show</th>
      <td>583004</td>
      <td>8.0</td>
      <td>1998</td>
      <td>1990</td>
    </tr>
  </tbody>
</table>
</div>



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
realmente_bem_avaliados = imdb_por_nome[imdb_por_nome.get("Rating") > 8.6]
realmente_bem_avaliados
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
      <th>Votes</th>
      <th>Rating</th>
      <th>Year</th>
      <th>Decade</th>
    </tr>
    <tr>
      <th>Title</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>The Godfather</th>
      <td>1027398</td>
      <td>9.2</td>
      <td>1972</td>
      <td>1970</td>
    </tr>
    <tr>
      <th>The Shawshank Redemption</th>
      <td>1498733</td>
      <td>9.2</td>
      <td>1994</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Il buono, il brutto, il cattivo (1966)</th>
      <td>447875</td>
      <td>8.9</td>
      <td>1966</td>
      <td>1960</td>
    </tr>
    <tr>
      <th>The Lord of the Rings: The Two Towers</th>
      <td>967389</td>
      <td>8.7</td>
      <td>2002</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>The Dark Knight</th>
      <td>1473049</td>
      <td>8.9</td>
      <td>2008</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>Inception</th>
      <td>1271949</td>
      <td>8.7</td>
      <td>2010</td>
      <td>2010</td>
    </tr>
    <tr>
      <th>Fight Club</th>
      <td>1177098</td>
      <td>8.8</td>
      <td>1999</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>The Godfather: Part II</th>
      <td>692753</td>
      <td>9.0</td>
      <td>1974</td>
      <td>1970</td>
    </tr>
    <tr>
      <th>Shichinin no samurai</th>
      <td>206216</td>
      <td>8.7</td>
      <td>1954</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>Goodfellas</th>
      <td>644556</td>
      <td>8.7</td>
      <td>1990</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>12 Angry Men</th>
      <td>384187</td>
      <td>8.9</td>
      <td>1957</td>
      <td>1950</td>
    </tr>
    <tr>
      <th>The Matrix</th>
      <td>1073043</td>
      <td>8.7</td>
      <td>1999</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>The Lord of the Rings: The Return of the King</th>
      <td>1074146</td>
      <td>8.9</td>
      <td>2003</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>Schindler's List</th>
      <td>761224</td>
      <td>8.9</td>
      <td>1993</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Star Wars: Episode V - The Empire Strikes Back</th>
      <td>700283</td>
      <td>8.7</td>
      <td>1980</td>
      <td>1980</td>
    </tr>
    <tr>
      <th>The Lord of the Rings: The Fellowship of the Ring</th>
      <td>1099087</td>
      <td>8.8</td>
      <td>2001</td>
      <td>2000</td>
    </tr>
    <tr>
      <th>Star Wars</th>
      <td>770011</td>
      <td>8.7</td>
      <td>1977</td>
      <td>1970</td>
    </tr>
    <tr>
      <th>One Flew Over the Cuckoo's Nest</th>
      <td>606395</td>
      <td>8.7</td>
      <td>1975</td>
      <td>1970</td>
    </tr>
    <tr>
      <th>Pulp Fiction</th>
      <td>1166532</td>
      <td>8.9</td>
      <td>1994</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Forrest Gump</th>
      <td>1078416</td>
      <td>8.7</td>
      <td>1994</td>
      <td>1990</td>
    </tr>
  </tbody>
</table>
</div>



Com base em tudo o que vimos acima, podemos agora responder a perguntas mais elaboradas, como: "Qual é a maior avaliação que um filme teve década de 1990?"

Primeiramente, verificamos quais filmes são da década de 1990:


```python
e_da_decada_de_1990 = imdb_por_nome.get("Decade") == 1990
e_da_decada_de_1990
```




    Title
    M                                        False
    Singin' in the Rain                      False
    All About Eve                            False
    Léon                                      True
    The Elephant Man                         False
                                             ...  
    Forrest Gump                              True
    Le salaire de la peur                    False
    3 Idiots                                 False
    Network                                  False
    Eternal Sunshine of the Spotless Mind    False
    Name: Decade, Length: 250, dtype: bool



Em seguida, filtramos apenas por estes filmes em nosso `DataFrame`:


```python
filmes_da_decada_de_1990 = imdb_por_nome[e_da_decada_de_1990]
filmes_da_decada_de_1990
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
      <th>Votes</th>
      <th>Rating</th>
      <th>Year</th>
      <th>Decade</th>
    </tr>
    <tr>
      <th>Title</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Léon</th>
      <td>635139</td>
      <td>8.6</td>
      <td>1994</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Mononoke-hime</th>
      <td>192165</td>
      <td>8.4</td>
      <td>1997</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Saving Private Ryan</th>
      <td>769893</td>
      <td>8.5</td>
      <td>1998</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>In the Name of the Father</th>
      <td>95212</td>
      <td>8.1</td>
      <td>1993</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Before Sunrise</th>
      <td>158867</td>
      <td>8.0</td>
      <td>1995</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>The Silence of the Lambs</th>
      <td>767224</td>
      <td>8.6</td>
      <td>1991</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>The Shawshank Redemption</th>
      <td>1498733</td>
      <td>9.2</td>
      <td>1994</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Heat</th>
      <td>388239</td>
      <td>8.2</td>
      <td>1995</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Toy Story</th>
      <td>535249</td>
      <td>8.3</td>
      <td>1995</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Beauty and the Beast</th>
      <td>268480</td>
      <td>8.0</td>
      <td>1991</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Fight Club</th>
      <td>1177098</td>
      <td>8.8</td>
      <td>1999</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>L.A. Confidential</th>
      <td>376590</td>
      <td>8.3</td>
      <td>1997</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>The Usual Suspects</th>
      <td>656756</td>
      <td>8.6</td>
      <td>1995</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Terminator 2: Judgment Day</th>
      <td>658564</td>
      <td>8.5</td>
      <td>1991</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Goodfellas</th>
      <td>644556</td>
      <td>8.7</td>
      <td>1990</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>American Beauty</th>
      <td>735056</td>
      <td>8.4</td>
      <td>1999</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>The Sixth Sense</th>
      <td>630994</td>
      <td>8.1</td>
      <td>1999</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>La haine</th>
      <td>90937</td>
      <td>8.0</td>
      <td>1995</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Groundhog Day</th>
      <td>384272</td>
      <td>8.0</td>
      <td>1993</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Twelve Monkeys</th>
      <td>415809</td>
      <td>8.0</td>
      <td>1995</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>The Matrix</th>
      <td>1073043</td>
      <td>8.7</td>
      <td>1999</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Unforgiven</th>
      <td>248514</td>
      <td>8.3</td>
      <td>1992</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>American History X</th>
      <td>694602</td>
      <td>8.5</td>
      <td>1998</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Trois couleurs: Rouge</th>
      <td>57644</td>
      <td>8.0</td>
      <td>1994</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Reservoir Dogs</th>
      <td>578684</td>
      <td>8.3</td>
      <td>1992</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Casino</th>
      <td>294394</td>
      <td>8.2</td>
      <td>1995</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Schindler's List</th>
      <td>761224</td>
      <td>8.9</td>
      <td>1993</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>The Green Mile</th>
      <td>672878</td>
      <td>8.5</td>
      <td>1999</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Jurassic Park</th>
      <td>520391</td>
      <td>8.0</td>
      <td>1993</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Lock, Stock and Two Smoking Barrels (1998)</th>
      <td>372863</td>
      <td>8.2</td>
      <td>1998</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Fargo</th>
      <td>395997</td>
      <td>8.1</td>
      <td>1996</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Good Will Hunting</th>
      <td>529800</td>
      <td>8.2</td>
      <td>1997</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Trainspotting</th>
      <td>419372</td>
      <td>8.1</td>
      <td>1996</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Se7en</th>
      <td>895411</td>
      <td>8.6</td>
      <td>1995</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Braveheart</th>
      <td>653769</td>
      <td>8.3</td>
      <td>1995</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Underground</th>
      <td>39447</td>
      <td>8.0</td>
      <td>1995</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>The Big Lebowski</th>
      <td>473988</td>
      <td>8.2</td>
      <td>1998</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>The Lion King</th>
      <td>548750</td>
      <td>8.4</td>
      <td>1994</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>La vita è bella</th>
      <td>358305</td>
      <td>8.6</td>
      <td>1997</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>The Truman Show</th>
      <td>583004</td>
      <td>8.0</td>
      <td>1998</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Pulp Fiction</th>
      <td>1166532</td>
      <td>8.9</td>
      <td>1994</td>
      <td>1990</td>
    </tr>
    <tr>
      <th>Forrest Gump</th>
      <td>1078416</td>
      <td>8.7</td>
      <td>1994</td>
      <td>1990</td>
    </tr>
  </tbody>
</table>
</div>



Encontramos então a maior avaliação apenas entre esses filmes:


```python
filmes_da_decada_de_1990.get('Rating').max()
```




    9.2



Finalmente, podemos fazer tudo isso de forma mais concisa utilizando encadeamento:


```python
imdb_por_nome[imdb_por_nome.get('Decade') == 1990].get('Rating').max()
```




    9.2



Outro exemplo interessante é se lembrarmos da nossa pergunta anterior de qual é o filme mais antigo em `imdb`. Podemos responder à essa pergunta também com uma linha, mas agora utilizando o método `.min()`:


```python
imdb_por_nome[imdb_por_nome.get("Year") == imdb_por_nome.get("Year").min()]
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
      <th>Votes</th>
      <th>Rating</th>
      <th>Year</th>
      <th>Decade</th>
    </tr>
    <tr>
      <th>Title</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>The Kid</th>
      <td>55784</td>
      <td>8.3</td>
      <td>1921</td>
      <td>1920</td>
    </tr>
  </tbody>
</table>
</div>



#### **Pergunta 4.3.**

Nas células de códigos abaixo, utilize o método `.mean()` para encontrar a avaliação média para filmes lançados no século 20 e a avaliação média para filmes lançados no século 21 para os filmes em `imdb`.

*<u>Dica</u>: Lembre que o ano 2000 faz parte do século 20, e que o filme mais antigo do conjunto de dados é de 1921!*


```python
avaliacao_media_do_seculo_20 = imdb_por_nome[imdb_por_nome.get("Year") <= 2000].get("Rating").mean()
avaliacao_media_do_seculo_20
```




    np.float64(8.280113636363636)




```python
avaliacao_media_do_seculo_21 = imdb_por_nome[imdb_por_nome.get("Year") > 2000].get("Rating").mean()
avaliacao_media_do_seculo_21
```




    np.float64(8.23108108108108)



Uma outra quantidade interessante nesse contexto é a propriedade `shape`, que nos informa *quantas linhas* e *quantas colunas* existem em um `DataFrame`. 


```python
imdb_por_nome.shape
```




    (250, 4)



Tecnicamente, uma *propriedade* é similar à um método que não precisa ser chamado adicionando parênteses, e seu tipo é `tuple` (*tuple*, ou *tupla*):


```python
type(imdb_por_nome.shape)
```




    tuple



Assim como um array, você pode obter o primeiro elemento da tupla `shape` utilizando `[0]` e o segundo elemento usando `[1]`. 

*<u>Nota</u>: Os `DataFrames` possuem apenas linhas e colunas, mas existem `array`s com mais de duas dimensões. Nesses casos, `.shape` terá um número de elementos igual ao número de dimensões do objeto correspondente.*

Por exemplo, podemos obter o número de linhas em `imdb_por_nome` acessando:


```python
imdb_por_nome.shape[0]
```




    250



Naturalmente, podemos utilizar esse artifício para descobrir *quantos elementos* (ou, mais precisamente, *quantas linhas*) de um `DataFrame` satisfazem uma certa condição!

Por exemplo, em `imdb`, "Quantos filmes são do século 20?":


```python
imdb_por_nome[imdb_por_nome.get("Year") <= 2000].shape[0]
```




    176



*<u>Nota</u>: Um erro comum nesse contexto é **esquecer de filtrar o `DataFrame` antes de avaliar seu shape**. Nesse caso, se aplicarmos `.shape` à `Series` booleana, teremos o mesmo número de linhas do DataFrame original!*


```python
series_bool = imdb_por_nome.get("Year") <= 2000
series_bool
```




    Title
    M                                         True
    Singin' in the Rain                       True
    All About Eve                             True
    Léon                                      True
    The Elephant Man                          True
                                             ...  
    Forrest Gump                              True
    Le salaire de la peur                     True
    3 Idiots                                 False
    Network                                   True
    Eternal Sunshine of the Spotless Mind    False
    Name: Year, Length: 250, dtype: bool




```python
series_bool.shape[0]
```




    250



#### **Pergunta 4.4.** 

Nas células de código abaixo, utilize `.shape` (e um pouco de aritmética) para encontrar a *proporção* de filmes no conjunto de dados que foram lançados no século 20, e a proporção análoga no século 21.

*<u>Dica 1</u>: A proporção de filmes lançados no século 20 é igual ao número de filmes lançados no século 20, dividido pelo *número total* de filmes no conjunto de dados.*

*<u>Dica 2</u>: Como só existem essas duas possibilidades (século 20 e 21) em `imdb`, a soma de ambas as proporções deve ser igual a 1!*


```python
proporcao_do_seculo_20 = imdb_por_nome[imdb_por_nome.get("Year") <= 2000].shape[0] / imdb_por_nome.shape[0]
proporcao_do_seculo_20
```




    0.704




```python
proporcao_do_seculo_21 = imdb_por_nome[imdb_por_nome.get("Year") > 2000].shape[0] / imdb_por_nome.shape[0]
proporcao_do_seculo_21
```




    0.296



#### **Pergunta 4.5.**

Finalmente, vamos revisitar o DataFrame `populacao_por_ano`, que analisamos no início do laboratório! Na célula de código abaixo, encontre o ano em que a população mundial ultrapassou pela primeira vez os 7 bilhões.

*<u>Dica 1</u>: O índice de `populacao_por_ano` é o ano correspondente, então ao filtrarmos a coluna `Populacao` pela condição de interesse, você pode acessar o índice com `.index`.*

*<u>Dica 2</u>: Tanto a coluna `Populacao` quanto o índice `Ano` já estão ordenados em ordem crescente, então você pode fazer o que se pede utilizando o método `.min()` na Series filtrada.*

*<u>Dica 3</u>: Para evitar escrever o número `7` com nove `0`s, você pode utilizar a notação científica `7e9` para representar 7 bilhões. Embora tecnicamente `7e9` seja um `float` e não um `int`, a comparação produz o mesmo resultado em ambos os casos.*


```python
ano_que_a_populacao_ultrapassou_7_bilhoes = populacao_por_ano[populacao_por_ano.get("Populacao") >= 7e9].index.min()
ano_que_a_populacao_ultrapassou_7_bilhoes
```




    np.int64(2011)



# Linha de chegada 🏁

Parabéns! Você concluiu o Laboratório 1 com sucesso 👏👏👏

Para enviar sua tarefa:

1. Selecione `Kernel -> Restart Kernel and Run All Cells` para garantir que você executou todas as células, incluindo as células de teste.
1. Leia o notebook do começo ao fim com cuidado para ter certeza de que está tudo bem e que todos os testes foram aprovados.
1. Baixe seu notebook usando `File -> Save and Export Notebook As -> HTML` e, em seguida, carregue seu notebook para o Moodle.
