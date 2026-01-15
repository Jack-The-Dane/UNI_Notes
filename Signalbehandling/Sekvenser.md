Vi betragter kun kausale sekvenser:
$$x(nT) = 0 \text{    for } n\lt 0$$
Sekvenser kan så udtrykkes som funktioner af samplenummeret $n$ som vist her:
$$x(n) = \sum_{k=0}^{\infty} x(kT) \delta (kT-nT)$$
Enhedssamplen og enhedsspringsamplen:
![[Pasted image 20230921093437.png]]
Ved brug af enhedssamplen $\delta(n)$ kan sekvensen $x(n)$ udtrykkes som:
$$x(n) = \sum_{k=0}^{\infty} x(k) \delta (n-k)$$
Spektrum for det impulssamplede signal $x_s$ kan findes ved Laplacetransformation af:
$$x_s(t)= \sum_{n=0}^{\infty} x(nT) \delta (t-nT)$$
Ved Laplacetransformation fås:
$$X_s(s) = \sum_{n=0}^{\infty} x(nT) e^{-snT}$$
### Eksempel
![[Pasted image 20230921094439.png]]
![[Pasted image 20230921094505.png]]
![[Pasted image 20230921094531.png]]
![[Pasted image 20230921094542.png]]
Det er nu Z-transformationen bliver relevant, for at undgå gentagelserne langs den imaginære akse.
