Når der laves en FFT analyse på en sekvens, så er den anvendte sekvens fundet fra
impulsresponset $h_\infty (n)$ ganget med den rektangulære vinduesfunktion, dvs.
$$h(n) = h_\infty (n) w(n)$$
hvor
$$w(n) = \cases{1 \;\;\;\; \text{hvis} -M \leq n \leq M \cr 
0 \;\;\;\; \text{ellers}}$$
![[Pasted image 20231005082748.png]]
## Frekvensrespons
![[Pasted image 20231005084519.png]]
![[Pasted image 20231005084537.png]]
En multiplikation af signaler i tidsdomæne giver en foldning i frekvensdomænet.
![[Pasted image 20231005085123.png]]
![[Pasted image 20231005085142.png]]

## Rektangulært vindue
![[Pasted image 20231005085449.png]]
Som det kan ses er bredden på main loben ikke så stor, men amplituden af side lobes er forholdsvist stor.

## Bartlett vindue
![[Pasted image 20231005091025.png]]
Det kan ses at main lobe er noget bredere end for rektangulært, men til gengæld er sidelobes amplitude også lavere. Har altså mindre Gibbs oscillationer.
## Hamming og Hanning vindue
![[Pasted image 20231005091457.png]]
![[Pasted image 20231005091519.png]]
