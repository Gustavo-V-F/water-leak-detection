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
                                                               
# Protótipo
## Plataforma de *hardware*
Inicialmente é escolhida a placa de desenvolvimento da STMicroelectronics, a placa *Blue Pill*, de codinome STM32F103C8T6, devido aos seus *Analog-Digital
Converters* (ADCs) de 12-bits de alta velocidade, ao seu componente de *Direct Memory Access* (DMA) para redução de uso do processador e amplas ferramentas
de desenvolvimento fornecidas pela STMicroelectronics. Também é utilizado o programador e depurador ST-Link V2 para as operações de gravação e depuração 
por meio da interface *Serial Wire Debug* (SWD).

![Imagem da placa de desenvolvimento Blue Pill](/imgs/blue-pill.jpg "Blue Pill")

## Ambiente de desenvolvimento
O desenvolvimento dá-se no sistema operacional Windows 10 de versão 10.0.19043 (compilação 19043) com o uso da 
[STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html). Essa IDE baseada na *framework* [Eclipse&reg;/CDT&trade;](https://www.eclipse.org/)
já possui integradas as ferramentas [OpenOCD](https://openocd.org/), [GNU *toolchain* para arquitetura ARM](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm), 
[STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html) e [STM32CubeProgrammer](https://www.st.com/en/development-tools/stm32cubeprog.html).

Resumidamente, o fluxo da realização do protótipo segue os seguintes passos:
1. Seleção do microcontrolador, das suas configurações de portas, periféricos, comunicação e geração de código por meio do [STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html);
2. Desenvolvimento do código necessário para a aquisição e transmissão das amostras;
3. Gravação pelo uso da ferramenta [STM32CubeProgrammer](https://www.st.com/en/development-tools/stm32cubeprog.html);
4. E depuração de *hardware* utilizando servidores do *GNU Project Debugger* (GDB) customizados pela STMicroelectronics ou implementados pelo [OpenOCD](https://openocd.org/).
                                                               
## Configuração dos ADCs da placa de desenvolvimento *Blue Pill*
                                      
Faz-se as seguintes configurações para realizar aquisições de forma paralela entre os dois ADCs para a faixa de 0 até 3,3 V:
                                                               
![Imagem da configuração do primeiro ADC](/imgs/adc1.png "Configuração ADC1")

![Imagem da configuração do segundo ADC](/imgs/adc2.png "Configuração ADC2")

![Imagem da configuração do *clock* do ADCs](/imgs/clock.png "Configuração do clock dos ADCs")

Observa-se que o *clock* principal dos ADCs foi reduzido para 562,5 kHz, em que ele é ainda menor devido ao número de ciclos entre amostras de 239,5 ciclos + 14,5 ciclos de atraso inerente a estrutura do ADC [(ST, 2021)](#bibliografia). Isso resulta em aproximadamente 2,2 kHz de frequência de amostragem.
                                                               
### Código para inicialização dos ADCs
                                                               
As inicialização dos ADCs é diretamente no arquivo `main.c`, onde os trechos relevantes são apresentados abaixo:
                                                               
```C
/* Private define ------------------------------------------------------------*/
/* USER CODE BEGIN PD */
#define ADC_BUFFER_SIZE 256
#define ADC_HALF_BUFFER_SIZE_IN_BYTES 2*ADC_BUFFER_SIZE
/* USER CODE END PD */

/* Private macro -------------------------------------------------------------*/
/* USER CODE BEGIN PM */

/* USER CODE END PM */

/* Private variables ---------------------------------------------------------*/

/* USER CODE BEGIN PV */
uint32_t adc_buf[ADC_BUFFER_SIZE];
/* USER CODE END PV */
[...]
int main(void)
{
  [...]
  MX_ADC1_Init();
  MX_ADC2_Init();
  /* USER CODE BEGIN 2 */
  HAL_ADC_Start(&hadc2);
  HAL_ADCEx_MultiModeStart_DMA(&hadc1, adc_buf, ADC_BUFFER_SIZE);
  [...]
```

Nota-se que todos os dados são escritos em um único *buffer*, nisso a componente DMA do microcontrolador automaticamente preenche-o com as aquisições. Além disso também permite adicionar funcionalidades em diferentes momentos de escrita dos dados por meio de suas funções de *callback*, onde são modificadas no trecho de código abaixo:
                                                               
```C
[...]
/* USER CODE BEGIN 4 */
void HAL_ADC_ConvHalfCpltCallback(ADC_HandleTypeDef *hadc){
	CDC_Transmit_FS((uint8_t*)adc_buf, ADC_HALF_BUFFER_SIZE_IN_BYTES);
}

void HAL_ADC_ConvCpltCallback(ADC_HandleTypeDef *hadc){
	CDC_Transmit_FS((uint8_t*)adc_buf + ADC_HALF_BUFFER_SIZE_IN_BYTES, ADC_HALF_BUFFER_SIZE_IN_BYTES);
}
[...]
```
São enviados os pacotes de dados por USB quando o *buffer* estiver preenchido até a metade enquanto os ADCs fazem os restantes das aquisições, e, novamente quando o *buffer* estiver completamente cheio.

### Exemplo em *hardware*

Por meio de dois potênciometros alimentados pela própria placa são modificados os valores de entrada dos ADCs, como visto nas imagens abaixo:

![Imagem da aquisição dos ADCs (exemplo 1)](/imgs/dados1.png "Aquisições ADCs (Exemplo 1)")

![Imagem da aquisição dos ADCs (exemplo 2)](/imgs/dados2.png "Aquisições ADCs (Exemplo 2)")
							    
Nessas imagens o *software* [Realterm](https://sourceforge.net/projects/realterm/) recebeu pela comunicação USB as amostras dos ADCs. Denota-se que seus valores variam na faixa de 2-bits, e, portanto, serão considerados apenas os valores de 10-bits a partir do MSB.
							     
## Sensor

O sensor escolhido para o projeto foi o MPS20N0040D-S [(RADIONICA, 20??)](#bibliografia), que possui as seguintes especificações:

![Imagem do sensor de pressão](/imgs/sensor.png "Sensor de pressão")
							       
| Especificações                                          | MPS20N0040D-S            |
| :-----------------------------------------------------: | :----------------------: |
| Quantidade de sensores de pressão                       | 2                        |
| Faixa de escala de pressão ou _Full Scale_ (F.S.) (MPa) | 0,04                     |
| Pressão de sobrecarga (% F.S.)                          | 300                      |
| Tensão de bias                                          | +-25 mV                  |
| Saída                                                   | 50 mV até 100 mV         |
| Temperatura máxima de trabalho do sensor (ºC)           | -40 até 80               |
| Precisão do sensor                                      | 0,25 % F.S. (0,1 kPa)    |

Vê-se que a saída do sensor é de baixa tensão, logo, ele requer um circuito de amplificação antes de ser conectado a placa.
							       
### Circuito de amplificação
							       
O esquemático do circuito é disponibilizado a seguir:

![Imagem do esquemático do circuito de amplificação](/imgs/circuito-amp.png "Esquemático do circuito de amplificação do sensor")

Nele é realizado no primeiro estágio um ganho de 50 vezes do sinal (de 50 mV até 100 mV para 2,5 V até 5 V), já no segundo estágio é somado e amplificado negativamente com um sinal de referência de -2,5 V (2,5 V até 5 V para -2,5 V até 0 V) e no último estágio é amplificado por -2 (-2,5 V até 0 V para 0 V até 5 V). Seu valor de saída de 0 até 5 V pode ser facilmente reduzido para 0 V até 3,3 V (faixa de tensão dos ADCs) por meio de um divisor resistivo.
							       
### Protótipo do circuito de amplificação
							       
Nas imagens abaixo está o circuito de amplificação montado em bancada:
							       
![Imagem do circuito de amplificação em bancada](/imgs/bancada.jpg "Circuito de amplificação do sensor em bancada")

![Imagem da alimentação](/imgs/alimentacao.jpg "Alimentação do circuito de amplificação do sensor em bancada")

Para simular o comportamento do sensor de pressão foi montada também a ponte H, nela foram trocados valores de resistência para alterar a tensão de comparação. Na sequência de imagens abaixo, estão dispostos 5 multímetros, no topo está a medida de tensão da saída da ponte H, e da direita para a esquerda estão, respectivamente, as medidas de tensão de referência de 2,5 V provida pelo TL413 amplificada por -1 pelo TL072, a tensão amplificada pelo amplificador de instrumentação INA118, a adição das tensões anteriores amplificada por -1 e a saída de 0 V até 5 V na última medida do multímetro.

Para o valor de resistência de 33,9 k:
![Imagem do circuito de amplificação em bancada com valor de resistência de 33,9 k](/imgs/55m.jpg "Circuito de amplificação do sensor em bancada para 33,9 k")

Para o valor de resistência de 34,3 k: 
![Imagem do circuito de amplificação em bancada com valor de resistência de 34,3 k](/imgs/65m.jpg "Circuito de amplificação do sensor em bancada para 34,3 k")

Para o valor de resistência de 35,11 k: 
![Imagem do circuito de amplificação em bancada com valor de resistência de 35,11 k](/imgs/85m.jpg "Circuito de amplificação do sensor em bancada para 35,11 k")

Para o valor de resistência de 36 k: 
![Imagem do circuito de amplificação em bancada com valor de resistência de 36 k](/imgs/95m.jpg "Circuito de amplificação do sensor em bancada para 36 k")
	
## Protótipo em bancada

Para efeitos de teste, foi utilizado um cano de 3 metros de comprimento com vazamentos simulados por torneiras instaladas à 0,975 metros e 2,51 metros do sensor mais próximo da entrada de água. E os dois sensores são distanciados por 2,955 metros. O protótipo é apresentado abaixo:
							       
![Imagem do protótipo contruído para os testes](/imgs/prototipo.jpg "Protótipo em bancada")

### Resultados 

Foram realizados dois testes de 1 minuto cada ao todo, por meio do *script* python abaixo as aquisições recebidas por USB foram armazenadas em arquivos .csv.
							       
```Python
import serial
import csv

csv_filename = 'pressure_sensor_data_raw' # Change to 'pressure_sensor_data_raw2' for second dataset
header = ['t','sensor0', 'sensor1']
sensor0 = [0, 0];
sensor1 = [0, 0];
total_time = 60;
sample_freq = 562500/(239.5+14.5); # ADCs sampling frequency / (selected number of cycles + ADCs delay in cycles)
sample_time = 1/sample_freq;
sample_amount = int(round(total_time/sample_time));

# NOTE the user must ensure that the serial port and baudrate are correct
serPort = "/dev/ttyACM0";
baudRate = 115200;
ser = serial.Serial(serPort, baudRate);
print("Serial port " + serPort + " open:  Baudrate " + str(baudRate));

with open(csv_filename+'.csv', 'w', encoding='UTF8', newline='') as pressure_sensor_data:
    data_write = csv.writer(pressure_sensor_data)
    
    # write the header
    data_write.writerow(header)
    
    #print(str((((int.from_bytes(sensor0[1], "little") << 8) + int.from_bytes(sensor0[0], "little")) >> 2)) + ', ' 
    #      + str((((int.from_bytes(sensor1[1], "little") << 8) + int.from_bytes(sensor1[0], "little")) >> 2)) + ';');
    for i in range(0, sample_amount):
        sensor0[0] = ser.read();
        sensor0[1] = ser.read();
        sensor1[0] = ser.read();
        sensor1[1] = ser.read();
        
        # write the data
        data_write.writerow([i*sample_time,
                            str((((int.from_bytes(sensor0[1], "little") << 8) + int.from_bytes(sensor0[0], "little")) >> 2)),
                            str((((int.from_bytes(sensor1[1], "little") << 8) + int.from_bytes(sensor1[0], "little")) >> 2))])
    print('Finished writing to '+ csv_filename +'.csv');
```

No primeiro teste (`'python/pressure_sensor_data_raw.csv'`) teve de ser ajustado por potenciômetros de 10 kOhms as saídas do INA118 (ao invés de apenas resistores de 10 kOhms) para compensar a tensão de bias do sensor, os dados obtidos dos sensores resultaram nos dois gráficos a seguir:

![Imagem do gráfico do primeiro teste](/imgs/plot_sensor_saturado.png "Gráfico do primeiro teste")

Nele observa-se platôs devido a saturação do sinal amplificado para a entrada dos ADCs, eles causam discrepâncias no cálculo da distância do vazamento, logo não é possível obtê-los.
	
Já no segundo teste (`'python/pressure_sensor_data_raw2.csv'`) foi feito um ajuste para diminuir a sensibilidade do ganho de amplificação, assim esperava-se que os valores estivessem dentro da faixa de 0 V até 3,3 V da entrada dos ADCs. No entanto ainda nota-se saturação, mesmo que não tão intensa como no primeiro teste, como pode ser visto nos gráficos abaixo:
	
![Imagem do gráfico do segundo teste](/imgs/plot_sensor.png "Gráfico do segundo teste")

Por inspeção visual vê-se que há uma queda brusca de pressão entre 3,0 e 3,4 segundos nos dois sensores, onde os símbolos **x** verdes representam pontos de máximo local, e os vermelhos, pontos de mínimo local. Nisso foi calculado o ponto de vazamento utilizando o *script* Python abaixo:
	
![Imagem do gráfico do primeiro vazamento](/imgs/plot_sensor_primeiro.png "Gráfico do primeiro vazamento")

```Python
def mean_time_delta(n2, n1, n4, n3):
    return abs((n2-n1+n4-n3)/2);

def leak_point(pipeline_length, time_delta, npw_speed=360.56, fluid_speed=1):
    # From upstream
    return (pipeline_length+time_delta*(npw_speed-fluid_speed))/2;
    
time0_max = np.asarray(t)[maxima0.astype(int)];
time0_min = np.asarray(t)[minima0.astype(int)];

time1_max = np.asarray(t)[maxima1.astype(int)];
time1_min = np.asarray(t)[minima1.astype(int)];

measured_length = 2.955;    

time_delta2510 = mean_time_delta(time0_max[2], time1_max[3], time0_min[3], time1_min[4]);
leak2510 = leak_point(measured_length, time_delta2510);

print("Vazamento no ponto de 2,51 m:")
print("Diferença de tempo média entre os dois sensores =", time_delta2510);
print("Distância do vazamento calculada =", leak2510);
```

Disto teve-se um resultado de 2,41 metros, que representa um erro de 3,94 % comparado ao real de 2,51 metros. E para o segundo vazamento foi realizado o cálculo para a região entre 39,5 segundos e 40,5 segundos a partir da imagem abaixo.
	
![Imagem do gráfico do segundo vazamento](/imgs/plot_sensor_segundo.png "Gráfico do segundo vazamento")

```Python
time_delta975 = mean_time_delta(time0_max[27], time1_max[15], time0_min[28], time1_min[17]);
leak975 = leak_point(measured_length, time_delta975);

print("Vazamento no ponto de 0,975 m:")
print("Diferença de tempo média entre os dois sensores =", time_delta975);
print("Distância do vazamento calculada =", leak975);
```
	
O cálculo resulta em um valor de 11,58 metros, que é incompatível com o valor na realidade de 0,975 metros. Isso ocorre devido a saturação, a curva não coincide perfeitamente nos mesmos pontos, e portanto, não é válida.

## Resolução de problemas
Infelizmente, devido a pandemia e múltiplos fatores que afetaram a indústria tecnológica, a escassez de *chips* se tornou algo comum, dando espaço para
dispositivos alternativos e clones de microcontroladores. Nisso, certas funcionalidades como as de depuração e gravação podem não ser suportadas 
pela fabricante para tais dispositivos, como é o caso da STMicroelectronics.

![Imagem de erro de verificação de dispositivo original da STMicroelectronics](/imgs/not-supported.png "Sem suporte")

O autor desse projeto possui um clone, com um microcontrolador de código CS32F103C8T6, o que implica no não funcionamento das ferramentas de depuração 
customizadas pela STMicroelectronics, sendo necessárias configurações adicionais para a execução da depuração:

1. Alterar a opção de *Debug Probe* para ST-Link (OpenOCD);

    ![Imagem do primeiro passo para execução da depuração](/imgs/1-step-dbg.png "Primeiro passo")

2. Habilitar a opção *Show generator options*;

    ![Imagem do segundo passo para execução da depuração](/imgs/2-step-dbg.png "Segundo passo")

3. Mudar frequência de 8 MHz para 4 MHz em *Connection Setup*, habilitar a opção *Enable debug in low power mode* e selecionar *Software system reset* na opção *Reset Mode*;

    ![Imagem do terceiro passo para execução da depuração](/imgs/3-step-dbg.png "Terceiro passo")
    
4. Clicar na opção *Show Command Line*, selecionar todo o texto na nova janela que surge e selecione a opção *Copy & Close*;
 
    ![Imagem do quarto passo para execução da depuração](/imgs/4-step-dbg.png "Quarto passo")
    
5. Executar a opção *Debug*, no que ocorrerá uma falha para identificar o dispositivo, porém o arquivo de configuração necessário ainda é gerado;

    ![Imagem do quinto passo para execução da depuração](/imgs/5-step-dbg.png "Quinto passo")
    
6. Dentro do menu *Debug Configurations* adicione uma nova configuração dentro da seção *GDB Hardware Debugging*;
 
    ![Imagem do sexto passo para execução da depuração](/imgs/6-step-dbg.png "Sexto passo")
    
7. Na aba *Debugger* escreva dentro da caixa de texto *GDB Command*:
    ```
    ${gnu_tools_for_stm32_compiler_path}\arm-none-eabi-gdb.exe
    ```
    Também habilite a opção *Use remote target* e selecione a opção *OpenOCD (via socket)* em *JTAG Device*;
    
    ![Imagem do sétimo passo para execução da depuração](/imgs/7-step-dbg.png "Sétimo passo")
    
8. Dentro do menu *External Tools Configurations* adicione uma nova configuração;
 
    ![Imagem do oitavo passo para execução da depuração](/imgs/8-step-dbg.png "Oitavo passo")
    
9. Na aba *Main*, escreva no campo *Location*:
    ```
    ${stm32cubeide_openocd_path}\openocd.exe
    ```
    Já no campo *Working Directory* digite:
    ```
    ${project_loc}
    ```
    E no campo *Arguments* é possível colar o texto copiado no item 4 ou digitar o código abaixo:
    ```
    "-f" ${project_name}.cfg "-s" ${project_loc} "-s" ${stm32_openocd_script_root_path} "-s" ${stm32_openocd_alt_script_root_path} "-c" "gdb_report_data_abort enable" "-c" "gdb_port 3333" "-c" "tcl_port 6666" "-c" "telnet_port 4444"
    ```
    Onde, caso seja utilizado o código acima, deve ser adicionada a variável ```${stm32_openocd_alt_script_root_path}``` que provém a substituição para o caminho:
    ```
    C:\ST\STM32CubeIDE_1.8.0\STM32CubeIDE\plugins\com.st.stm32cube.ide.mpu.debug.openocd_2.0.100.202110211057\resources\openocd\st_scripts
    ```
    No que seu caminho é diferente do apresentado pela variável ```${stm32_openocd_script_root_path}```.
    
    ![Imagem do nono passo para execução da depuração](/imgs/9-step-dbg.png "Nono passo")
    
10. Agora para iniciar o servidor GDB para a depuração deve ser executado o *External Tool* configurado nos itens 8 a 9, 
    e depois deve ser executada a configuração de depuração realizada nos itens 6 a 7. Ao final o depurador é iniciado com sucesso!

# Bibliografia
[1] ASSOCIAÇÃO BRASILEIRA DE NORMAS TÉCNICAS. **NBR 5626: Sistemas prediais de água fria e água quente — 
Projeto, execução, operação e manutenção**. Rio de Janeiro. 2020. Disponível em: <https://www.studocu.com/pt-br/document/universidade-federal-do-espirito-santo/hidraulica/nbr-5626-2020-sistemas-predias-agua-fria-e-agua-quente/9478034>.

[2] LI, J. et al. **A novel location algorithm for pipeline leakage based on the attenuation of negative pressure wave**. Process Safety and Environmental Protection, v. 123, p. 309–316, 2019. ISSN 0957-5820. Disponível em: <https://www.sciencedirect.com/science/article/pii/S0957582019300813>.

[3] HINDERDAEL, M. F.; DE BAERE, D.; GUILLAUME, P.. Proof of Concept of Crack Localization Using Negative Pressure Waves in Closed Tubes for Later Application in Effective SHM System for Additive Manufactured Components. **Applied Sciences**, v. 6, n. 2, p. 33, 1 fev. 2016. Disponível em: <https://www.mdpi.com/2076-3417/6/2/33>.
  
[4] ST. **RM008 Reference manual**. 2021. Disponível em: <https://www.st.com/resource/en/reference_manual/cd00171190-stm32f101xx-stm32f102xx-stm32f103xx-stm32f105xx-and-stm32f107xx-advanced-arm-based-32-bit-mcus-stmicroelectronics.pdf>
	
[5] RADIONICA. **Pressure Sensor MPS20N0040D-S**. 20??. Disponível em: <https://softroboticstoolkit.com/files/sorotoolkit/files/mps20n0040d-s_datasheet.pdf>
