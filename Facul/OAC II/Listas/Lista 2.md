## Enunciado completo

![[Lista2.pdf]]


## Questão 1
![[Pasted image 20241006171229.png]]

### A
![[Pasted image 20241006171248.png]]
```
addi $t4, $zero, 2
root: 
	add $t1, $t2, $t3
	lw $t3, 0x100($t1)
	sw $t3, 0x200($t1)
	subi $t4, $t4, 2
	beq $t4, $t3, root
	addi $t3, $t3, 0x100
```

|                      | 1   | 2   | 3   | 4                  | 5                               | 6   | 7                | 8                                | 9                     | 10  | 11  | 12  |
| -------------------- | --- | --- | --- | ------------------ | ------------------------------- | --- | ---------------- | -------------------------------- | --------------------- | --- | --- | --- |
| addi $t4, $zero, 2   | BI  | DI  | EX  | MEM                | WB                              |     |                  |                                  |                       |     |     |     |
| add $t1, $t2, $t3    |     | BI  | DI  | EX (Foward t1 -> ) | MEM                             | WB  |                  |                                  |                       |     |     |     |
| lw $t3, 0x100(\$t1)  |     |     | BI  | DI                 | (<-Foward t1) EX(Foward t3 -> ) | MEM | WB               |                                  |                       |     |     |     |
| sw \$t3, 0x200(\$t1) |     |     |     | X                  | BI                              | DI  | (<-Foward t1 )EX | (<-Foward t3) MEM (Foward t3 ->) | WB                    |     |     |     |
| subi $t4, $t4, 2     |     |     |     |                    |                                 | BI  | DI               | EX (Foward t4 ->)                | MEM                   | WB  |     |     |
| beq $t4, $t3, root   |     |     |     |                    |                                 |     | BI               | DI                               | (<-Foward t3 e t4 )EX | MEM | WB  |     |
| addi $t3, $t3, 0x100 |     |     |     |                    |                                 |     |                  | BI                               | DI                    | EX  | MEM | WB  |


### B
![[Pasted image 20241006171302.png]]
```
addi $t4, $zero, 2
root: 
	add $t1, $t2, $t3
	lw $t3, 0x100($t1)
	sw $t3, 0x200($t1)
	subi $t4, $t4, 2
	beq $t4, $t3, root
	addi $t3, $t3, 0x100
```

Estava fazendo o fowarding do valor que será atribuído à t1 em `add $t1, $t2, $t3` para o valor de entrada para a ALU `lw $t3, 0x100(\$t1)`, onde a partir do valor de t1 é calculado o endereço que será feito o load.
## Questão 2
![[Pasted image 20241006171316.png]]

i <- $t1
resultado <- $s2
*arranjo <- $s0

```
addi $t1, $0, 0 # inicializa i com 0
LOOP: 
	# resultado = resultado + arranjo[0]
	lw $s1, 0($s0) # carrega primeiro valor do arranjo
	add $s2, $s2, $s1 # resultado é incrementado com o valor do primeiro elemento do arranjo
	
	addi $s0, $s0, 4 # desloca o ponteiro do arranjo em 4 bytes, fazendo com que o primeiro elemento seja um novo elemento
	
	addi $t1, $t1, 1 # i++

	# reinicia o LOOP caso i < 100
	slti $t2, $t1, 100 # seta 1 em t2, caso i < 100
	bne $t2, $0, LOOP # se t2 for diferente de 0, volta para o inicio do LOOP
	
```

```c
# considerando que i, resultado e arranjo estão inicializados
i = 0 // iniciliza i
while (i< 100){
	resultado = resultado + arranjo[i]
	i ++;
}


```

## Questão 3
![[Pasted image 20241006171328.png]]

### A
![[Pasted image 20241006171427.png]]

```
lw $1, 40($6) #i1
add $2, $3, $1 #i2
add $1, $6, $4 #i3
sw $2, 20($4) #i4
and $1, $1, $4 #i5
```

Em `i2` é feita uma adição sobre um o registrador $1, que possui o seu valor atualizado em `i1`. Pelo valor de $1 ser atribuído por uma leitura na memória de dados, mesmo que haja forwarding, precisaria da adição de uma bolha. 

Existe também um conflito entre `i4` e `i2`.

O outro conflito seria entre `i5` e `i3`, que é solucionado com o forwarding.
### B
![[Pasted image 20241006171434.png]]
```
lw $1, 40($6) #i1
nop
nop
add $2, $3, $1 #i2
add $1, $6, $4 #i3
nop
sw $2, 20($4) #i4
nop
and $1, $1, $4 #i5
```
### C
![[Pasted image 20241006171444.png]]
```
lw $1, 40($6) #i1
nop
add $1, $6, $4 #i3
add $2, $3, $1 #i2
sw $2, 20($4) #i4
and $1, $1, $4 #i5
```
### D
![[Pasted image 20241006171500.png]]
Sim, pode ser resolvido. Dessa forma, as instruções irão acessar a memória em momentos diferentes.
### E
![[Pasted image 20241006171511.png]]
Adicionando um bolha entre as duas instruções, caso haja fowarding no pipeline. Em caso contrário, adicionar duas bolhas.
## Questão 4
![[Pasted image 20241006171521.png]]

### A
![[Pasted image 20241006171559.png]]

```
add r5, r2, r1
lw r3, 4(r5)
lw r2, 0(r2)
or r3, r5, r3
sw r3, 0(r5)
```

Sem fowarding, teriamos que ter uma execução assim:

|                | 1   | 2   | 3   | 4   | 5                                                               | 6                   | 7                             | 8                             | 9   | 10  | 11                  | 12  | 13  | 14  |
| -------------- | --- | --- | --- | --- | --------------------------------------------------------------- | ------------------- | ----------------------------- | ----------------------------- | --- | --- | ------------------- | --- | --- | --- |
| add r5, r2, r1 | BI  | DI  | EX  | MEM | ==WB (salvou r5 na memoria - primeira parte do ciclo)==<br><br> |                     |                               |                               |     |     |                     |     |     |     |
| nop            |     | -   | -   | -   | -                                                               | -                   |                               |                               |     |     |                     |     |     |     |
| nop            |     |     | -   | -   | -                                                               | -                   | -                             |                               |     |     |                     |     |     |     |
| lw r3, 4(r5)   |     |     |     | BI  | ==DI (lê r5 da memória - segunda parte do ciclo)==              | EX (calcula r5 + 4) | MEM (busca r5 + 4 na memoria) | ==WB==<br>==(escreve em r3)== |     |     |                     |     |     |     |
| lw r2, 0(r2)   |     |     |     |     | BI                                                              | DI                  | EX                            | MEM                           | WB  |     |                     |     |     |     |
| nop            |     |     |     |     |                                                                 | -                   | -                             | -                             | -   | -   |                     |     |     |     |
| or r3, r5, r3  |     |     |     |     |                                                                 |                     | BI                            | ==DI (lê r3)==                | EX  | MEM | ==WB (escreve r3)== |     |     |     |
| nop            |     |     |     |     |                                                                 |                     |                               | -                             | -   | -   | -                   | -   |     |     |
| nop            |     |     |     |     |                                                                 |                     |                               |                               | -   | -   | -                   | -   | -   |     |
| sw r3, 0(r5)   |     |     |     |     |                                                                 |                     |                               |                               |     | BI  | ==DI (lê r3)==      | EX  | MEM | WB  |


```
add r5, r2, r1
nop
nop
lw r3, 4(r5)
lw r2, 0(r2)
nop
or r3, r5, r3
nop
nop
sw r3, 0(r5)
```


### B
![[Pasted image 20241006171607.png]]
Original: 
```python
add r5, r2, r1
nop
nop
lw r3, 4(r5)
lw r2, 0(r2)
nop
or r3, r5, r3
nop
nop
sw r3, 0(r5)

```

Não há como rearranjar de forma que diminua o número de nops.
### C
![[Pasted image 20241006171615.png]]

|                | 1   | 2   | 3              | 4            | 5               | 6                      | 7            | 8   | 9   |
| -------------- | --- | --- | -------------- | ------------ | --------------- | ---------------------- | ------------ | --- | --- |
| add r5, r2, r1 | BI  | DI  | EX (Foward ->) | MEM          | WB <br><br>     |                        |              |     |     |
| lw r3, 4(r5)   |     | BI  | DI             | (<-Foward)EX | MEM (Foward ->) | WB                     |              |     |     |
| lw r2, 0(r2)   |     |     | BI             | DI           | EX              | MEM                    | WB           |     |     |
| or r3, r5, r3  |     |     |                | BI           | DI              | (<-Foward)EX(Foward->) | MEM          | WB  |     |
| sw r3, 0(r5)   |     |     |                |              | BI              | DI                     | (<-Foward)EX | MEM | WB  |

Ou seja, não há problema. Sempre o forwarding resolve o problema que poderia dar.
### D


add r4, r3, r1
sw r4, 0(r4)

![[Pasted image 20241011225247.png]]
Baseado na tabela gerada na pergunta anterior:
No ciclo 3, há um forward de EX/MEM para EX. 

No ciclo 4, recebe-se o forward de EX/MEM para EX gerado no ciclo 3.

No ciclo 4, há um forward de MEM/WB para EX
#### Gabarito
![[Pasted image 20241024181544.png]]
### E
![[Pasted image 20241006171630.png]]

### F
![[Pasted image 20241006171639.png]]
