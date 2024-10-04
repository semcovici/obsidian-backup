
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






![[Lista1_2024.pdf]]