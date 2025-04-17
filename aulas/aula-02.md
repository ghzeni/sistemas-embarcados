# RISC PARADIGM SHIFT

Geralmente, instruções complexas não eram usadas, e o efeito equivalente era obtido por uma sequência de instruções mais simples.
A inclusão de uma única instrução complexa no instruction set poderia impactar a performance geral ao impôr um clock rate menor

> [!NOTE] O clock de um sistema é determinado pela sua instrução complexa mais lenta


- tipos de dados disponiveis da arquitetura cortex (bit, byte, half-word...)
- diagrama de estados de privileged thread etc
- dois tipos de pilha (PSP, MSP)
	- nunca as duas estão ativas ao mesmo tempo
	- como ele muda? de acordo com o diagrama de estados
	- pilha principal -> sistema operacional
	- pilha de processo -> aplicação
- todos os registradores (os 16, sendo que 3 tem uso especial)
- registradores que afetam o estado do ?
- relação de bits
- como funcionam os flags (carry, overflow etc)
- IPSR (0 ou exceção)
- combinação desses registradores (nunca cai um bit em cima do outro)
- significado de cada um dos flags