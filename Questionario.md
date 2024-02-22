# Questionário Sistemas Embarcados I

## 1. Explique brevemente o que é compilação cruzada (***cross-compiling***) e para que ela serve.
A compliação cruzada é um processo que permite desenvolvedores criarem prgramas para dispositivos ou sistemas que não equivalem à plataforma que estão trabalhando 
diretamente, ou seja, eles irão criar códigos exercutáveis para uma plataforma diferente daquela em que o compilador está sendo exerutado. Um exemplo prático disso ocorre quando um desenvolvedor está trabalhando em um computador com arquitetura x86 como um compudador comum, mas deseja compilar um programa para ser executado em um dispositivo móvel com arquitetura ARM, dessa forma ele faria uma compilação cruzada para criar o binário compatível com a plataforma de destino.

## 2. O que é um código de inicialização ou ***startup*** e qual sua finalidade?
Antes mesmo da função main() ser chamada, uma sequência de programas é executada, e um deles é o código de startup, consistindo em instruções ou rotinas que são ativadas imediatamente após a inicialização de um sistema embarcado. Entre essas rotinas inclui inicializar os stacks, adicionar ao stack os argumentos argc e argv, ou qualquer outro parâmetro fornecido via linha de comando, faz a cópia de conteúdos das seções da memória não volátil para a RAM, inicializa a seção .bss com zeros e aloca a tabela de vetores de interrupção na memória. Além disso, o heap é inicializado para permitir a alocação dinâmica de memória conforme necessário pelo programa, para assim finalmente, a função main() ser chamada para iniciar a execução do programa principal. 

## 3. Sobre o utilitário **make** e o arquivo **Makefile responda**:

#### (a) Explique com suas palavras o que é e para que serve o **Makefile**.
O Makefile é um código usado para automatizar a compilação e vinculação de programas e bibliotecas, simplificando um processo que geralmente é complexo devido à grande quantidade de arquivos fonte nos programas. Dentro do arquivo Makefile, encontram-se várias regras que definem como os diferentes componentes de um programa devem ser executados, onde cada regra inclui um target, prerequisites e recipe.

#### (b) Descreva brevemente o processo realizado pelo utilitário **make** para compilar um programa.
O utilitário Make utiliza as regras definidas no arquivo Makefile para automatizar a compilação de programas, assim seguindo uma sequência de passos como a leitura das regras de compilação e dependências do arquivo Makefile, a análise para determinar quais componentes precisam ser compilados e vinculados. Em seguida, verifica os timestamps para identificar quais arquivos foram modificados desde a última compilação, compilando apenas os arquivos fonte alterados ou aqueles cujas dependências foram modificadas, resultando na geração de arquivos objeto correspondentes. Logo depois, vincula os arquivos objeto compilados para criar o executável final do programa e, finalmente, gera o executável final, finalizando o processo de compilação. Durante todo esse processo, o Make evita recompilar arquivos que não foram modificados desde a última compilação e assegura que as regras de compilação definidas no Makefile sejam seguidas adequadamente.

#### (c) Qual é a sintaxe utilizada para criar um novo **target**?
A sintaxe utilizada para criar um novo target é: 

targets: prerequisites
	recipe

Os targets e pré-requisitos são especificados no Makefile como nomes de arquivos separados por espaços. Geralmente, cada regra tem apenas um target, mas em certos casos pode haver mais de um. É crucial observar que a linha de comandos (recipe) associada a um target deve iniciar com uma tabulação.

#### (d) Como são definidas as dependências de um **target**, para que elas são utilizadas?
As dependências dos targets criados são estabelecidas no Makefile através da lista de pré-requisitos, onde cada pré-requisito representa um arquivo ou outro target necessário para construir o target em questão. Ao ser invocado, o Make realiza a verificação dos timestamps dos pré-requisitos em relação aos timestamps do target, garantindo que todas as dependências sejam satisfeitas. Assim, as dependências são declaradas para assegurar que determinados arquivos ou recursos estejam disponíveis antes de compilar um determinado target, evitando a repetição de etapas de compilação desnecessárias e garante que todas as partes do projeto estejam sempre atualizadas.

#### (e) O que são as regras do **Makefile**, qual a diferença entre regras implícitas e explícitas?
As regras do Makefile são instruções que informam duas coisas, quando um target está desatualizado e como atualizá-lo. Diante disso, existem dois tipos de regras, as implícitas e as explícitas, enquanto as regras explícitas definem diretamente quando e como recriar um ou mais targets no Makefile, as regras implícitas são deduzidas pelo Make, que utiliza as extensões dos arquivos para determinar quais comandos executar.

## 4. Sobre a arquitetura **ARM Cortex-M** responda:

### (a) Explique o conjunto de instruções ***Thumb*** e suas principais vantagens na arquitetura ARM. Como o conjunto de instruções ***Thumb*** opera em conjunto com o conjunto de instruções ARM?

### (b) Explique as diferenças entre as arquiteturas ***ARM Load/Store*** e ***Register/Register***.

### (c) Os processadores **ARM Cortex-M** oferecem diversos recursos que podem ser explorados por sistemas baseados em **RTOS** (***Real Time Operating Systems***). Por exemplo, a separação da execução do código em níveis de acesso e diferentes modos de operação. Explique detalhadamente como funciona os níveis de acesso de execução de código e os modos de operação nos processadores **ARM Cortex-M**.

### (d) Explique como os processadores ARM tratam as exceções e as interrupções. Quais são os diferentes tipos de exceção e como elas são priorizadas? Descreva a estratégia de **group priority** e **sub-priority** presente nesse processo.

### (e) Qual a diferença entre os registradores **CPSR** (***Current Program Status Register***) e **SPSR** (***Saved Program Status Register***)?

### (f) Qual a finalidade do **LR** (***Link Register***)?

### (g) Qual o propósito do Program Status Register (PSR) nos processadores ARM?

### (h) O que é a tabela de vetores de interrupção?

### (i) Qual a finalidade do NVIC (**Nested Vectored Interrupt Controller**) nos microcontroladores ARM e como ele pode ser utilizado em aplicações de tempo real?

### (j) Em modo de execução normal, o Cortex-M pode fazer uma chamada de função usando a instrução **BL**, que muda o **PC** para o endereço de destino e salva o ponto de execução atual no registador **LR**. Ao final da função, é possível recuperar esse contexto usando uma instrução **BX LR**, por exemplo, que atualiza o **PC** para o ponto anterior. No entanto, quando acontece uma interrupção, o **LR** é preenchido com um valor completamente  diferente,  chamado  de  **EXC_RETURN**.  Explique  o  funcionamento  desse  mecanismo  e especifique como o **Cortex-M** consegue fazer o retorno da interrupção. 

### (k) Qual  a  diferença  no  salvamento  de  contexto,  durante  a  chegada  de  uma  interrupção,  entre  os processadores Cortex-M3 e Cortex M4F (com ponto flutuante)? Descreva em termos de tempo e também de uso da pilha. Explique também o que é ***lazy stack*** e como ele é configurado. 


## Referências

### Básicas

[1] [STM32F411xC Datasheet](https://www.st.com/resource/en/datasheet/stm32f411ce.pdf)

[2] [RM0383 Reference Manual](https://www.st.com/resource/en/reference_manual/rm0383-stm32f411xce-advanced-armbased-32bit-mcus-stmicroelectronics.pdf)

[3] [Using the GNU Compiler Collection (GCC)](https://gcc.gnu.org/onlinedocs/gcc/index.html)

[4] [GNU Make](https://www.gnu.org/software/make/manual/html_node/index.html)

### Vídeos Microsoft Teams

[5] [05 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[6] [06 - Arquitetura Cortex-M Parte 1/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[7] [07 - Arquitetura Cortex-M Parte 2/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[8] [08 - Microcontroladores STM32](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[9] [10 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

### Material Suplementar

[5] [A General Overview of What Happens Before main()](https://embeddedartistry.com/blog/2019/04/08/a-general-overview-of-what-happens-before-main/)
 
[6] [Bare metal embedded lecture-1: Build process](https://youtu.be/qWqlkCLmZoE?si=mn5yDnJYudQ1PpZH)
 
[7] [Bare metal embedded lecture-2: Makefile and analyzing relocatable obj file](https://youtu.be/Bsq6P1B8JqI?si=yuNLPj3JQ-2IT1yo)
 
[8] [Bare metal embedded lecture-3: Writing MCU startup file from scratch](https://youtu.be/2Hm8eEHsgls?si=c27MpZ47ApiMSwHR)
 
[9] [Lecture 15: Booting Process](https://youtu.be/3brOzLJmeek?si=MsHRUEJP8zofjwJQ)
