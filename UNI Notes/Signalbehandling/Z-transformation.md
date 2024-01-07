Definition af $z$ - transformationen af en kausal sekvens $x(n)$ :
$$X(z) = \sum_{n=0}^{\infty} x(n)z^{-n}$$
Bemærk at denne konvergerer hvis $\vert z \vert \lt 1$ 
## Notation
Følgende notation benyttes til (invers) $z$-transformation
$$X(z) = \mathcal{Z}[x(n)]$$
$$x(n) = \mathcal{Z}^{-1}[X(z)]$$
## Relation mellem Laplace og Z-transformation
Den Laplace transformerede af en sekvens $x(n)$
$$X_s(s)=\sum_{n=0}^{\infty}x(n)e^{-snT}
$$
Sammenlignes dette med $z$-transformation ses det at 
$$X_s(s) = X(z) \;\;\;\; \text{når} \;\; z=e^{st}$$
Det kan også ses at 
$$s={1 \over T}\ln(z)$$
Så den generelle relation mellem $s$ og $z$ er 
$$z = e^{sT} \;\;\;\; \text{hvor } \; s=\sigma + j\omega$$
På polær form kan $z$ skrives
$$ z = e^{sT} = e^{\sigma \over f_s} \angle 2\pi {f \over f_s}$$
For $\sigma \lt 0$ fås $\vert z \vert \lt 1$. Dermed kommer venstre halvplan af s-planet (alle stabile systemer) til at ligge inden for enhedscirklens radius
![[Pasted image 20231011222856.png]]
Ud fra figuren kan det ses at linjer i s-planet bliver til vinkler i z-domænet. Jo større imaginær værdi, jo større vinkel. 

## Regler for Z-transformation
![[Pasted image 20231011223548.png]]

## Z-transformationspar
![[Pasted image 20231011224130.png]]

## Overføringsfunktion
![[Pasted image 20231011225522.png]]
![[Pasted image 20231011225614.png]]

### 1. Ordenssystem
![[Pasted image 20231011225634.png]]
### 2.Ordenssystem
![[Pasted image 20231011225651.png]]

## Poler og nulpunkter
### Poler
Et tidsdiskret system har poler for værdierne af z hvor $H(z)$ er lig med ∞, dvs. polerne er
rødder for nævnerpolynomiet af $H(z)$.
En overføringsfunktion
$$H(z) = {P(z) \over Q(z)}$$
har poler for værdier af $z$ hvor $Q(z)=0$.
### Nulpunkter
Et tidsdiskret system har poler for værdierne af z hvor $H(z)$ er lig med 0, dvs. polerne er
rødder for tællerpolynomiet af $H(z)$.
En overføringsfunktion
$$H(z) = {P(z) \over Q(z)}$$
har nulpunkter for værdier af $z$ hvor $P(z)=0$.

## Invers Z-transformation
Invers z-transformation benyttes til at bestemme udgangsresponset y(n) for et tidsdiskret
system for en given indgangsstimulus x(n). Denne analyse foregår efter følgende
procedure
1. Systemets overføringsfunktion H(z) opstilles med positive potenser af z.
2. Indgangssekvensen x(n) z-transformeres. (Anvend tabelopslag)
3. Udgangsresponset i z-domæne beregnes Y (z) = H(z)X(z).
4. Udgangssekvensen y(n) udregnes ved invers z-transformation af Y (z). (Anvend
tabelopslag)
![[Pasted image 20231011230435.png]]
### Eksempel
![[Pasted image 20231011230557.png]]
![[Pasted image 20231011230638.png]]
Da $\ln(0, 5) = −0, 693$ kan $y(n)$ også skrives $y(n) = e^{−0,693n}$.

## Invers z-transformation ved partialbrøkopløsning
![[Pasted image 20231011231032.png]]![[Pasted image 20231011231106.png]]

### Eksempel
![[Pasted image 20231011231255.png]]
![[Pasted image 20231011231456.png]]
![[Pasted image 20231011231803.png]]
