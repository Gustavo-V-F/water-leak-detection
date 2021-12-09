# Detecção de vazamento em tubulações hidráulicas de edificações e residências
Projeto a ser desenvolvido para a avaliação da disciplina de Projeto Integrador 3 do curso de engenharia eletrônica da Instituição Federal de Santa Catarina - Câmpus Florianópolis.

# Problemática
Não é incomum ocorrerem vazamentos e disrupções no sistema de distribuição hidráulicas prediais e residenciais devido ao desgaste, mal dimensionamento e a outros fatores extenuantes. Logo a possibilidade da detecção desses eventos permite avisos e alertas que contribuem para a redução do tempo de resposta como também para a sua automatização.

![Imagem de vazamento de um reservatório para a sua distribuição](/imgs/vazamento.png "Vazamento")

# Projeto
Toma-se conhecimento de que para o projeto devem ser consideradas as restrições da norma [NBR5626 (2020)](#bibliografia) para os valores da pressão estática máxima, de 400 kPa, pressão dinâmica mínima, de 5 até 15 kPa, dependendo da peça, e transientes devido a rápida abertura ou fechamento de válvulas, conhecidos como golpe de aríete, de até 200 kPa somados a pressão estática máxima. Posto isso, é utilizado o experimento realizado por [LI et al. (2019)](#bibliografia) como referência para criar uma prova de conceito com dimensionamento adequado às normas vigentes.

Desse modo, o projeto será constituído por um encanamento de 3 até 6 metros, dois sensores de pressão e, ao menos, duas válvulas em diferentes localidades da tubulação. Também devem ter medidas que suportem as pressões especificadas previamente. Nisso os dois sensores, distanciados de ponta a ponta no cano, detectam ondas de pressão em diferentes instantes no tempo, assim permitindo a descoberta do ponto de vazamento com alta exatidão. De exemplo o experimento de referência é ilustrado abaixo:

![Imagem do experimento de referência](/imgs/setup.png "Experimento")

# Especificações

Para a escolha do sensor de pressão deve-se levar em conta os limites estabelecidos pela norma, onde é considerado uma faixa mínima de 0 até 400 kPa para a sua região de operação e até 600 kPa devido à possíveis transientes. Além disso o tempo de resposta, segundo [HINDERDAEL, M. F.; DE BAERE, D. e GUILLAUME, P. (2016)](#bibliografia), tem de seguir a seguinte equação:

![Equação da incerteza do local do vazamento](https://latex.codecogs.com/gif.latex?\Delta&space;x&space;=&space;\frac{c}{2&space;f_{s}})

Onde _c_ é velocidade do som da onda de pressão negativa de 343 m/s, _f<sub>s<sub>_ é a frequência de amostragem e _&Delta;x_ é incerteza do local do vazamento.

Por exemplo, caso seja assumida uma incerteza de 50 cm, isso implica em uma frequência de 343 Hz. Assim, algumas possibilidades de sensores de pressão que suportem a faixa de pressão operacional e o seu limite de sobrecarga são:

| Sensor/Transdutor                    | [MIK-P300](http://www.meacon.cn/index.php?mod=show&mid=28&pid=52&id=10)  | [Marquardt 2066.2103](https://www.marquardt-shop.com/en/products/switches/sensors/2066/2066.2103.html) | [XDB304](https://portuguese.alibaba.com/product-detail/xdb304-g1-4-1-2mpa-174psi-5-12vdc-0-3m-cable-carbon-steel-alloy-environmental-protection-plating-air-compressor-pressure-sensor-1600057045056.html) | [HDP500](https://pt.aliexpress.com/item/4000315678180.html) |
| :---:                                                       | :---:                                                | :---:           | :---:       | :---:       |
| Faixa de escala de pressão ou _Full Scale_ (F.S.) (MPa)     | 0-0,6                                                | 0-0,45          | 0-0,5       | 0-0,4       |
| Pressão de sobrecarga (% F.S.)                              | 200                                                  | > 200           | 150         | 150         |
| Alimentação (Vdc)                                           | 12-36                                                | 5               | 5-12        | 9-36        |
| Saída                                                       | 4-20mA (HART); 0-20mA (HART); 0-5Vdc; 1-5Vdc; 0-10Vdc; RS485 | 1,125-3,6Vdc    | 0,5-4,5Vdc; 0-5Vdc; 1-5Vdc | 4-20mA (HART) |
| Precisão                                                    | 0,1 % F.S. (0,6 kPa)                                 | 0,52 x pressão(bar) + 1,02 [V] (mínimo) e 0,58 x pressão(bar) + 1,23 [V] (máximo) | 1 % F.S. (5 kPa) | 0,25 % F.S. (1 kPa) |
| Sensibilidade térmica (% F.S./Cº)                           | 0,03                                                 | N/A             | 0,03        | 0,03        |
| Resposta de frequência (kHz)                                | 5 até 650                                            | N/A             | N/A         | 5 até 650   |
| Tempo de resposta (ms)                                      | < 10                                                 | N/A             | <= 3        | <= 50       |
| Temperatura de trabalho (Cº)                                | -40 até 85                                           | -10 até 70      | -20 até 85  | -20 até 70  |
| Temperatura de armazenamento (Cº)                           | -40 até 125                                          | -40 até 90      | N/A         | -40 até 120 |
| Conexão                                                     | G 1/4; G 1/2; 1/2 NPT; 1/4 NPT; M12 * 1,5; M20 * 1,5 | G 3/8           | G 1/4       | M20 * 1,5   |

E as especificações mínimas desejadas do sensor e do projeto são:

| Especificações                                          | Desejadas                |
| :-----------------------------------------------------: | :----------------------: |
| Quantidade de sensores de pressão                       | 2                        |
| Faixa de escala de pressão ou _Full Scale_ (F.S.) (MPa) | 0,4                      |
| Pressão de sobrecarga (% F.S.)                          | 150                      |
| Temperatura máxima de trabalho do sensor (ºC)           | >= 70                    |
| Precisão do sensor                                      | 1 % F.S. (4 kPa)         |
| Frequência de amostragem (Hz)                           | 172                      |
| Tempo de resposta (ms)                                  | <= 6                     |
| Faixa de erro esperado do local de vazamento (m)        | 1                        |
| Comprimento da tubulação (m)                            | 6                        |

# Bibliografia
[1] ASSOCIAÇÃO BRASILEIRA DE NORMAS TÉCNICAS. **NBR 5626: Sistemas prediais de água fria e água quente — 
Projeto, execução, operação e manutenção**. Rio de Janeiro. 2020. Disponível em: <https://www.studocu.com/pt-br/document/universidade-federal-do-espirito-santo/hidraulica/nbr-5626-2020-sistemas-predias-agua-fria-e-agua-quente/9478034>.

[2] LI, J. et al. **A novel location algorithm for pipeline leakage based on the attenuation of negative pressure wave**. Process Safety and Environmental Protection, v. 123, p. 309–316, 2019. ISSN 0957-5820. Disponível em: <https://www.sciencedirect.com/science/article/pii/S0957582019300813>.

[3] HINDERDAEL, M. F.; DE BAERE, D.; GUILLAUME, P.. Proof of Concept of Crack Localization Using Negative Pressure Waves in Closed Tubes for Later Application in Effective SHM System for Additive Manufactured Components. **Applied Sciences**, v. 6, n. 2, p. 33, 1 fev. 2016. Disponível em: <https://www.mdpi.com/2076-3417/6/2/33>.
