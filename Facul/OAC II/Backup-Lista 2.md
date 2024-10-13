[[Lista2.pdf]]


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

 **Estágios do pipeline:**

O pipeline possui 5 estágios:

1. **BI (Busca de Instrução)**: O estágio onde a instrução é buscada na memória.
2. **DI (Decodificação)**: Onde a instrução é decodificada e os registradores envolvidos são lidos.
3. **EX (Execução)**: Onde as operações aritméticas ou lógicas são executadas.
4. **MEM (Memória)**: Onde acessos à memória (leitura/escrita) ocorrem.
5. **WB (Write-back)**: Onde o resultado é escrito de volta ao registrador.

 Conteúdos iniciais de registradores e memória relevantes:

- $t1 = 0x100
- $t2 = 0x100
- $t3 = 0x100
- $t4 = 0x100

 **Execução:**

| Ciclo | Instrução           | BI  | DI  | EX  | MEM | WB  |
| ----- | ------------------- | --- | --- | --- | --- | --- |
| 1     | add $t4, $zero, 2   | BI  |     |     |     |     |
| 2     | add $t1, $t2, $t3   | BI  | DI  |     |     |     |
| 3     | lw $t3, 0x100($t1)  | BI  | DI  | EX  |     |     |
| 4     | sw $t3, 0x200($t1)  | BI  | DI  | EX  | MEM |     |
| 5     | sub $t4, $t4, 2     | BI  | DI  | EX  | MEM | WB  |
| 6     | add $t3, $t3, 0x100 | BI  | DI  | EX  | MEM | WB  |
### B
![[Pasted image 20241006171302.png]]
No **quinto ciclo**, a instrução **sub $t4, $t4, 2** está no estágio **EX** (Execução). No entanto, a unidade de adiantamento precisa garantir que o valor atualizado de $t4, que foi calculado na primeira instrução **add $t4, $zero, 2**, esteja disponível. Nesse momento, a unidade de adiantamento utiliza o valor atualizado de $t4 do estágio **WB** da primeira instrução e o encaminha diretamente para o estágio **EX** da instrução **sub**.

Assim, o forwarding (adiantamento) está enviando o valor correto de $t4, evitando que o pipeline tenha que inserir bolhas para esperar que o valor esteja disponível após o write-back.

**Comparações que podem estar sendo feitas**:

- A unidade de adiantamento verifica se a instrução **sub $t4, $t4, 2** depende de valores que ainda não foram escritos em seus registradores. Nesse caso, detecta a dependência de $t4, que está sendo atualizado pela primeira instrução.

Essa é a função principal do forwarding no quinto ciclo: garantir que o valor de $t4 atualizado esteja disponível para a instrução **sub**.

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
Na sequência de instruções dada, podemos identificar os seguintes tipos de conflitos:

- **1ª instrução: lw $1, 40 ($6)**  
    Essa instrução carrega o valor da memória para o registrador $1.
    
- **2ª instrução: add $2, $3, $1**  
    Essa instrução depende do resultado da 1ª, pois precisa do valor de $1, que está sendo carregado da memória. Esse é um conflito do tipo **RAW (Read After Write)**. Se houver adiantamento (forwarding), esse conflito pode ser resolvido sem a necessidade de bolhas.
    
- **3ª instrução: add $1, $6, $4**  
    Essa instrução depende do valor anterior de $1, mas como o valor de $1 foi atualizado pela primeira instrução, também há um **RAW**. Contudo, esse conflito não pode ser resolvido com adiantamento imediato, já que o resultado de $1 só estará disponível após o término da 1ª instrução, e o pipeline precisará inserir bolhas.
    
- **4ª instrução: sw $2, 20($4)**  
    Essa instrução não depende diretamente de outras, mas há um risco de conflito estrutural, se o pipeline não puder fazer leitura e escrita na memória ao mesmo tempo.
    
- **5ª instrução: add $1, $1, $4**  
    Essa depende da 3ª instrução, que também escreve no registrador $1. Outro **RAW** acontece aqui, necessitando de bolhas ou adiantamento.
    

**Resumo dos conflitos e solução com adiantamento:**

- A 2ª instrução (add $2, $3, $1) depende da 1ª, mas o adiantamento pode resolver esse conflito.
- A 3ª instrução (add $1, $6, $4) causará uma bolha, pois depende do valor carregado na 1ª instrução, e o valor de $1 ainda não está disponível.
- A 5ª instrução (add $1, $1, $4) depende da 3ª e pode causar bolhas, pois há um **RAW**.

### B
![[Pasted image 20241006171434.png]]
Se não houver adiantamento ou detecção automática de conflitos, precisamos inserir _NOPs_ manualmente para evitar os conflitos de dependência. A sequência de instruções com _NOPs_ seria a seguinte:

```assembly
lw $1, 40 ($6)
nop
nop
add $2, $3, $1
add $1, $6, $4
nop
add $1, $1, $4
sw $2, 20($4)
```
**Explicação:**

- Após a instrução `lw`, inserimos dois NOPs antes da instrução `add $2, $3, $1`, pois o valor de $1 não estará disponível até que a instrução `lw` termine de carregar o valor.
- Após a instrução `add $1, $6, $4`, inserimos um NOP antes da instrução `add $1, $1, $4` para garantir que o novo valor de $1 esteja pronto.
### C
![[Pasted image 20241006171444.png]]

Agora, podemos tentar rearranjar as instruções para minimizar a quantidade de NOPs. Por exemplo, podemos alterar a ordem das instruções para evitar a necessidade de NOPs, aproveitando o registrador temporário R7.

Uma possível rearranjo seria:
```
lw $1, 40 ($6)
add $1, $6, $4
sw $2, 20($4)  # Instrução sem dependência direta
add $2, $3, $1
add $1, $1, $4
```
Neste caso:

- Movemos a instrução `sw $2, 20($4)` para logo após o `lw`, já que não há dependência direta entre essas instruções, permitindo que o pipeline prossiga sem interrupção.
- Eliminamos a necessidade de NOPs ao rearranjar as instruções, mantendo a execução correta do código.

### D
![[Pasted image 20241006171500.png]]
O conflito estrutural ocorre quando duas instruções tentam acessar a memória ao mesmo tempo. No caso da sequência de instruções fornecida, isso poderia acontecer se o pipeline tentasse executar `lw` e `sw` simultaneamente. Para resolver esse conflito, uma abordagem seria inserir um _NOP_ para separar as operações de leitura e escrita na memória:

```
lw $1, 40 ($6)
nop
sw $2, 20($4)
```

### E
![[Pasted image 20241006171511.png]]
A sequência de instruções fornecida é:
```
load $1, (10) $2
add $2, $1, $3
```
Aqui, temos um conflito RAW, já que a instrução `add` depende do resultado do `load` (valor de $1). Para evitar um conflito, a unidade de detecção de conflitos deve inserir um _NOP_ ou bolha entre essas duas instruções para garantir que o valor carregado para $1 esteja disponível antes de ser utilizado na operação `add`.

**Procedimento**:

- A unidade de detecção de conflitos pode inserir uma bolha no pipeline para atrasar a execução da instrução `add $2, $1, $3` até que o valor de $1 esteja disponível.
## Questão 4
![[Pasted image 20241006171521.png]]

### A
![[Pasted image 20241006171559.png]]
A sequência de instruções é a seguinte:

1. `add r5, r2, r1`
2. `lw r3, 4(r5)`
3. `lw r2, 0(r2)`
4. `or r3, r5, r3`
5. `sw r3, 0(r5)`

Vamos identificar os **conflitos**:

- A instrução 2 depende da instrução 1, pois `r5` é usado como endereço de memória na segunda instrução, logo, temos um **RAW (Read After Write)** entre a primeira e a segunda instrução.
- A instrução 4 também depende da instrução 1, pois `r5` está sendo usado novamente.
- A instrução 5 depende da instrução 4, pois `r3` é atualizado na instrução 4 e é usado na instrução 5.

**Inserindo NOPs**: Sem o uso de forwarding ou de detecção de conflito, será necessário inserir _NOPs_ para garantir que os dados necessários estejam prontos. A sequência de instruções com NOPs seria assim:
```
add r5, r2, r1
nop
nop
lw r3, 4(r5)
lw r2, 0(r2)
nop
or r3, r5, r3
sw r3, 0(r5)

```
**Explicação**:

- Após a instrução `add r5, r2, r1`, inserimos dois NOPs antes da instrução `lw r3, 4(r5)` para garantir que o valor de `r5` esteja pronto.
- Após a instrução `lw r2, 0(r2)`, inserimos um NOP antes da instrução `or r3, r5, r3` para garantir que os valores de `r3` e `r5` estejam prontos.

### B
![[Pasted image 20241006171607.png]]
Para minimizar os NOPs, podemos tentar rearranjar as instruções e usar o registrador temporário `r7` para armazenar temporariamente alguns valores. Aqui está uma possível reordenação das instruções:

```
add r5, r2, r1
lw r7, 0(r2)      # Usa r7 para evitar conflitos com r2
lw r3, 4(r5)
nop
or r3, r5, r3
sw r3, 0(r5)
```

**Explicação**:

- A instrução `lw r7, 0(r2)` foi movida antes do `lw r3, 4(r5)` para evitar o conflito entre `r2` e `r5`.
- Inserimos apenas um NOP antes da instrução `or r3, r5, r3`, minimizando a quantidade de NOPs necessária.
### C
![[Pasted image 20241006171615.png]]
Se houver forwarding, mas **não houver detecção de conflitos**, o processador ainda poderá executar algumas instruções corretamente, mas poderá haver casos em que ele não identificará dependências corretamente e ocorrerão erros na execução, especialmente nos casos em que o dado não pode ser adiantado em tempo suficiente. Isso pode causar resultados incorretos, pois o processador tentará usar valores que ainda não estão prontos.

Por exemplo:

- Na ausência de detecção de conflitos, o processador pode não identificar a dependência entre a instrução 1 (`add r5, r2, r1`) e a instrução 2 (`lw r3, 4(r5)`), levando à leitura de um valor incorreto de `r5` no estágio EX de `lw`.
### D
![[Pasted image 20241006171622.png]]

O pipeline funciona com adiantamento para evitar que as instruções esperem até o final da escrita (WB). O adiantamento pega os valores dos estágios de execução anteriores (EX/MEM ou MEM/WB) e os usa no estágio de execução.

Vamos descrever o que ocorre nos primeiros 5 ciclos com adiantamento:

- **Ciclo 1 (add r5, r2, r1)**:
    
    - No estágio EX, o valor de `r5` é calculado como a soma de `r2` e `r1`.
- **Ciclo 2 (lw r3, 4(r5))**:
    
    - O valor de `r5`, gerado na instrução anterior, precisa ser adiantado para o estágio EX da instrução `lw` através da unidade de forwarding.
- **Ciclo 3 (lw r2, 0(r2))**:
    
    - Não há conflito direto aqui, então o valor de `r2` pode ser lido diretamente da memória.
- **Ciclo 4 (or r3, r5, r3)**:
    
    - O valor de `r3` e `r5` precisa ser adiantado da instrução anterior e da primeira instrução, respectivamente, para o estágio EX.
- **Ciclo 5 (sw r3, 0(r5))**:
    
    - O valor de `r3` é adiantado do estágio EX da instrução `or` para ser usado no estágio EX do `sw`.
### E
![[Pasted image 20241006171630.png]]
Na ausência de forwarding, precisaríamos de uma **unidade de detecção de conflitos** que inserisse bolhas automaticamente quando identificasse dependências de dados entre instruções. Os novos sinais seriam:

1. **Sinais de detecção de dependências** entre instruções consecutivas, para identificar quando o valor de um registrador de destino (rd) de uma instrução está sendo usado como operando (rs ou rt) por uma instrução subsequente.
2. **Sinal de bolha (stall)**: Quando uma dependência é detectada, a unidade de detecção precisa ativar um sinal para inserir uma bolha e atrasar a instrução dependente.

### F
![[Pasted image 20241006171639.png]]

Nos primeiros 5 ciclos, a unidade de detecção de conflitos precisa monitorar os registradores envolvidos em cada instrução para determinar se há dependências que exigem bolhas. Aqui está uma possível atribuição de sinais:

- **Ciclo 1**: Nenhuma bolha necessária, pois estamos apenas executando a primeira instrução (`add`).
- **Ciclo 2**: Detecção de dependência entre a instrução 1 (`add r5, r2, r1`) e a instrução 2 (`lw r3, 4(r5)`), inserindo uma bolha se não houver forwarding.
- **Ciclo 3**: Não há dependências diretas, então nenhum sinal de bolha é ativado.
- **Ciclo 4**: Detecção de dependência entre a instrução 2 (`lw r3, 4(r5)`) e a instrução 4 (`or r3, r5, r3`), inserindo uma bolha se não houver forwarding.
- **Ciclo 5**: Detecção de dependência entre a instrução 4 (`or r3, r5, r3`) e a instrução 5 (`sw r3, 0(r5)`), inserindo bolhas se necessário.

Essa seria a função da unidade de detecção de conflitos sem o uso de forwarding.

Se precisar de mais explicações ou ajuda em algum ponto específico, é só avisar!