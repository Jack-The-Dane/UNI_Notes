FIR Filtre designes ved hjælp af FFT.

## Definition
Et Finite Impulse Response filter, har et endeligt impulsrespons, som definerer filterets størrelse. 
Et FIR-filter med N samples har impulsresponssekvens:
![[Pasted image 20231109082111.png]]
![[Pasted image 20231109082134.png]]

Alle poler for et FIR-filter vil ligge i Origo, så et FIR filter kan ikke blive ustabilt. 

Udgangssekvensen af et FIR filter vil bestå af en vægtet sum af indgangssekvensen.

Realisationsstrukturen for et FIR filter, vil derfor kun afhænge af tidligere og nuværende indgangssekvenser, og ikke af tidligere udgangssignaler. Dette er også grunden til at impulsresponset er endeligt.

![[Pasted image 20231109082844.png]]
Filteret har lineær fase, da nulpunkterne er i par rundt om real-aksen, som set på figuren.

![[Pasted image 20231109083226.png]]

![[Pasted image 20231109083317.png]]
