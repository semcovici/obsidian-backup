![[lista2_2024.pdf]]


# Questão 1

![[Pasted image 20241202014718.png]]

## Minha resposta

Definições:
**Multicore:**
Multicore refere-se a um único chip que contém vários núcleos de processadores independentes, permitindo que tarefas sejam processadas paralelamente. Isso se relaciona com a definição "múltiplos processadores em um único encapsulamento", pois os núcleos, embora sejam processadores separados, estão integrados em um único chip físico.

**Superpipeline:**
Superpipeline representa uma arquitetura de pipeline com um número maior de estágios, possibilitando que múltiplas instruções sejam processadas em diferentes etapas simultaneamente, aumentando a taxa de processamento. Isso se conecta à definição "pipelines com grande número de estágios", que descreve diretamente essa característica.
![[Pasted image 20241202024304.png]]
![[Pasted image 20241202024432.png]]
![[Pasted image 20241202024457.png]]
**Superescalar:**
Superscalar é um design de processador que utiliza múltiplos pipelines em paralelo, permitindo a execução simultânea de várias instruções e explorando o paralelismo em nível de instrução. Assim, está associado à definição "múltiplos pipelines que operam em paralelo", já que essa é a essência da arquitetura superscalar.
![[Pasted image 20241202024616.png]]
![[Pasted image 20241202024719.png]]
![[Pasted image 20241202024742.png]]

**Pipeline dinâmico:**
Pipeline dinâmico é uma técnica em que as instruções são executadas fora de ordem em um pipeline, reorganizando-as para otimizar recursos e reduzir atrasos. Isso está diretamente relacionado à definição "execução de instruções fora de ordem em um pipeline", que descreve exatamente essa abordagem.

**Multiprocessadores:**
Multiprocessadores são sistemas que possuem vários processadores trabalhando juntos e compartilhando um mesmo espaço de memória. Isso se alinha com a definição "múltiplos processadores compartilhando um espaço de endereços", que caracteriza a principal funcionalidade desses sistemas.
## Gabarito

![[Pasted image 20241202020956.png]]
extraido de [[p2_2020_com_gabarito.pdf]]
# Questão 2

![[Pasted image 20241202014732.png]]

## Conceitos

As dependências em **pipeline de execução** (como em MIPS) surgem devido à necessidade de organizar a leitura e escrita em registradores ou memória, especialmente em arquiteturas que tentam executar instruções em paralelo. Vamos detalhar cada tipo de dependência:

 **1. RAW (Read After Write) – Dependência Verdadeira**
 - **Definição:** Ocorre quando uma instrução tenta **ler um valor** que foi ou será **escrito por uma instrução anterior**.
 - A instrução que **lê** o dado depende do resultado da instrução que **escreve** o dado.
 - **Condições para existir:**
    1. Um registrador ou posição de memória deve ser **escrito por uma instrução anterior**
    2. Esse mesmo registrador ou memória deve ser **lido por uma instrução posterior**.
- **Exemplo:**
    ```mips
    I1: ADD F1, F2, F3  # Escreve F1 (F1 = F2 + F3)
    I2: SUB F4, F1, F5  # Lê F1 (F4 = F1 - F5)
    ```
    
    - **RAW entre I1 e I2**: I2 tenta ler `F1` que foi escrito em I1.
- **Por que é importante?** Se I2 tentar executar antes de I1 ter terminado, pode ocorrer um **hazard** (inconsistência no dado).

 **2. WAR (Write After Read) – Dependência Antiga**
- **Definição:** Ocorre quando uma instrução tenta **escrever um valor** em um registrador que será ou já foi **lido por uma instrução anterior**.
- A instrução que **escreve** pode sobrescrever o valor antes que ele seja **lido**.
- **Condições para existir:**
    1. Um registrador ou memória deve ser **lido por uma instrução anterior**.
    2. Esse mesmo registrador ou memória deve ser **escrito por uma instrução posterior**.
- **Exemplo:**
    
    ```mips
    I1: MUL F1, F2, F3  # Lê F2 e F3
    I2: ADD F2, F4, F5  # Escreve F2
    ```
    
    - **WAR entre I1 e I2**: I2 tenta escrever em `F2`, mas I1 precisa ler o valor original de `F2`.
- **Por que é importante?** Se I2 for executada antes de I1 terminar a leitura, pode sobrescrever o valor de `F2` e causar um erro.
**3. WAW (Write After Write) – Dependência de Saída**
- **Definição:** Ocorre quando duas instruções tentam **escrever no mesmo registrador**.
- A instrução posterior deve sobrescrever o valor gerado pela instrução anterior.
- **Condições para existir:**
    1. Um registrador ou memória deve ser **escrito por uma instrução anterior**.
    2. Esse mesmo registrador ou memória deve ser **escrito novamente por uma instrução posterior**.
- **Exemplo:**
    
    ```mips
    I1: ADD F1, F2, F3  # Escreve F1
    I2: MUL F1, F4, F5  # Também escreve F1
    ```
    
    - **WAW entre I1 e I2**: Ambas escrevem no registrador `F1`.
- **Por que é importante?** Se I2 for executada antes de I1 terminar, o valor correto de I1 nunca será salvo no registrador.
    

---

### **4. RAR (Read After Read) – Não é um Hazard**

- **Definição:** Ocorre quando duas instruções **leem o mesmo registrador**. Isso não causa dependência ou hazards, já que nenhuma das instruções modifica o valor.
    
- **Exemplo:**
    
    ```mips
    I1: ADD F3, F1, F2  # Lê F1 e F2
    I2: MUL F4, F1, F2  # Também lê F1 e F2
    ```
    
    - **RAR entre I1 e I2**: Ambas leem `F1` e `F2`, mas não modificam seus valores.
- **Por que não é um problema?** A leitura é inofensiva, desde que nenhum valor seja alterado.
    

---

### **Resumo das Condições:**

|**Dependência**|**Descrição**|**Condição Principal**|
|---|---|---|
|**RAW**|Uma leitura depois de uma escrita|Instrução lê um dado que outra vai escrever|
|**WAR**|Uma escrita depois de uma leitura|Instrução escreve um dado que outra lê|
|**WAW**|Duas escritas no mesmo registrador|Ambas escrevem no mesmo registrador/memória|
|**RAR**|Duas leituras do mesmo registrador (inofensivo)|Apenas leem, sem escrita|

---

### **Como identificar dependências?**

1. **Analise as operações de cada instrução:**
    
    - Quais registradores/memória são **escritos** (destinos).
    - Quais registradores/memória são **lidos** (fontes).
2. **Compare com as instruções anteriores ou posteriores:**
    
    - Para **RAW**: A instrução atual precisa de um valor escrito por uma anterior.
    - Para **WAR**: A instrução atual sobrescreve um registrador que será lido por uma anterior.
    - Para **WAW**: A instrução atual sobrescreve um registrador que já foi sobrescrito.
3. **Ordem de execução importa:**
    
    - Dependências só ocorrem se as instruções tiverem impacto na ordem de execução.

Se precisar de mais exemplos ou mais explicações, é só avisar!

## Minha Resolução

Não tem






## Gabarito
![[Pasted image 20241202021513.png]]

extraído de [[p2_2020_com_gabarito.pdf]]



# Questão 3
![[Pasted image 20241202014751.png]]


## Gabarito

![[Pasted image 20241202021543.png]]
extraído de [[p2_2020_com_gabarito.pdf]]

# Questão 4
![[Pasted image 20241202014811.png]]

## a)
![[Pasted image 20241202014832.png]]

### Gabarito

![[Pasted image 20241202021621.png]]
extraído de [[p2_2020_com_gabarito.pdf]]
## b)
![[Pasted image 20241202014844.png]]

### Gabarito
![[Pasted image 20241202021632.png]]
extraído de [[p2_2020_com_gabarito.pdf]]
# Questão 5

![[Pasted image 20241202014909.png]]
![[Pasted image 20241202015551.png]]
### Gabarito 
![[Pasted image 20241202021818.png]]
extraído de [[p2_2020_com_gabarito.pdf]]
# Questão 6
![[Pasted image 20241202015616.png]]
![[Pasted image 20241202015630.png]]


### Gabarito

![[Pasted image 20241202021921.png]]

extraído de [[p2_2020_com_gabarito.pdf]]

