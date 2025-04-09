# TivaWare

As instruções para o Lab2 estão no arquivo Lab2_Tiva_Keil_2023_2.  
O arquivo Keil MDK - New project apresenta explicações de como criar um projeto novo no uVision.  
O arquivo modelo lab mostra as seções para um relatório de laboratório. Lembre-se que o relatório deve ser no readme.md.   
Adicionalmente, incluo o manual "getting started" do MDK.  
  
Adicionalmente ao solicitado no pdf abaixo, inclua no relatório as respostas ao seguinte:  
Na situação em que a execução está parada na primeira linha da função main, logo após a carga do programa.  
- qual o valor do registrador VTOR e que este valor significa?  
- qual o valor corrente do PC e o respectivo significado?  
- qual o valor corrente do registrador CONTROL e o que isto significa (examine cada campo deste registrador)  
- qual o valor corrente do registrador xPSR e o que isto significa (examine cada campo deste registrador)  
- quem está em uso, o MSP ou o PSP? qual seu valor? para onde ele aponta (RAM, Flash)?

---
# Introdução
_A que se refere este relatório. Qual o experimento, objetivos do experimento,
objetivos de aprendizado._

# Planejamento das fases do processo de desenvolvimento
_Liste a sequência de etapas a serem seguidas para resolução deste Lab. Observe
um slide do enunciado a respeito deste planejamento._

# Definição do problema a ser resolvido
_Descreva o problema a ser resolvido sem falar da solução a ser elaborada para resolver este problema._

# Especificação da solução
_Descreva (informalmente) a solução a ser implementada.
Elabore uma especificação para a solução do problema – observe um slide sobre esta especificação. Identifique quais itens da especificação se referem a funcionalidade implementada na solução e quais itens se referem a características não funcionais e restrições impostas ao processo de desenvolvimento._

# Estudo da plataforma de HW
_A partir do estudo da documentação da placa da Tiva e seu processador, registre aqui aspectos importantes para este experimento. Por exemplo: qual a frequencia do cristal usado na placa, como (em que pinos) os botões e leds estão conectados, qual o nível de sinal corresponde a led aceso ou apagado, qual o nível de sinal que corresponde ao botão estar pressionado. Quantos bits tem o contador do SysTick, qual a máxima contagem deste, que período de tempo isto representa considerando a configuração do clock._

# Estudo da plataforma de SW
_Identifique na documentação do Tivaware, quais as funções que seriam uteis para a solução planejada. Como configurar o clock do processador, como acessar o SysTick, e as interrupções, como interagir com GPIO, como gerar interrupções a partir do GPIO, como garantir que o vetor de exceções está na Flash._

# Projeto (design) da solução
_Planeje como será a implementação da solução. Que funções do Tivaware, dentre
as identificadas na seção acima, efetivamente serão utilizadas. Em se tratando de uma solução a ser implementada exclusivamente em SW (não será necessário nenhum desenvolvimento de HW), apresente diagramas de como o SW irá operar. Utilize notação padronizada (ou seja, UML) para apresentar diagramas._

# Configuração do projeto na IDE (Keil uVision).
_Liste as configurações relevantes que devem ser setadas no projeto no IAR-
EWARM. Certifique-se que você sabe o que as configurações significam e esteja
preparado para defender suas escolhas durante a apresentação do lab._

# Teste e depuração.
_Planeje que testes você fará para garantir que a especificação foi efetivamente
implementada. 
Como você pode garantir que a frequência do clock é aquela que planejou ser? 
Como garantir que as medidas de tempo apresentadas estão corretas?_

---

# Lab 2 – interagindo com a placa Tiva

1. Obtenha o TivaWare versão 2.2.0.295
2. Estudando o TivaWare
	1. a) na pasta examples/boards/ek-tm4c1294xl, abram o projeto project0, revisem as configurações, executem. Estudem este projeto principalmente do ponto de vista de inicialização do clock e inicialização / uso do GPIO.
	2. b) na pasta examples/boards/ek-tm4c1294xl, abram o projeto watchdog, revisem as configurações, executem. Estudem este projeto principalmente do ponto de vista de interrupções com ISRs em Flash.

ATENÇÃO: as diretivas IF :DEF: ELSE e ENDIF são do compilador/assembler v5 e não são compatíveis com a versão 6 usada neste semestre. Se houver erros de compilação causados nestas linhas, substituam pelas diretivas atuais de pré-processamento: ``#ifdef #else #endif``
- As funções do TivaWare “sabem” se adaptar aos diferentes modelos de processadores da família TM4C. De que maneira informamos ao ambiente de compilação qual o processador que estamos usando?
- O que significa o prefix MAP_ antes das chamadas de funções do TivaWare, a exemplo de: ``MAP_SysCtlPeripheralEnable``

3. Na pasta seuid_ELEW32, crie uma pasta Lab2.
4. Entenda como é o processo de inicialização que ocorre antes da função main ser chamada. Dica: na configuração de depuração, deselecione o “Run to main”, assim você poderá executar passo-a-passo, até mesmo em assembly, o processo de inicialização.

	**Inclua no seu relatório a sua explicação deste processo de inicialização.**

5. Crie um projeto novo na pasta Lab2. Observe cuidadosamente as opções de projeto dos projetos exemplo estudados anteriormente.
	
	Observe o pdf que descreve a criação de um projeto no Keil-MDK.

![[Criando um projeto no Keil.png]]

# Objetivo

O objetivo da aplicação a ser desenvolvida no Lab2 é medir o tempo de reação do usuário, isto será feito acendendo um LED e medindo o tempo até o usuário pressionar um botão. Pode até ser entendido como um jogo onde o objetivo é responder no menor tempo possível.

---
Um projeto bem elaborado deve incluir as seguintes atividades:

1. Planejamento das fases do processo de desenvolvimento.
2. Definição do problema a ser resolvido.
3. Especificação da solução (use a especificação no próximo slide como referência e faça os refinamentos que julgar necessário).
4. Estudo da plataforma de HW (placa Tiva e seu processador).
5. Estudo da plataforma de SW (TivaWare).
6. Projeto (design) da solução.
7. Identificação (e entendimento) da funcionalidade do TivaWare e do HW que serão utilizadas na solução.
8. Configuração do projeto na IDE (Keil uVision).
9. Edição do código da solução.
10. Teste e depuração.
11. Entrega dos resultados (sincronizar seu código com o seu GitHub e relatório no formato .md).

# Lab 2 - Especificação
Requisitos funcionais:
RF1 - O jogo deve ligar o LED D1 para informar ao jogador o início da contagem de tempo.
RF1.1 - O LED deve ser aceso até 1 segundo após o início da operação da placa.
RF2 - O jogo usa o botão SW1 para entrada de dados pelo usuário.
RF3 - O jogo deve apresentar a contagem de tempo no Terminal Serial indicando o número de clocks entre o LED acender e o botão SW1 ser pressionado e o valor de tempo correspondente em ms.

Requisitos e Restrições não funcionais:
RNF 1 - O limite superior de contagem de tempo é o equivalente a 3 segundos.
RNF 2 - Usar o SysTick como temporizador.
RNF 3 - Usar funções da TivaWare para acesso a I/O, SysTick e temporização.
RNF 4 - A solução deve fazer uso de interrupções, obrigatoriamente de GPIO e opcionalmente do SysTick.
RNF 5 – O vetor de exceções deve estar em memória Flash e não na RAM.
Prof. Douglas Renaux - disciplina Sistemas Embarcados - UTFPR

Questões:
- Qual o papel do registrador VTOR de um Cortex-M4? Em que periférico integrado está localizado?
- Consultando o valor corrente do VTOR é possível saber se o vetor de exceções está na Flash ou na RAM?
- Que funções do TivaWare alteram a posição do vetor de exceções? Por quê?

Entrega
• Sincronizar o código fonte do Lab2 e arquivos de configuração com o
seu github. Os projetos exemplo do TivaWare não devem ser colocados no github.
• Incluir um readme.md na pasta do Lab2 (no github) com o relatório deste experimento.
• O relatório deve tratar dos passos 1 a 10. O formato deste relato está no arquivo em anexo. Use o arquivo anexo apenas como referência pois a submissão é no readme.md. Submeter apenas uma entrega por equipe. O relatório também deve responder a todas as questões colocadas no enunciado deste experimento. Acrescente mais seções se necessário. Estimo cerca de 8 a 10 páginas em cada relatório.