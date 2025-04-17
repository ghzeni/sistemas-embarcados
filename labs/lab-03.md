especificação da solução: o que eu quero que a solução faça
- não dizendo como ele está sendo feito, e sim o que recebe e como retorna

"que registradores eu vou usar pra guardar as variaveis desse algoritmo?"

"quantos clocks leva pra processar essas imagens?"
- dica: cortex m4 ja tem dentro dele um contador de clocks: nasce quando ligo e vai contando... DWT.
- ler DWT quando inicia a função, ler DWT quando retorna e subtrair.

- rodar o programa gera 2 informações: histograma e numero de clocks
