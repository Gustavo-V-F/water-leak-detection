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
