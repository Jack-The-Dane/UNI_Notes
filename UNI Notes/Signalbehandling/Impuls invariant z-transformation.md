Kategorien af z-transformationer kaldet input invariant z-transformation karakteriseres ved at lade responset til en bestemt type indgangssignal (step, impuls, rampe) være invariant under z-transformation.
Vi kigger på impuls invariant z-transformation, dvs.
$$h(n)=h(nT)=h(t) \vert _{t=nT}$$

![[Pasted image 20231102091427.png]]

## Fremgangsmåde
For at finde en impulsinvariant z-transformation, så z-transformeres impulsresponset
$$H(z)=T \cdot Z[h(n)]$$
![[Pasted image 20231102091539.png]]
![[Pasted image 20231102091651.png]]

### 1. ordens systemer
![[Pasted image 20231102092143.png]]

### 2. Ordens systemer
![[Pasted image 20231102092222.png]]
![[Pasted image 20231102092434.png]]

## Design procedure
Følgende procedure benyttes til design af digitale filtre ved brug af impuls invariant z-transformation
1. Bestem det analoge prototypefilters frekvensnormerede overføringsfunktion H(s).
2. Partialbrøksopløs H(s) til 1. og 2. ordens overføringsfunktioner (maksimalt antal 2. ordens overføringsfunktioner).
3. Denormer koefficienterne ki og polerne σi + jωi ved multiplikation med afskæringsfrekvensen eller centerfrekvensen.
$$H(z) = T \sum_{i=1}^{N}k_{i}\frac{z}{z - e^{s_{i}T}} = T \sum_{i=1}^{N}k_{i}\frac{1}{1 - e^{s_{i}T}z^{-1}}$$
For 2.orden brøker, se Balders noter. (Transformation af 2. Ordens overføringsfunktion)
1. Bestem den digitale overføringsfunktions koefficienter.

2. Implementer overføringsfunktionen som en parallelstruktur.

### Eksempel 2. ordens Butterworth
![[Pasted image 20231102092807.png]]
![[Pasted image 20231102093324.png]]
![[Pasted image 20231102093402.png]]
![[Pasted image 20231102093426.png]]
Amplituden er magen til Matched z-transformation, men fasen følger det analoge filter meget tættere.