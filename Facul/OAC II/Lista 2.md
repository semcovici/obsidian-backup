![[Lista2.pdf]]


## Questão 1
![[Pasted image 20241006171229.png]]

### A
![[Pasted image 20241006171248.png]]

**A sequência de instruções é a seguinte:**

1. **add $t4, $zero, 2**
2. **add $t1, $t2, $t3**
3. **lw $t3, 0x100($t1)**
4. **sw $t3, 0x200($t1)**
5. **sub $t4, $t4, 2**
6. **add $t3, $t3, 0x100**

### B
![[Pasted image 20241006171302.png]]

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

### B
![[Pasted image 20241006171434.png]]

### C
![[Pasted image 20241006171444.png]]

### D
![[Pasted image 20241006171500.png]]
### E
![[Pasted image 20241006171511.png]]
## Questão 4
![[Pasted image 20241006171521.png]]

### A
![[Pasted image 20241006171559.png]]
### B
![[Pasted image 20241006171607.png]]

### C
![[Pasted image 20241006171615.png]]

### D
![[Pasted image 20241006171622.png]]


### E
![[Pasted image 20241006171630.png]]

### F
![[Pasted image 20241006171639.png]]
