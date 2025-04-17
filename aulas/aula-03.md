pq importante assembly em embarcados?
	- se vc programa bem em assembly, impossivel ter um código em melhor performance

- resolver bugs porque entendemos o que tá acontecendo em assembly

# Instruction Set
NVIC - controlador de interrupções
MPU - unidade de proteção de memória
FPU - unidade de proteção de ponto flutuante
- muitas instruções dão suporte a DSP
```
label: MNEMONIC Destination, Operand1, Operand2 ;comment
```
- columa 1 reservado pra label, nunca vamos colocar codigo de instrução na coluna um
- Mnemônico é tipo a função (em nível de máquina)

--
Barrel Shifter - deslocamento: a mesma instrução que tá fazendo logica e aritmetica tambem esta fazendo um deslocamento

Instruction register - alguns dos bits do codigo binario viram uma constante, e a constante cai aqui

cerquilha indicando constante codificada dentro instrução

uma instrução tem ou 16 ou 32 bits... pq? por causa do tamanho dos bytes/bits?

16
ADD | dest R0 | op1 é R5 | sobram poucos bits pra dizer qual é o valor imediato

MOV R0, #0xE000E000 só posso codificar pq ela repete

1. "isso cabe em 8 bits?"
2. "ele cabe num desses padrões aqui?"
	1. se sim, consigo usar uma instrução MOV Rqqr, # 
	2. MOV e MOVT
	3. LDR - guardo uma constante em memoria e depois leio a constante

unsigned: valem os flags Z e C
com sinal, vale o Z, V e N

instruções sempre vão mexer com todos os flags, nós é que vamos interpretar se for operando sem sinal interpretar os 2 de cima, se for com sinal interpretar os 3

S no final (ADDS) significa modifica os flags.

interpretar os flags alterados pela instrução pra ir por um caminho ou por outro

ITT - prefixo pra instruções condicionais
ADDEQ só vai ser executada pra uma certa combinação de flags
e ADDSEQ s'ovai ser executada pra outra combinação de flags

Entender exatamente o que está acontecendo em cada caso.

# IT Block
If Then xyz
xyz pode ser T (then) ou E (else)

ITTE EQ
ADDEQ
SUBEQ
ORRNE (inverter EQ - Not Equal)
se cabe no maximo 4, só pode ter 3 dps dele (conferir)

BCC pode ser dentro de um IT ou fora

**Último bit do PC é sempre 0**
No nosso caso, o PC sempre tem que estar em 1 (Thumb)

Salto pra endereço ímpar?
Último bitzinho não é endereço, é o flag T

Quais são as instruções que interpretam último bit como sendo o flag T?
- BX
- BLX
- pop {PC}

- pq faria uma soma de 32 bits com carry?
- operações com 64 -> gera carry -> soma na parte alta

- LSR só funciona com divisão por 2 se for sem sinal
- ASR -> divisão por 2 com números com sinal

# ROR rotate right
girar 4 pra um lado é o mesmo que girar 28 pro outro

- exercicio de assembly no display_minimal do professor

- o que é little endian? "termina no endereço menor"?
big-endian: não usamos. Processadores antigos. Não é necessário entrar em detalhes.
A figura de cima é a importante.

---
- Endereço sempre está num registrador. Rn é o registrador de endereços.
- Memória é um vetor de 4GB, o que tem dentro do colchetes é a posição na memória.
- `[Rn, #off]` soma o valor e então tenho o endereço.
- colocar um segundo registrador como sendo o offset
	- variavel em c que é o indice do vetor
	- `[Rn sendo inicio do vetor, posição do vetor]` tipo em C
	- primeiro calculo o endereço, depois vou na memoria e leio (LDR nesse caso)
---
push = stmfd (f de full d de descend)
pop = LDMFD

---
cenário que demandou a instrução de barreiras: efeito esteja efetivo antes de executar a instrução seguinte

---
BL e BLX mexem no flag T

---
se a ultima instrução de uma rotina for um pop pc significa vá na pilha tire o valor que tá no topo da pilha e coloque no pc -- ao fazer isso estou executando um salto

---
barreiras: segurar o processador

### DMB
segura o próximo acesso a memória

DSB
apenas esperando dado chegar na memória

10:33
lab2 registrador VTOR reprogram a posição da tabela de vetores de exceção
normalmente nasce em 0 mas através do VTOR posso reconfigurar 

ISB
O efeito de mexer no VTOR tem que ser finalizado. NVIC tem que avisar.
_efeito_

## DMB DSB ISB raro de usar

instruções de barreira esperam chegar num determinado ponto antes de continuar execução

DMB: usar depois de alterar o vetor e habilitar o IRQ correspondente
ISB depois de alterar código

DSB: ?

---
