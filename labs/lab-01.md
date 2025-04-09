Lab 1

# Objetivos:

1. Validar a infraestrutura laboratorial necessária para os próximos experimentos: Keil uVision, Kit da placa Tiva e Github.
	- Opcionalmente: *Doxygen*.
2. Entender as principais funcionalidades disponíveis no ambiente de desenvolvimento Keil uVision.

# Passo-a-passo

## 1. GitHub para versionamento
Usem o Github para gerenciar versões do código e compartilhar com seu colega de equipe.

Opcionalmente, usem o Doxygen de forma a documentar o código de cada lab no próprio código fonte. Ver dicas de uso nos slides a seguir.

Não criem branches para cada um dos Labs.

## 2. Instalação da IDE
Instalar o IDE da Keil versão 5.42a. Há um passo-a-passo da instalação. Interessante [[ativar-licenca-community|ativar a licença “Community”]].

## 3. Estrutura de pastas 
Em uma pasta vazia no seu computador, planeje a estrutura futura de pastas para os Labs desta disciplina

![[estrutura-pastas-lab01.png]]

Os arquivos fonte na pasta `userid_ELEW32` devem ser os arquivos de sua autoria, exceto por arquivos específicos de inicialização e configurações (p.ex. configuração do [[linker]]).

## 4. Criação do projeto
Criar um projeto novo na pasta Lab1 a partir do meu github publico: https://github.com/dougrenaux/dougrenaux_ELEW32_public especificamente a pasta **Lab1_blinky**

Verifique o funcionamento deste código. Entenda o que está sendo feito.

## 5. Inclusão de símbolos pré-definidos
Altere o projeto exemplo para incluir atribuir o valor destes símbolos pré-definidos ([[predefined preprocessor symbols]]) à variáveis globais:

``__cplusplus`` 
``__DATE__``
 ``__TIME__`` 
 ``__FILE__`` 
 ``__LINE__`` 
 ``__STDC__``
``__ARMCC_VERSION`` 
``__TARGET_ARCH_THUMB``
``__STDC_VERSION__`` 

Examine os valores atribuídos e interprete-os. (*dica: acesso o [manual online do compilador ARM em uso](https://developer.arm.com/documentation/dui0375/g/Compiler-specific-Features/Predefined-macros) para entender os valores de cada um destes símbolos)

Pergunta #1: **Que cuidados você precisará ter para que o compilador não descarte estes valores?**

## 6. Execução na placa
Certifique-se que nas opções de configuração de projeto:

- Texas TM4C1294NCPDT com coprocessador numérico
- Depurador usado: Stelaris ICDI.

O código deve ser executado na placa Tiva, não use o simulador.

## 7. Durante a execução
Ao executar o programa,

Pergunta #2: **Como visualizar o valor dos símbolos pré-definidos?**

Pergunta #3: **Quais os valores dos símbolos pré-definidos que você apresentou? O que significam?**

## 8. Depuração

- Quais os comandos referentes a controle da execução (passo-a-passo, step-over, step-out, breakpoints,...) ?
- Como visualizar registradores da CPU?
- Como visualizar registradores de periféricos integrados?
- Como visualizar/modificar endereços específicos de memória?
- Como visualizar o valor de variáveis ou de expressões?
- Por que nem todas as variáveis podem ter seu valor visualizado?


# Questionário

- Que cuidados você precisará ter para que o compilador não descarte os valores dos [[predefined preprocessor symbols]]?

R: Para que os valores não sejam descartados pelo compilador, eles precisam estar sendo usados na main. A equipe encontrou informações sobre o uso do modificador `volatile` mas mesmo adicionando antes da declaração das variáveis, os valores continuaram inacessíveis durante o runtime pelo debugger.

- Como visualizar o valor dos [[predefined preprocessor symbols]]?
R: Adicionando-os a um `printf` e monitorando seus valores via *Watch*

- Quais os valores dos [[predefined preprocessor symbols]] que você apresentou? O que significam?

Endereço de memória em que estão armazenados e valor armazenado nos símbolos, respectivamente.

``__DATE__``:  0x00001578 "Apr  6 2025" | Data da compilação do arquivo
 ``__TIME__``: 0x00001584 "15:39:09" | Hora da compilação do arquivo
 ``__FILE__``: 0x0000158F "src_other/main.c" | Caminho e nome do arquivo
 ``__cplusplus``: 0x0000158D "C" | 

Os demais valores retornaram ``<cannot evaluate>``. Talvez por conta da mudança de versão de compilador ou forma com que os valores foram inicializados pela equipe. 


- Quais os comandos referentes a controle da execução (passo-a-passo, step-over, step-out, breakpoints,...) ?
F5: Run
F11: Step
F10: Step-over
Ctrl+F11: Step-out
F9: Insert/remove Breakpoint
Ctrl+B: Visualizar Breakpoints

- Como visualizar registradores da CPU?
R: Durante o Debugger, os registradores aparecem listados na janela à esquerda.

- Como visualizar registradores de periféricos integrados?
R: Durante a execução do Debugger, é possível acessar registradores específicos clicando em View -> System Viewer -> `<periférico desejado>` -> `<registrador desejado>`

## Método 1: Usando a Janela "Peripherals" (Recomendado)

1. **Inicie a sessão de debug**:
    - Clique no ícone "Start/Stop Debug Session" (ou Ctrl+F5)
2. **Acesse os periféricos**:
    - Menu: **View → Peripherals → System Viewer**
    - Selecione o periférico desejado (ex: GPIO, TIMER, UART)
3. **Navegue pelos registradores**:
    
    - A janela mostrará todos os registradores do periférico selecionado
        
    - Valores em vermelho indicam modificações recentes

- Como visualizar/modificar endereços específicos de memória?
R: Adicionando uma variável à `Memory`, é possível alterar manualmente seus endereços de memória.

- Como visualizar o valor de variáveis ou de expressões?
R: Basta adicionar o valor delas ao Watch.

- Por que nem todas as variáveis podem ter seu valor visualizado?
R:

# Dúvidas
1. De que forma o compilador descarta as variáveis?
	1. Qual dessas formas está acontecendo nessa situação?