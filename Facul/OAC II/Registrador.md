## O que é um registrador?

Registradores são pequenas áreas de armazenamento de dados temporários diretamente integradas à CPU, usados para armazenar variáveis, endereços de memória ou resultados intermediários. 

### Características principais:
- **Alta velocidade:** Acesso imediato aos dados.
- **Tamanho pequeno:** Normalmente 32 bits ou 64 bits.
- **Função temporária:** Armazenamento durante a execução de instruções.

---

## Registradores no MIPS

### Registradores de Propósito Geral
- **$t0 a $t9:** Registradores temporários, não precisam ser preservados entre operações.
- **$s0 a $s7:** Registradores salvos, preservam valores entre chamadas de funções.
### Registradores Especiais
- **$zero ($0):** Sempre armazena o valor 0. Usado para operações onde um valor constante de zero é necessário.
- **$at:** Registrador temporário reservado para a montagem de instruções (assembler temporary). Usado pelo assembler e não pelo programador diretamente.
- **$v0 e $v1:** Registradores de valores de retorno. Usados para armazenar os resultados de funções.
- **$a0 a $a3:** Registradores de argumentos. Usados para passar parâmetros para funções.

### Registradores de Controle
- **$fp (Frame Pointer):** Usado para apontar para o início do quadro de ativação da função atual na pilha.
- **$sp (Stack Pointer):** Aponta para o topo da pilha, que armazena dados temporários e quadros de ativação.
- **$ra (Return Address):** Armazena o endereço de retorno após a conclusão de uma função.
- **PC (Program Counter):** Armazena o endereço da próxima instrução a ser executada.