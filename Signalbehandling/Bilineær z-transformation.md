Formålet med bilineær z-transformation er at eliminere den aliaseringsfejl, der opstår ved både matched z-transformation og impuls invariant z-transformation.
Ved bilineær z-transformation substitueres $s$ i $H(s)$ med en funktion af $z$ ($s=f(z)$), dvs
$$H(z) = H(s) \vert _{s=f(z)}$$
Jævnfør relationen mellem s og z, $z = e^{sT}$ må s være $s = {1 \over T} \ln{z}$ 
Denne funktion for s vil vi gerne indsætte i overføringsfunktionen, men dette giver ikke en rationel funktion (en funktion med et polynomium i tæller og nævner),derfor aproksimeres $\ln{z}$.

## Approksimation af logaritme
Den naturlige logaritme er defineret som den uendelige sum:
![[Pasted image 20231106214245.png]]
Men dette kan ikke indsættes i overføringsfunktionen, da vi ville få et uendelig langt udtryk.
Derfor approksimeres logaritmen som:
$$\ln(z) \approx 2{z-1 \over z +1}$$
Afvigelsen mellem de to funktioner kan ses her:
![[Pasted image 20231106214520.png]]

## Princip
![[Pasted image 20231106214634.png]]
Der ganges igennem med $1+z^{-1}$ på begge sider af brøkstregen for ikke at have en brøk i nævneren.

## Relation mellem s- og z-plan
### Amplitude
![[Pasted image 20231106214915.png]]
![[Pasted image 20231106215035.png]]
![[Pasted image 20231106215048.png]]
Højre halvplan af s-planen er så mappet til alt det uden om enhedscirklen i z-planen.

### Fase
![[Pasted image 20231106215502.png]]
Det at argumentet for z går mod 180 grader er forskellen mellem rigtig z-transformation, og bilineær z-transformation. Det er denne egenskab der gør at frekvensaksen bliver forvrænget efter transformationen.
## Frekvens warping
Da frekvensområdet $0< f <∞$ for det analoge filter transformeres til frekvensområdet $0< f < f_o$ for det digitale filter, bliver frekvensaksen deformeret. Dette påvirker afskæringsfrekvensen $ω_a$ og stopbåndsfrekvensen $ω_s$ for det digitale filter.
![[Pasted image 20231106215954.png]]
Som det kan ses bliver afskæringsfrekvensen og stopbåndsfrekvensen rykket lidt ned. Dette kan modvirkes ved at rykke sine frekvenser lidt op før man laver bilineær z-transformation, da man ved hvor meget de bliver flyttet.
Hvor meget de skal flyttes findes således:
![[Pasted image 20231106220401.png]]
efter første brøk er der blevet ganget igennem med $e^{j \omega {T \over 2}}$ 
Dette giver noget der kan omskrives ved hjælp af eulers identiteter, og det kan så videre omskrives til tangens, udfra trigonometriske identiteter.
Det endelige tal kan sammenlignes med det orginale tal:
![[Pasted image 20231106220824.png]]
Så jo højere frekvensen bliver, jo mere upræcis bliver tangens-relationen (den blå streg).
Dette er forsøgt illustreret her:
![[Pasted image 20231106221034.png]]
Som det kan ses er pasbåndet blevet noget smallere. 

### Eksempel
![[Pasted image 20231106221318.png]]
![[Pasted image 20231106221445.png]]

## Prewarping
![[Pasted image 20231106221520.png]]

### Eksempel
![[Pasted image 20231106221653.png]]
![[Pasted image 20231106221709.png]]
![[Pasted image 20231106221746.png]]
For det specifikke filter er det nødvendige ordenstal 3.
Proceduren for at finde det digitale filter ud fra det frekvensnormerede prototype filter er
1. Denormer prototypefiltret til den prewarpede afskæringsfrekvens $Ω_a$ 
2. Find det digitale filter ved bilineær z-transformation

![[Pasted image 20231106221848.png]]
![[Pasted image 20231106221910.png]]
![[Pasted image 20231106221950.png]]

## Koefficienter af 1. Ordenssystem
![[Pasted image 20231106222119.png]]
![[Pasted image 20231106222132.png]]

### Eksempel
![[Pasted image 20231106222333.png]]
![[Pasted image 20231106222400.png]]
![[Pasted image 20231106222445.png]]
![[Pasted image 20231106222501.png]]

## Koefficienter af 2. Ordens systemer
![[Pasted image 20231106222601.png]]
![[Pasted image 20231106222624.png]]
![[Pasted image 20231106222638.png]]

### Eksempel
![[Pasted image 20231106222734.png]]
![[Pasted image 20231106222757.png]]
![[Pasted image 20231106222808.png]]
Amplitude og fase plot:
![[Pasted image 20231106222819.png]]
Impulsrespons:
![[Pasted image 20231106222854.png]]

## Design af højpas filter ved bilineær z-transformation
**Design procedure:**
![[Pasted image 20231106223128.png]]
**Bestemmelse af konstanter**
![[Pasted image 20231106223251.png]]
**Bestemmelse af ordenstal og overføringsfunktion**
![[Pasted image 20231106223330.png]]
![[Pasted image 20231106223452.png]]
