## Explicação Rápida

![[Pasted image 20241003023427.png]]



## Explicação Detalhada

### 1. `addi` (Add Immediate)

Adiciona um valor imediato (constante) a um registrador e armazena o resultado em um registrador destino.

**Sintaxe:**

```assembly
addi $dest, $src, immediate
```

**Exemplo:**

```assembly
addi $t0, $t1, 5  # $t0 = $t1 + 5
```

**Em C:**

```c
t0 = t1 + 5;
```

---

### 2. `lw` (Load Word)

Carrega uma palavra (32 bits) da memória para um registrador.

**Sintaxe:**

```assembly
lw $dest, offset($base)
```

**Exemplo:**

```assembly
lw $t0, 4($sp)  # Carrega a palavra do endereço ($sp + 4) para $t0
```

**Em C:**

```c
t0 = *(sp + 1);  // Considerando sp como um ponteiro para int
```

---

### 3. `add` (Add)

Adiciona dois registradores e armazena o resultado em um registrador destino.

**Sintaxe:**

```assembly
add $dest, $src1, $src2
```

**Exemplo:**

```assembly
add $t0, $t1, $t2  # $t0 = $t1 + $t2
```

**Em C:**

```c
t0 = t1 + t2;
```

---

### 4. `slti` (Set on Less Than Immediate)

Define o registrador destino como 1 se o registrador fonte for menor que o valor imediato; caso contrário, define como 0.

**Sintaxe:**

```assembly
slti $dest, $src, immediate
```

**Exemplo:**

```assembly
slti $t0, $t1, 10  # $t0 = ($t1 < 10) ? 1 : 0
```

**Em C:**

```c
t0 = (t1 < 10) ? 1 : 0;
```

---

### 5. `bne` (Branch on Not Equal)

Desvia para uma etiqueta se dois registradores não forem iguais.

**Sintaxe:**

```assembly
bne $src1, $src2, label
```

**Exemplo:**

```assembly
bne $t0, $t1, label  # Se $t0 != $t1, vai para 'label'
```

**Em C:**

```c
if (t0 != t1) {
    goto label;
}
```

---

### 6. `slt` (Set on Less Than)

Define o registrador destino como 1 se o primeiro registrador fonte for menor que o segundo; caso contrário, define como 0.

**Sintaxe:**

```assembly
slt $dest, $src1, $src2
```

**Exemplo:**

```assembly
slt $t0, $t1, $t2  # $t0 = ($t1 < $t2) ? 1 : 0
```

**Em C:**

```c
t0 = (t1 < t2) ? 1 : 0;
```

---

### 7. `beq` (Branch on Equal)

Desvia para uma etiqueta se dois registradores forem iguais.

**Sintaxe:**

```assembly
beq $src1, $src2, label
```

**Exemplo:**

```assembly
beq $t0, $t1, label  # Se $t0 == $t1, vai para 'label'
```

**Em C:**

```c
if (t0 == t1) {
    goto label;
}
```

---

### 8. `subi` (Subtract Immediate)

Subtrai um valor imediato de um registrador e armazena o resultado no registrador destino.

**Sintaxe:**

```assembly
subi $dest, $src, immediate
```

**Nota:** `subi` não é uma instrução MIPS padrão. Em vez disso, usa-se `addi` com um valor negativo.

**Exemplo usando `addi`:**

```assembly
addi $t0, $t1, -5  # $t0 = $t1 - 5
```

**Em C:**

```c
t0 = t1 - 5;
```

---

### 9. `j` (Jump)

Desvia incondicionalmente para uma etiqueta.

**Sintaxe:**

```assembly
j label
```

**Exemplo:**

```assembly
j loop_start  # Vai para 'loop_start'
```

**Em C:**

```c
goto loop_start;
```

---

### 10. `li` (Load Immediate)

Carrega um valor imediato (constante) em um registrador.

**Sintaxe:**

```assembly
li $dest, immediate
```

**Exemplo:**

```assembly
li $t0, 100  # $t0 = 100
```

**Em C:**

```c
t0 = 100;
```

---

### 11. `syscall`

Chama um serviço do sistema (sistema operacional), como entrada/saída.

**Exemplo de imprimir um inteiro:**

```assembly
li $v0, 1      # Código de serviço para imprimir inteiro
li $a0, 5      # Inteiro a ser impresso
syscall        # Chama o serviço
```

**Em C (aproximado):**

```c
printf("%d", 5);
```

---

### 12. `move`

Copia o valor de um registrador para outro.

**Sintaxe:**

```assembly
move $dest, $src
```

**Exemplo:**

```assembly
move $t0, $t1  # $t0 = $t1
```

**Em C:**

```c
t0 = t1;
```

---

### 13. `bgt` (Branch on Greater Than)

Desvia para uma etiqueta se o primeiro registrador for maior que o segundo.

**Nota:** `bgt` não é uma instrução MIPS básica. Pode ser implementada usando `slt` e `bne`.

**Exemplo:**

Para `bgt $t1, $t2, label`, você pode reescrever como:

```assembly
slt $t0, $t2, $t1     # $t0 = ($t2 < $t1)
bne $t0, $zero, label  # Se $t1 > $t2, vai para 'label'
```

**Em C:**

```c
if (t1 > t2) {
    goto label;
}
```

---

### 14. `sub` (Subtract)

Subtrai o segundo registrador fonte do primeiro e armazena o resultado no registrador destino.

**Sintaxe:**

```assembly
sub $dest, $src1, $src2
```

**Exemplo:**

```assembly
sub $t0, $t1, $t2  # $t0 = $t1 - $t2
```

**Em C:**

```c
t0 = t1 - t2;
```

---

### 15. `sw` (Store Word)

Armazena uma palavra (32 bits) de um registrador na memória.

**Sintaxe:**

```assembly
sw $src, offset($base)
```

**Exemplo:**

```assembly
sw $t0, 8($sp)  # Armazena o valor de $t0 no endereço ($sp + 8)
```

**Em C:**

```c
*(sp + 2) = t0;  // Considerando sp como um ponteiro para int
```

---

### 16. `mult` (Multiply)

Multiplica dois registradores; o resultado (64 bits) é armazenado nos registradores especiais `HI` e `LO`.

**Sintaxe:**

```assembly
mult $src1, $src2
```

**Exemplo:**

```assembly
mult $t1, $t2  # HI:LO = $t1 * $t2
```

Para acessar o resultado, você precisa mover o conteúdo de `LO` ou `HI` para um registrador.

---

### 17. `mflo` (Move From LO)

Move o conteúdo do registrador especial `LO` para um registrador.

**Sintaxe:**

```assembly
mflo $dest
```

**Exemplo:**

```assembly
mflo $t0  # $t0 = LO
```

**Uso combinado com `mult`:**

```assembly
mult $t1, $t2
mflo $t0    # $t0 = resultado de $t1 * $t2
```

**Em C:**

```c
t0 = t1 * t2;
```

---

### 18. `jr` (Jump Register)

Salta para o endereço contido em um registrador. Comumente usado para retornar de sub-rotinas.

**Sintaxe:**

```assembly
jr $ra  # Retorna para o endereço em $ra (registrador de retorno)
```

**Exemplo:**

```assembly
jr $ra  # Retorna de uma função
```

**Em C:**

```c
return;  // Em contexto de função
```

---