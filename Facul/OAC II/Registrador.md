$fp
$sp

$0
$v0
## O que é?

Um registrador é uma pequena área de armazenamento de dados dentro da unidade central de processamento (CPU) de um computador. Ele é usado para armazenar temporariamente dados que estão sendo processados, como valores de variáveis, endereços de memória, resultados intermediários de cálculos, ou instruções.
Características principais dos registradores:

- **Alta velocidade:** Os registradores são extremamente rápidos, muito mais rápidos do que a memória RAM, porque estão diretamente integrados ao processador. Isso permite que a CPU tenha acesso imediato aos dados que estão sendo usados nos cálculos ou operações.
- **Tamanho pequeno:** Embora sejam muito rápidos, os registradores têm um tamanho bastante limitado. Eles geralmente armazenam uma pequena quantidade de dados, como 32 bits (4 bytes) ou 64 bits (8 bytes), dependendo da arquitetura do processador.
- **Função temporária:** Os registradores são usados para armazenamento temporário de dados durante a execução de instruções. Depois que os dados são processados, o conteúdo do registrador pode ser descartado ou substituído por novos dados.

## Tipos de registradores no MIPS

No MIPS (uma arquitetura RISC), existem diferentes tipos de registradores, e cada um tem um propósito específico. Alguns exemplos incluem:

- **Registradores de propósito geral:** Esses registradores são usados para armazenar dados temporários ou variáveis durante o processamento. No MIPS, eles são nomeados como $t0 a $t9 (para dados temporários) e $s0 a $s7 (para dados salvos). Por exemplo:
	- **$s0 a $s7:** Registradores usados para armazenar valores que precisam ser preservados entre chamadas de funções.
	- **$t0 a $t9:** Registradores temporários, usados quando não há necessidade de manter o valor após uma operação específica.
- **Registrador de instrução (PC - Program Counter)**: Armazena o endereço da próxima instrução a ser executada.
- **Registrador de retorno:** O registrador $ra (return address) armazena o endereço de retorno de uma sub-rotina (função).



MBR MAR IR IBR PC AC MQ

![[Pasted image 20241003015428.png]]
