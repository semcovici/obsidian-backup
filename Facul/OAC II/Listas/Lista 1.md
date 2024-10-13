![[Lista1_2024.pdf]]
## Questão 1
![[Pasted image 20240930195539.png]]
```python fold title:analysis_q1.asm
addi $t1, $0, $0 # adiciona 0 + 0 e armazena em armazena em $t1, ou seja, atribui 0 a $t1
LOOP: lw, $s1, 0($s0) # carrega o valor no endereço em $s0 
add $s2, $s2, $s1 # adiciona o valor em $s1 em $s2
addi $s0, $s0, 4 # adiciona 4 no endereço armazenado em $s0, ou seja, pula para o endereço do próximo elemento do array de inteiros, já que inteiros ocupam 32 bits = 4 bytes
addi $t1, $t1, 1 # adiciona 1 em $t1
slti $t2, $t1, 100 # verifica se o valor em $t1 é menor que 100. Caso seja, armazena 1 em $t2, caso contrário $t2 terá 0.
bne $t2, $s0, LOOP # verifica se $t2 não tem o mesmo valor de $s0, que é 0. Caso não seja igual (branch not equal), volta para LOOP
```

```c fold title:resposta_q1.c
// declaracao de variaveis
int i; // $t1
int result; // $s2 
int * MemArrray_ptr = MemArray; // $s0 - assumindo MemArray como inicializado

i = 0// addi $t1, $0, $0

while(i < 100){

	int aux = *MemArray_ptr;// aux armazena o valor contido no endereco apontado por MemArray_ptr (ponteiros apontam para o tamanho inteiro do dado, entao ao incrementar passamos para o proximo inteiro na memoria, que, no caso de um array, é o proximo elemento do array)
	MemArray_ptr ++; // move ponteiro do array para o proximo endereco
	i ++;
}
```


> [!NOTE] Palavra
>Em termos simples, em computação, uma **palavra** é um grupo de bits que um computador processa como uma unidade. O tamanho de uma palavra varia dependendo do tipo de computador. A palavra geralmente tem o mesmo tamanho que o processador do computador pode manipular de uma vez só.
>
> No contexto do MIPS e de muitos computadores modernos, uma palavra é composta por **32 bits**. Isso significa que uma "palavra" é um conjunto de 32 zeros e uns (como `10101010...` com 32 dígitos), e o computador trata isso como um único pedaço de informação.
> Por exemplo:
> -  Se você tem um processador de **32 bits**, uma palavra tem **32 bits** (ou 4 bytes, já que 1 byte = 8 bits).
> - Se o processador for de **64 bits**, então a palavra tem **64 bits**.


> [!NOTE] registrador $0
> O registrador $0 ou $zero sempre armazena a constante 0, o que pode ser bastante útil para algumas aplicações



## Questão 2

![[Pasted image 20241002005206.png]]


```
LOOP:   slt $t2, $0, $t1 
        beq $t2, $0, DONE
        subi $t1, $t1, 1
        addi $s2, $s2, 2
        j LOOP
DONE:
```
### A
![[Pasted image 20241002005234.png]]
Assumindo que $t1 e $s2 são possuem, inicialmente, o valor 0.



Primeiramente, no comando `slt $t2, $0, $t1`, é setado o valor de $t2 como 0, já que $t1 não possui um valor menor que $0, pois 0 não é menor que 0. 

Após isso, em `beq $t2, $0, DONE`, como $t2 possui o valor 0, ou seja, o valor de $t2 é igual ao valor de $0 , o programa "pula" parar DONE.

Como não há código após DONE, o programa finaliza.
### B
![[Pasted image 20241002005259.png]]

```
LOOP:   slt $t2, $0, $t1 
        beq $t2, $0, DONE
        subi $t1, $t1, 1
        addi $s2, $s2, 2
        j LOOP
DONE:
```

```c fold resolucao_q2_b.c
int A; //$s1
int B; //$s2
int i; //$t1
int temp; //$t2


while(i < 0){
	i --;
	B += 2;
}
```


## Questão 3
![[Pasted image 20241002011529.png]]

```c
for (i = 0; i < a; i++) 
    for (j = 0; j < b; j++)
        D[4 * j] = i + j;

```

a <- $s0 
b <- $s1
i <- $t0
j <- $t1
\*vetor_d <- $s2

``` assembly
    li $t0, 0           # i = 0
loop_i:
    bge $t0, $s0, end_i # Se i >= a, fim do loop externo

    li $t1, 0           # j = 0
loop_j:
    bge $t1, $s1, end_j # Se j >= b, fim do loop interno

    # Calcular o endereço de D[4 * j]
    sll $t2, $t1, 2     # t2 = j * 4

    # Carregar o endereço base de D
    add $t3, $s2, $t2   # t3 = endereço de D[j]

    # Calcular i + j e armazenar no endereço D[4 * j]
    add $t4, $t0, $t1   # t4 = i + j
    sw $t4, 0($t3)      # Armazenar i + j em D[j]

    # Incrementar j
    addi $t1, $t1, 1
    j loop_j            # Repetir o loop interno

end_j:
    # Incrementar i
    addi $t0, $t0, 1
    j loop_i            # Repetir o loop externo

end_i:
```



## Questão 4
![[Pasted image 20241004235024.png]]
![[Pasted image 20241004235036.png]]


```assembly
.text
main:
    li $v0, 5 # armazena 5 em $v0 (indica que no syscall tem que esperar o input de um inteiro)
    syscall # pede o input de um inteiro
    move $t0, $v0 # move o inteiro inputado para $t0
    li $v0, 5 # armazena 5 em $v0 (indica que no syscall tem que esperar o input de um inteiro)
    syscall # pede o input de um inteiro
    move $t1, $v0 # move o inteiro inputado para $t1
    bgt $t0, $t1, t0_bigger # se o inteiro digitado primeiro pelo usuário for maior que o segundo, pula pra t0_bigger
    move $t2, $t1 # move o valor de $t1 para $t2
    b endif # pula incondicionalmente para endif
t0_bigger:
    move $t2, $t0 # move o valor de $t0 para $t2
endif:
    move $a0, $t2 # move o maior número para $a0 (o valor em $a0 vai ser impresso em syscall)
    li $v0, 1 # armazena 1 em $v0 (indica que o syscall deve imprimir um inteiro)
    syscall # imprime o inteiro em $a0
    li $v0, 10 $armazena 10 em $v0 (indica que o syscall deve encerrar o programa)
    syscall # encerra o programa

```

O código pede 2 inputs do usuário, imprime o maior dentre os dois inputs e encerra o programa.


```
.text
    .globl main
main:
    li $a0, 5              # Carrega 5 em $a0 (argumento para a função)
    jal Funcao             # Chama a função Funcao
    move $s0, $v0          # Armazena o valor de retorno em $s0
    li $v0, 10             # Código da syscall para encerrar o programa
    syscall                # Executa syscall para encerrar o programa

Funcao:
    sub $sp, $sp, 4        # Reserva espaço na pilha
    sw $ra, 0($sp)         # Salva o endereço de retorno na pilha
    li $t1, 1              # Carrega 1 em $t1
    slti $t0, $a0, 2       # Define $t0 como 1 se $a0 < 2
    beq $t0, $zero, Calcula # Se $a0 >= 2, vai para Calcula
    add $v0, $zero, $zero  # Define retorno $v0 = 0 se $a0 < 2
    beq $a0, $zero, Sai    # Se $a0 == 0, salta para Sai
    add $v0, $t1, $zero    # Se $a0 == 1, define retorno $v0 = 1

Sai:
    lw $ra, 0($sp)         # Restaura $ra da pilha
    add $sp, $sp, 4        # Desaloca espaço da pilha
    jr $ra                 # Retorna à função chamadora

Calcula:
    add $a1, $a0, $zero    # Copia $a0 para $a1
Loop:
    sub $a1, $a1, $t1      # Decrementa $a1
    jal Multiplica         # Chama a sub-rotina Multiplica
    add $a0, $v0, $zero    # Atualiza $a0 com o valor de retorno
    bne $a1, $t1, Loop     # Continua o loop se $a1 != 1
    j Sai                  # Salta para Sai ao terminar o loop

Multiplica:
    mult $a0, $a1          # Multiplica $a0 e $a1
    mflo $v0               # Move o resultado da multiplicação para $v0
    jr $ra                 # Retorna à função chamadora



```

Esse codigo faz um fatorial
## Questão 5

![[Pasted image 20241006023717.png]]


```
.data VET: .word 23, -43, 55, -9, -7, 21, -76, 12, -45, -10 # Vetor com os valores TAM: .word 10 # Tamanho do vetor 

.text .globl main

main:

	la $t0, VET # armazena end base do vetor
	lw $t1, TAM # armazena valor em TAM

	li $t2, 0 # t2 <- i


LOOP: 
	slt $t3, $t2, $t3 # verifica se i < TAM
	beq $t3, $0, FIM:

	sll $t4, $t2, 2 # i * 4 (obtem deslocamento necessario pra chegar no elemento i)

	add $t5, $t0, $t4 # obtem endereco do elemento i
	lw $t6, 0($t5) # obtem valor do elemento i

	move $a0, $t6 # elemento i como argumento da funcao
	jal calc_abs # chama funcao de obter valor absoluto

	sw $v0, 0($t5) # salva valor absoluto no array

	addi $t2, $t2, 1 # i++

	j LOOP




calc_abs:

	slt $t0, $a0, $0 # verifica se o input a0 é negativo
	bne $t0, $0, make_positive # branch se a0 for negativo

	move $v0, $a0 # armazena o valor de a0 no registrador de retorno
	jr $ra


make_positive: 
	sub $v0, $0, $a0 # v0 = -a0
	jr $ra # retorna 


FIM:


```

## Questão 6
![[Pasted image 20241006023730.png]]

```
.data 
	VET: .word 23, 43, 55, 9, 7, 21, 76, 12, 45, 10 # Vetor de inteiros 
	TAM: .word 10 # Tamanho do vetor 
	PAR: .word 0 # Inicializa o contador de pares 
	IMPAR: .word 0 # Inicializa o contador de ímpares 
	
.text 
	.globl main

main:

	la $t0, VET # armazena endereco base de VET
	lw $t1, TAM # armazena valor de TAM

	li $t2, 0 # inicializa contador de par
	li $t3, 0 # inicializa contador de impar


	li $t4, 0 # inicializa i = 0

LOOP:
	slt $t5, $t4, $t1 # verifica se i < TAM
	beq $t5, $0, FIM # termina se i >= TAM

	sll $t6, $t4, 2 # obtem deslocamento necessario para alcancar elemento i
	addi $t7, $t0, $t6 # obtem endereco do elemento i

	lw $t8, 0($t7) # obtem elemento i

	andi $t1, $t0, 1 # Faz a operação AND bit a bit com 1 e armazena o resultado em $t1 
	beq $t1, $zero, is_even # Se $t1 for 0, o número é par (vai para is_even) 
	bne $t1, $zero, is_odd # Se $t1 for diferente de 0, o número é ímpar (vai para is_odd)

is_even:
	addi $t2, $t2, 1 # incrementa contador de par
	j LOOP

is_odd:
	addi $t3, $t3, 1 # incrementa contador de impar
	j LOOP

FIM:

	sw $t2, PAR
	sw $t3, IMPAR

	
	# Finalizar o programa 
	li $v0, 10 # Chamada de sistema para terminar o programa 
	syscall
	



```




## Questão 7
![[Pasted image 20241006023756.png]]

```
Enquanto i < 100
    v[i+1] = v[i] + 1;
    se v[i+1] != 10
        a++;
    fim se;
    b = c * 2 - d;
fim enquanto
```

```
# i <- $s0
# endereço base de v <- $s1
# a <- $s1
# c <- $s2
# d <- $s3

LOOP: slti $t0, $s0, 100
beq $t0, $0, FIM

sll $t1, $s0, 2 # multiplica por 4 i para saber o endereço de v[i]
lw $t2, 0($t1) # le o valor em v[i]

addi $t3, $t2, 1 # obtem v[i] + 1
sw $t3, 4($t1) # v[i + 1] = v[i] + 1 

# if v[i+10] !=10
li $t4, 10 
bne $t3, $t4, increment_a


sll $t5, $s2, 1 # t5 = c*2
sub $t6, $t5, $s3 # b = c*2 - 5

j LOOP

increment_a:
	addi $s1, $s1, i

FIM:
```


```c
int fact(int n)
{
    if (n < 1)
        return 1;
    else
        return ((n + 1) * fact(n - 1));
}
```

```
fact:

	slti $t0, $a0, 1
	beq $t0, $0, return_one

	addi $a0, $a0, -1 # seta argumento de fact
	jal fact # chama fact

	addi $t1, $a0, 1 # t1 = n + 1
	mul $t2, $t1, $v0 # ((n + 1) * fact(n - 1))

	li $v0, $t2 # seta o retorno
	jr $ra # retorna 


return_one:

	li $v0, 1 # seta o retorno
	jr $ra # retorna 
```
##  Questão 8
![[Pasted image 20241004022009.png]]

A arquitetura de Von Neumann é a base das arquiteturas de computadores modernos e foi proposta por John von Neumann em 1945. Ela é chamada assim devido à sua abordagem unificada para tratar dados e instruções em um único espaço de memória.

### Principais características da arquitetura de Von Neumann:
1. **Memória única para dados e instruções**: Em uma máquina Von Neumann, tanto os dados quanto as instruções do programa são armazenados na mesma memória. Isso permite que o processador busque tanto os dados quanto as instruções dessa memória.
   
2. **Processamento sequencial**: A CPU executa as instruções de maneira sequencial, uma de cada vez, conforme armazenadas na memória.

3. **Ciclo de busca e execução**: A CPU segue um ciclo de busca, decodificação e execução, onde:
   - A instrução é buscada da memória.
   - A instrução é decodificada para determinar o que fazer.
   - A instrução é executada.
   
4. **Unidade de controle e ALU (Unidade Lógica e Aritmética)**: A arquitetura separa a Unidade de Controle, que gerencia o fluxo de instruções, e a ALU, que realiza operações lógicas e aritméticas.

5. **Armazenamento de programas**: O conceito de "programa armazenado" é uma característica central, onde o código do programa é armazenado na memória junto com os dados.

### Principal limitação da arquitetura de Von Neumann:
- **Bottleneck de Von Neumann (Gargalo de Von Neumann)**: A maior limitação dessa arquitetura é o "gargalo de Von Neumann", que ocorre porque a CPU e a memória compartilham o mesmo caminho para acessar tanto dados quanto instruções. Isso significa que apenas uma operação de leitura ou gravação pode acontecer por vez, o que limita a velocidade do processamento, pois a CPU pode ficar ociosa enquanto espera a memória fornecer os dados ou instruções necessários.

Essa limitação impacta a eficiência do sistema e tem levado ao desenvolvimento de arquiteturas alternativas, como a arquitetura Harvard, que separa os espaços de memória para dados e instruções, visando minimizar esse gargalo.






