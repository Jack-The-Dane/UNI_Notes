Tidsdiskret foldning kan benyttes til udregning af udgangssekvensen for et tidsdiskretsystem ved brug af indgangssekvensen $x(n)$ og impulsresponset $h(n)$.
![[Pasted image 20231025210503.png]]
foldningssummen er defineret som:
$$
y(n) = x(n) \cdot h(n) = \sum_{m=0}^{n} x(m)h(n-m)
$$
$h$ er forskinket med tiden m, hvilket svarer til en vægtet sum af impulser, hvor vægtningen til en given tid, er indgangssignalet.
Udgangssekvensen $y(n)$ kan også udregnes: 
$$
y(n) = h(n) \cdot x(n) = \sum_{m=0}^{n} h(m)x(n-m)
$$
Men det giver det samme.
## Eksempel
Vi betragter et system med følgende impulsrespons og indgangssekvens:
![[Pasted image 20231025211144.png]]
Vi vil bestemme udgangssekvensen $y(n)$ ved brug af tidsdiskret foldning:
$$
y(n) = h(n) \cdot x(n) = 0,5^n \cdot [u(n)-u(n-4)]
$$
Hvor $u(n)$ er enhedsspringsekvensen.
Udgangssekvensen udregnes ved brug af:
$$
y(n) = \sum_{m=0}^{n} h(m)x(n-m)
$$
for $n=0$ haves:
$$y(0)=h(0)x(0)$$
![[Pasted image 20231025211657.png]]

for $n=1$ haves:
$$y(1)=h(0)x(1)+h(1)x(0)$$
for $n=2$ haves:
$$y(2)=h(0)x(2)+h(1)x(1)+h(2)x(0)$$
![[Pasted image 20231025212629.png]]
