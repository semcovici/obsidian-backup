

![[files/Aula3_SIN5013_2024 1.pdf]]


## Definição
É uma abstração que nos permite focar no que ocorre com $f(n)$ quando n cresce indefinidamente.
- Termos de menor ordem não importam 
- constates não importam 
- em $f(n) = 2n^3 + 4000n^2 + 1000n - 47$, nos importa apenas $f(n)=n^3$

## Notações

### Big O 

$$ O(g(n)) = \{ f(n) : \exists c > 0, n_0 > 0 \mid 0 \leq f(n) \leq c \cdot g(n), \forall n \geq n_0 \} $$


Vídeo bom: https://youtu.be/gjw7AaOs9P8?si=cVtBMvJeiIiNGEXo

Seja n um inteiro positivo e sejam $f(n)$ e $g(n)$ funções positivas. Dizemos que $f(n)=O(g(n))$ (ou $f(n)$ é $g(n)$) se existem constantes positivas $c$ e $n_0$ tais que $f(n) \leq c \cdot g(n) \ \forall \ n \geq n_0$. 
![[Pasted image 20241015224000.png]]
Exemplo: 
Dado a função $f(n) = 5tn + 3t$, verifique se $f(n)$ é $O(g(n))$ para:

--- 
**Expressão:** $g(n) = n$

**Desenvolvimento:**
$f(n) = O(n)$ 
$f(n) \leq c \cdot g(n)$
$5tn + 3t \leq c \cdot n$
$5t + \frac{3t}{n} \leq c$
Dado que n cresce indefinidamente, o termo $\frac{3t}{n}$ tende a 0, assim podemos desprezá-lo. Tendo assim:
$5t \leq c$
Dado que c é uma constante positiva que pode assumir um valor qualquer, podemos atribuir um valor a ela como $6t$ que torna a expressão verdadeira, já que $5t \leq 6t$. Dessa forma, podemos dizer que:
$f(n)$ é $O(g(n))$

---
**Expressão:** $g(n) = n^2$

**Desenvolvimento:**
$f(n) \leq c \cdot g(n)$
$5tn + 3t \leq c \cdot n^2$
$\frac{5t}{n} + \frac{3t}{n^2} \leq c$
Dado que n cresce indefinidamente, os termos $\frac{5t}{n}$ e $\frac{3t}{n^2}$ tendem a 0, assim podemos desprezá-los. Tendo assim:
$0 \leq c$
Dado que c é uma constante positiva que pode assumir um valor qualquer, necessariamente essa afirmação é verdadeira. Dessa forma, podemos dizer que:
$f(n)$ é $O(g(n))$

---

**Desenvolvimento:**
$f(n) \leq c \cdot g(n)$
$5tn + 3t \leq c \cdot n^2$
$\frac{5t}{n} + \frac{3t}{n^2} \leq c$
Dado que n cresce indefinidamente, os termos $\frac{5t}{n}$ e $\frac{3t}{n^2}$ tendem a 0, assim podemos desprezá-los. Tendo assim:
$0 \leq c$
Dado que c é uma constante positiva que pode assumir um valor qualquer, necessariamente essa afirmação é verdadeira. Dessa forma, podemos dizer que:

$f(n)$ é $O(g(n))$

> Essa afirmação também se expande para $g(n) = n^k \ \forall \ k \geq 1$.

--- 
**Expressão:** $g(n) = \sqrt{n}$

**Desenvolvimento:**
$f(n) \leq c \cdot g(n)$
$5tn + 3t \leq c \cdot \sqrt{n}$
O termo $5tn + 3t$ cresce linearmente, enquanto o termo $\sqrt{n}$ irá crescer mais lentamente já que, necessariamente, a raiz de $n$ ($\sqrt{n}$) cresce mais lentamente que $n$. Dessa forma, podemos dizer que:

$f(n)$ não é $O(g(n))$

> Essa afirmação também se expande para $g(n) = n^k \ \forall \ k < 1$.
---
### Omega 

$$ \Omega(g(n)) = \{ f(n) : \exists c > 0, n_0 > 0 \mid 0 \leq c \cdot g(n) \leq f(n), \forall n \geq n_0 \} $$


Video bom: https://www.youtube.com/watch?v=t0MhdT7Z-_U

Seja $n$ um inteiro positivo e sejam $f(n)$ e $g(n)$ funções positivas. Dizemos que $f(n) = \Omega(g(n))$ (ou $f(n)$ é $\Omega(g(n))$) se existem constantes positivas $c$ e $n_0$ tais que $f(n) \geq c \cdot g(n) \ \forall \ n \geq n_0$

![[Pasted image 20241016004817.png]]

Exemplo: 
Dado a função $f(n) = 5tn + 3t$, verifique se $f(n)$ é $\Omega(g(n))$ para:


--- 
**Expressão:** $g(n) = n$

**Desenvolvimento:**
$f(n) = \Omega(n)$
$5tn + 3t \geq c \cdot n$
$5t + \frac{3t}{n} \geq c$
Dessa forma, temos que o termo $\frac{3t}{n}$ tende a 0, dado a natureza crescente de n. Ou seja, o que nos resta é provar que $5t \geq c$ e essa afirmação é verdadeira dado o fato de que podemos ter c como a constante $4t$, por exemplo.

Dessa forma, podemos dizer que:

$f(n)$ é $\Omega{(g(n))}$


--- 
**Expressão:** $g(n) = n^2$

**Desenvolvimento:**
$f(n) \geq c \cdot g(n)$
$5tn + 3t \geq c \cdot n^2$
$\frac{5t}{n} + \frac{3t}{n^2} \geq c$
Dado que os termos $\frac{5t}{n}$ e $\frac{3t}{n^2}$ tenderão a 0, temos que provar que $0 \geq c$ e, sendo $c$ uma constante positiva, podemos dizer que:

$f(n)$ não é $\Omega(g(n))$

---
**Expressão:** $g(n) = \sqrt{n}$

**Desenvolvimento:**
$f(n) \geq c \cdot g(n)$
$5tn + 3t \geq c \cdot \sqrt{n}$
O crescimento de $n$ é mais acelerado que o crescimento de $\sqrt{n}$. Dado que o valor da constante $3t$ pode ser desprezado, podemos afirmar que:

$f(n)$ é $\Omega(g(n))$

---
### Theta

$$ \Theta(g(n)) = \{ f(n) : \exists c_1 > 0, c_2 > 0, n_0 > 0 \mid 0 \leq c_1 \cdot g(n) \leq f(n) \leq c_2 \cdot g(n), \forall n \geq n_0 \} $$

Video bom: https://www.youtube.com/watch?v=t0MhdT7Z-_U

Seja n um inteiro positivo e sejam f(n) e g(n) funções positivas. Dizemos que $f(n) = \Theta{(g(n))}$ (ou $f(n)$ é $\Theta{(g(n)}$) se existem constantes positivas $c_1$, $c_2$ e $n_0$ tais que $c_1 \cdot g(n) \leq f(n) \leq c_2 \cdot g(n) \ \forall \ n \geq n_0$. 


![[Pasted image 20241016012414.png]]


> [!NOTE] Dica
> Se provarmos que $f(n)=O(g(n))$ e $f(n)=\Omega{(g(n))}$, temos que $f(n)=\Theta{(g(n))}$. Na mesma lógica, se provarmos que $f(n) \neq O(g(n))$ ou $f(n) \neq \Omega{(g(n))}$, temos que $f(n) \neq \Theta{(g(n))}$


Exemplo: 
Dado a função $f(n) = 5tn + 3t$, verifique se $f(n)$ é $O(g(n))$ para:

--- 
**Expressão:** $g(n) = n$

**Desenvolvimento:**
Como $f(n)=O(g(n))$ e $f(n)=\Omega{(g(n))}$, $f(n)=\Theta{(g(n))}$

--- 
**Expressão:** $g(n) = n^2$

**Desenvolvimento:**
Como $f(n)=O(g(n))$ e $f(n) \neq \Omega{(g(n))}$, $f(n) \neq \Theta{(g(n))}$

--- 
**Expressão:** $g(n) = \sqrt{n}$

**Desenvolvimento:**
Como $f(n)=O(g(n))$ e $f(n) \neq \Omega{(g(n))}$, $f(n) \neq \Theta{(g(n))}$

---



Alguns outros exemplos: https://www.youtube.com/watch?v=vqVnHLett28



## Sobre a Prova 

**Como demonstrar formalmente que $f(n) = \Theta(g(n))$ \[ ou $\Omega(g(n))$, $O(g(n))$ \]?**

- Devemos achar um *conjunto de constantes* $c_1$, $c_2$ e $n_0$ \[ ou $c$, $n_0$ \] que torne verdadeira a condição de pertinência para o conjunto.
- Encontrar *apenas um trio (ou dupla) de constantes* é suficiente!

**E como demonstrar formalmente que $f(n) \neq \Theta(g(n))$ \[ ou $\Omega(g(n))$, $O(g(n))$ \]?**

- Não basta encontrar um trio (ou dupla) de constantes que não satisfaça a condição de pertinência.
- É preciso demonstrar que é *impossível* determinar um trio (ou dupla) de constantes que satisfaça a condição de pertinência.


