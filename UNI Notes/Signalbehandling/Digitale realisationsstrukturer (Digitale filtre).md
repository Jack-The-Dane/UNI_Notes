## Direkte realisationsstrukturer
Der tages udgangspunkt i differensligning af orden $N$:
$$
y(n)=\sum_{i=0}^{N}a_ix(n-i)-\sum_{i=1}^{N}b_iy(n-i)
$$
Ved z-transformation fås følgende overføringsfunktion:
$$
H(z) = {Y(z) \over X(z)} = \frac{\sum_{i=0}^{N}a_iz^{-i}}{1+\sum_{i=1}^{N}b_iz^{-i}}
$$
Denne differenslinging kan implementeres på flere måder:
Direkte Type 1
Direkte Type 2

Blokdiagrammer benyttes til at illustrere implementeringen af tidsdiskrete systemer:
![[Pasted image 20231025214619.png]]
Cirkler er summationstegn, trekanter er forstærkning og firkanter er forsinkelse.

### Direkte Type 1
![[Pasted image 20231025214933.png]]
I denne struktur skal der gemmes et antal samples svarende til $N$ (filterorden) fra inputtet til brug i udregningen. Det samme skal gøres for outputtet, så der skal bruges i alt $2N$ hukommelsesblokke.
#### Eksempel
![[Pasted image 20231025215213.png]]
![[Pasted image 20231025215457.png]]

### Direkte Type 2
Direkte type 1 strukturen benytter $2N$ forsinkelseselementer, dvs. $2N$ værdier skal gemmes i filtret.
Direkte type 2 strukturen benytter kun $N$ forsinkelseselementer, hvilket kræver mindre hukommelse.
![[Pasted image 20231025215733.png]]
den nye funktion $W(z)$ vil fungere som udgangssignal for $X(z)$ og som indgangssignal for $Y(z)$. Hvis dette tegnes i et diagram, ser det således ud:
![[Pasted image 20231025220131.png]]
Dermed skal der kun gemmes $N$ samples i hukommelsen.

## Kaskade- og parallelrealisation
Når et filter skal implementeres, så representeres koefficienterne med et endeligt antal bits, hvilket betyder at de afrundes. Derfor er det vigtigt at mindske filtrets koefficientfølsomhed. 
Følgende giver stor koefficientfølsomhed
1. Systemets poler eller nulpunkter er placeret tæt sammen i z-planet. Dette sker fx hvis amplitudekarakteristikken har stejle flanker.
2. Systemet har poler med lille polargument. Dette sker når samplefrekvensen er valgt høj i forhold til systemets afskæringsfrekvens.
3. Systemet er af høj orden. Dette sker hvis systemet implementeres i en direkte type 1 eller type 2 realisationsstruktur. Fordi overføringsfunktionerne er meget følsomme overfor afrundinger i koefficienterne.

### Kaskaderealisation
Et højereordens system implementeres ofte som en kaskadekobling givet som følger:
$$
H(z)=H_1(z)\cdot H_2(z) \cdot H_3(z) \cdot \cdot \cdot \cdot H_M(z)$$
![[Pasted image 20231025220737.png]]
![[Pasted image 20231025220753.png]]
#### Skalering
![[Pasted image 20231025220809.png]]

#### Eksempel
![[Pasted image 20231025221008.png]]
![[Pasted image 20231025221126.png]]

### Parallelrealisation
![[Pasted image 20231025221350.png]]
Det gør man ved hjælp af partialbrøk opløsning
![[Pasted image 20231025221508.png]]
![[Pasted image 20231025221523.png]]
![[Pasted image 20231025221605.png]]
![[Pasted image 20231025221930.png]]
![[Pasted image 20231025222108.png]]
