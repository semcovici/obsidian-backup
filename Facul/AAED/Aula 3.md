
![[Aula3_SIN5013_2024.pdf]]

![[../../../Aula3_SIN5013_2024.pdf]]


## Definição
É uma abstração que nos permite focar no que ocorre com $f(n)$ quando n cresce indefinidamente.
- Termos de menor ordem não importam 
- constates não importam 
- em $f(n) = 2n^3 + 4000n^2 + 1000n - 47$, nos importa apenas $f(n)=n^3$

## Notações

### Big O 

Vídeo bom: https://youtu.be/gjw7AaOs9P8?si=cVtBMvJeiIiNGEXo

Seja n um inteiro positivo e sejam $f(n)$ e $g(n)$ funções positivas. Dizemos que $f(n)=O(g(n))$ (ou $f(n)$ é $g(n)$) se existem constantes positivas $c$ e $n_0$ tais que $f(n) \leq c \cdot g(n) \ \forall \ n \geq n_0$. 
![[Pasted image 20241015224000.png]]
Exemplo: 
Dado a função $f(n) = 5tn + 3t$, verifique se $f(n)$ é $O(g(n))$ para:

--- 
**Expressão:** $g(n) = n$

**Desenvolvimento:**
$f(n) = O(n)$ 
$f(n) \leq c \times g(n)$
$5tn + 3t \leq c \times n$
$5t + \frac{3t}{n} \leq c$
Dado que n cresce indefinidamente, o termo $\frac{3t}{n}$ tende a 0, assim podemos desprezá-lo. Tendo assim:
$5t \leq c$
Dado que c é uma constante positiva que pode assumir um valor qualquer, podemos atribuir um valor a ela como $6t$ que torna a expressão verdadeira, já que $5t \leq 6t$. Dessa forma, podemos dizer que:
$f(n)$ é $O(g(n))$

---
**Expressão:** $g(n) = n^2$

**Desenvolvimento:**
$f(n) \leq c \times g(n)$
$5tn + 3t \leq c \times n^2$
$\frac{5t}{n} + \frac{3t}{n^2} \leq c$
Dado que n cresce indefinidamente, os termos $\frac{5t}{n}$ e $\frac{3t}{n^2}$ tendem a 0, assim podemos desprezá-los. Tendo assim:
$0 \leq c$
Dado que c é uma constante positiva que pode assumir um valor qualquer, necessariamente essa afirmação é verdadeira. Dessa forma, podemos dizer que:
$f(n)$ é $O(g(n))$

---

**Desenvolvimento:**
$f(n) \leq c \times g(n)$
$5tn + 3t \leq c \times n^2$
$\frac{5t}{n} + \frac{3t}{n^2} \leq c$
Dado que n cresce indefinidamente, os termos $\frac{5t}{n}$ e $\frac{3t}{n^2}$ tendem a 0, assim podemos desprezá-los. Tendo assim:
$0 \leq c$
Dado que c é uma constante positiva que pode assumir um valor qualquer, necessariamente essa afirmação é verdadeira. Dessa forma, podemos dizer que:

$f(n)$ é $O(g(n))$

> Essa afirmação também se expande para $g(n) = n^k \ \forall \ k \geq 1$.

--- 
**Expressão:** $g(n) = \sqrt{n}$

**Desenvolvimento:**
$f(n) \leq c \times g(n)$
$5tn + 3t \leq c \times \sqrt{n}$
O termo $5tn + 3t$ cresce linearmente, enquanto o termo $\sqrt{n}$ irá crescer mais lentamente já que, necessariamente, a raiz de $n$ ($\sqrt{n}$) cresce mais lentamente que $n$. Dessa forma, podemos dizer que:

$f(n)$ não é $O(g(n))$

> Essa afirmação também se expande para $g(n) = n^k \ \forall \ k \l 1$.
> 

---



### Omega 



### Theta

