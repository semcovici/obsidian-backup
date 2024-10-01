
## Questão 1

![[Pasted image 20240930195539.png]]

> [!NOTE] Palavra
>Em termos simples, em computação, uma **palavra** é um grupo de bits que um computador processa como uma unidade. O tamanho de uma palavra varia dependendo do tipo de computador. A palavra geralmente tem o mesmo tamanho que o processador do computador pode manipular de uma vez só.
>
> No contexto do MIPS e de muitos computadores modernos, uma palavra é composta por **32 bits**. Isso significa que uma "palavra" é um conjunto de 32 zeros e uns (como `10101010...` com 32 dígitos), e o computador trata isso como um único pedaço de informação.
> Por exemplo:
> -  Se você tem um processador de **32 bits**, uma palavra tem **32 bits** (ou 4 bytes, já que 1 byte = 8 bits).
> - Se o processador for de **64 bits**, então a palavra tem **64 bits**.


> [!NOTE] registrador $0
> O registrador $0 ou $zero sempre armazena a constante 0, o que pode ser bastante útil para algumas aplicações

```python fold title:analysis_q1.asm
addi $t1, $0, $0 # adiciona 0 + 0 e armazena em armazena em $t1, ou seja, atribui 0 a $t1
LOOP lw, $s1, 0($s0)



```

```c fold title:resposta_q1.c

// declaracao de variaveis
int i; // $t1
int result; // $s2 
int *MemArrray; // $s0

i = 0// addi $t1, $0, $0






```





![[Lista1_2024.pdf]]