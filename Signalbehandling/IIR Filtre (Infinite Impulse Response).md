Et IIR filter har altid poler, så stabilitet skal overvejes.

### Forskelle imellem FIR filtre og IIR filtre
- Et FIR filter har 5 til 10 gange større realisationsstruktur end et tilsvarende IIR filter.
- Et FIR filter er altid stabilt, da det kun har nulpunkter.
- Et FIR filter kaldes en ikke-rekursiv struktur, mens et IIR filter kaldes en rekursiv struktur.
- Et FIR filter er mindre sensitivt overfor koefficientændringer og afrundingsfejl end et IIR filter.

## Design af IIR filtre
Digitale IIR-filtre kan designes ved transformation af prototype-filtre i s-domæne ved brug af følgende metoder.
- Matched z-transformation
- Impuls invariant z-transformation
- Bilineær z-transformation

### Fremgangsmåde
Et IIR-filter designes ved at følge proceduren
1. Filtrets specifikationer opstilles
2. Filtrets z-domæne overføringsfunktion opstilles. (Matched, Impulse Invariant eller Bilineær z-transformation benyttes.)
3. Der vælges optimal realisationsstruktur
4. Der fremstilles program til signalprocessor eller tegnes diagram for hardwareløsning

#### 1.
Fremgangsmetoden for design af IIR-filtre er z-transformation af et analogt prototype filter, dvs. vi transformerer
![[Pasted image 20231102082456.png]]
Transformationen fra s-domæne til z-domæne flytter polerne i s-planen til poler i z-planen, der giver et lignende Bode plot og filterrespons.
![[Pasted image 20231102082603.png]]
Læg mærke til at bode-plottene ikke er ens. Foldningsfrekvensen $f_o$ har flyttet sig. 

#### Matched z-transformation
Følgende procedure benyttes til design af digitale filtre ved brug af matched z-transformation
1. Bestem det analoge prototypefilters frekvensnormerede og faktoriserede overføringsfunktion H(s).
2. Bestem de analoge frekvensnormerede poler og nulpunkter.
3. Bestem de denormerede poler og nulpunkter. (Gang poler og nulpunkter med cutoff eller centerfrekvens (rad/s))
4. Bestem den digitale overføringsfunktions koefficienter.
5. Opskriv overføringsfunktionen og gang en konstant på, for at få konstant DC-forstærkning. Find konstanten med ligningen:
$$H(s) \vert _{s=0} = H(z) \vert _{z=1}$$
7. Implementer overføringsfunktionen som en kaskadestruktur.

Ved matched z-transformation overføres prototypefiltrets poler og nulpunkter direkte til z-domæne ved brug af formlen. (Poler og nulpunkter sættes ind for s i formlen)
$$z=e^{sT}$$
hvilket også kan skrives (Imaginær akse):
$$z=e^{j \omega T}$$
Real aksen bliver: ($s?\sigma,  \sigma \lt 0$)
$$z=e^{\sigma T}$$
![[Pasted image 20231102083350.png]]
Dette vil tage formen
![[Pasted image 20231102083518.png]]

##### Generelt eksempel
![[Pasted image 20231102083616.png]]
Læg mærke til at ved overførsel til z-domæne tilføjes et nulpunkt i (0,0), men dette får ingen betydning for amplitudekarakteristikken, da det ligger i (0,0). Men det får betydning for fasen.
![[Pasted image 20231102084513.png]]
##### Eksempel 1. orden
![[Pasted image 20231102084626.png]]
- 1. ordens filter, så dæmpning efter polen, 20 dB/decade
![[Pasted image 20231102084915.png]]
![[Pasted image 20231102084948.png]]

##### Eksempel 2. orden
![[Pasted image 20231102085305.png]]
![[Pasted image 20231102085500.png]]
For at finde $a_0$ sættes $z=1$ og så isoleres $a_0$
![[Pasted image 20231102085552.png]]

##### Eksempel 2.orden Butterworth
Design et digitalt 2. ordens Butterworth lavpasfilter med afskæringsfrekvens $f_a$ = 800 Hz
ved brug af Matched z-transformation med samplefrekvens på 8 kHz.
En frekvensnormeret overføringsfunktionen for et 2. ordens Butterworth lavpasfilter med
afskæringsfrekvens $f_a$ = 800 Hz er givet som
![[Pasted image 20231102085905.png]]
![[Pasted image 20231102090035.png]]
