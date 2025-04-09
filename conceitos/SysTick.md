SysTick é um temporizador (timer) embutido em microcontroladores ARM Cortex-M.

1. **Timer de sistema**: É um contador descendente de 24 bits que faz parte do núcleo Cortex-M.
2. **Propósito principal**: Fornecer um mecanismo simples para gerar interrupções em intervalos regulares, útil para:
    
    - Sistemas operacionais em tempo real (RTOS) para troca de tarefas
    - Medição de tempo
    - Criação de atrasos (delays) precisos

## Como ele é usado no código do blinky?

No código do blinky, ele é usado da seguinte forma:

```
SysTick_Config(SystemCoreClock / 1000ul);  /* Setup SysTick for 1 msec */
```

- `SystemCoreClock` é a frequência do clock do processador (em Hz)
- Dividindo por 1000, o timer irá gerar uma interrupção a cada 1ms

## A interrupção do SysTick

A função `SysTick_Handler` é chamada automaticamente a cada interrupção:
```
void SysTick_Handler(void) {
  msTicks++;
}
```

Ela simplesmente incrementa a variável global `msTicks`, que conta os milissegundos passados.

## Função Delay

O SysTick permite implementar delays precisos:
```
void Delay(uint32_t dlyTicks) {
  uint32_t curTicks;
  curTicks = msTicks;
  while ((msTicks - curTicks) < dlyTicks) { __NOP(); }
}
```

1. Armazena o valor atual de `msTicks`
2. Fica em loop até que a diferença entre o valor atual e o armazenado seja igual ao delay desejado
3. `__NOP()` é uma instrução "no operation" que não faz nada, apenas evita otimizações do compilador

## Resumo

No contexto deste programa, o SysTick está sendo usado para:

1. Manter uma contagem precisa do tempo em milissegundos
2. Permitir a criação de delays de 200ms para piscar os LEDs
3. Fornecer uma base de tempo para o sistema

É uma forma eficiente e de baixo [[overhead]] de medir o tempo em sistemas embarcados.