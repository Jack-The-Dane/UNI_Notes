De 4 grundlæggende filtertyper:
Lavpas: Tillader signaler med lav frekvens at passere, blokerer høje frekvenser
Højpas: Tillader signaler høj frekvens at passere, blokerer lave frekvenser
Båndpas: Tillader signaler med bestemte frekvenser at passere, blokerer alt andet
Båndstop: Blokerer bestemte frekvenser, lader alle andre frekvenser passere.
![[Pasted image 20230914082443.png]]
Terminologi:
Pasbånd: Frekvensområde, hvor signalet passerer igennem filteret
Stopbånd: Frekvensområde, hvor signalet dæmpes af filteret. 

For at designe et filter skal der bruges 3 oplysninger:
1. En (eller flere) afskæringsfrekvenser, til at angive frekvensområde
2. En stopbåndsfrekvens, hvor det er specificeret hvor stor en dæmpning filteret skal have ved den frekvens.
3. Information om hvor meget forstærkningsvariation der må være i pasbåndet.
![[Pasted image 20230914084857.png]]
Gruppeløbstid: 
Hvor stor tidsforsinkelse der er igennem filteret, afhænger ofte af frekvensen. Denne skal være konstant, hvis man vil undgå pulsoversving eller dæmpet oscillation.
Er defineret ved:
$$T_g = - \frac{d\phi(\omega)}{d\omega} [s]$$
Hvis filteret har konstant forsinkelse ved alle frekvenser, kaldes det at filteret har lineær fase.
#filtre #lavpas #højpas #båndpas #båndstop #pasbånd #stopbånd #gruppeløbstid #signalbehandling