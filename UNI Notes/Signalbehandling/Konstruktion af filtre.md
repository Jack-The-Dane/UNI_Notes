#konstruktion 
Filtre konstrueres normalt som en kaskade (sekvens) af 1. og 2. ordens filtre. Rækkefølgen af filtrene betyder noget og vælges ud fra de karakteristikker man ønsker. 
Den generelle overføringsfunktion for et lavpasfilter bruges ikke, da denne sætter meget høje krav til enten hardware konstruktion eller software resourcer.

### Eksempel
Implementering af 5. grads Chebyshev filter.
$$H(s) = \frac{A_0}{s⁵ +B_4s⁴+B_3s³+B_2s²+B_1s+b_0}$$
Dette filter kan implementeres som en sekvens af to 2. ordens filtre og et 1. ordensfilter
![[Pasted image 20230914092040.png]]

