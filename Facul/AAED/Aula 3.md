


![[../../../Aula3_SIN5013_2024.pdf]]


# Notações Assintóticas


## Definição
É uma abstração que nos permite focar no que ocorre com $f(n)$ quando n cresce indefinidamente.
- Termos de menor ordem não importam 
- constates não importam 
- em $f(n) = 2n^3 + 4000n^2 + 1000n - 47$, nos importa apenas $f(n)=n^3$

## Notações

### Big O 

Vídeo bom: https://youtu.be/gjw7AaOs9P8?si=cVtBMvJeiIiNGEXo

Seja n um inteiro positivo e sejam $f(n)$ e $g(n)$ funções positivas. Dizemos que $f(n)=O(g(n))$ (ou $f(n)$ é $g(n)$) se existem constantes positivas $c$ e $n_0$ tais que $f(n) \leq c \cdot g(n) \ \forall \ n \geq n_0$. 

![[../../../Screenshot 2024-10-15 at 10-30-12 Telegram Web.png]]


Exemplo: 
Dado a função $f(n) = 5tn + 3t$, verifique se $f(n)$ é $O(g(n))$ para:

$g(n) = n$
Para 
$f(n) = O(n)$ 
$f(n) \leq c.g(n)$
$5tn + 3t \leq c.g(n)$



f()

$g(n) = n^2$

$g(n) = \sqrt{n}$




### Omega 



### Theta

