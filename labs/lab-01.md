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
Instalar o IDE da Keil versão 5.42a. Há um passo-a-passo da instalação. Interessante ativar a licença “Community”.

## 3. Estrutura de pastas 
Em uma pasta vazia no seu computador, planeje a estrutura futura de pastas para os Labs desta disciplina

![[estrutura-pastas-lab01.png]]

Os arquivos fonte na pasta `userid_ELEW32` devem ser os arquivos de sua autoria, exceto por arquivos específicos de inicialização e configurações (p.ex. configuração do [[linker]]).

## 4. Criação do projeto
Criar um projeto novo na pasta Lab1 a partir do meu github publico: https://github.com/dougrenaux/dougrenaux_ELEW32_public especificamente a pasta **Lab1_blinky**

Verifique o funcionamento deste código. Entenda o que está sendo feito.

## 5. Inclusão de símbolos pré-definidos
Altere o projeto exemplo para incluir atribuir o valor destes símbolos pré-definidos ([[predefined preprocessor symbols]]) à variáveis globais:

- ``__cplusplus`` - modo de compilação C++
- 
``__DATE__``
 ``__TIME__`` 
 ``__FILE__`` 
 ``__LINE__`` 
 ``__STDC__``
``__ARMCC_VERSION`` 
``__TARGET_ARCH_THUMB``
``__STDC_VERSION__`` 

Examine os valores atribuídos e interprete-os. (*dica: acesso o manual online do compilador ARM em uso para entender os valores de cada um destes símbolos)

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
- Como visualizar o valor dos [[predefined preprocessor symbols]]?
- Quais os valores dos [[predefined preprocessor symbols]] que você apresentou? O que significam?
- Quais os comandos referentes a controle da execução (passo-a-passo, step-over, step-out, breakpoints,...) ?
- Como visualizar registradores da CPU?
- Como visualizar registradores de periféricos integrados?
- Como visualizar/modificar endereços específicos de memória?
- Como visualizar o valor de variáveis ou de expressões?
- Por que nem todas as variáveis podem ter seu valor visualizado?