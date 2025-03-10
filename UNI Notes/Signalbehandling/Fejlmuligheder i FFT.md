
## Aliasering
![[Pasted image 20231005093323.png]]
![[Pasted image 20231005093346.png]]

## Lækage-fænomenet
En Fast Fourier Transformation udføres på et signal med N samples. Dette svarer til at
signalet $x(n)$ er blevet multipliceret med en rektangulær vinduesfunktion med længde N.
Hvad er konsekvensen ved at anvende en rektangulært vinduesfunktion?
![[Pasted image 20231005093854.png]]
![[Pasted image 20231005093909.png]]

## Picket fencing
Når der udføres en N-punkts DFT, så vil afstanden mellem frekvenser i DFTen være
$F = fs=N$. Hvis der ønskes en højere opløsning af frekvensspektrum, så kan zero filling
anvendes, så signalet forøges til $L$ samples.
![[Pasted image 20231005094437.png]]
En eventuel vinduesfunktion skal kun omfatte de oprindelige $N$ samples.
I billedet er den optrukne linje det rigtige frekvensspektrum, mens de lodrette linjer er outputtet af DFT'en. Man ser altså ikke alle peaks i det øverste spektrum. Der er ingen konsekvens af at fylde 0'er ind efter signalet, da man teknisk set allerede har gjort det, da man brugte et rektangulært vindue. Den eneste ulempe, er at udregningen kommer til at tage længere tid, jo flere 0'er man putter på. 