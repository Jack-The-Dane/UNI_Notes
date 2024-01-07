#Sampling
At omdanne et tidskontinuert signal til en sekvens af tidsdiskrete målinger (et periodisk pulstog).
## Impulssampling
#Impulssampling #Sampler
Opbygning af en impulssampler:
![[Pasted image 20230921082438.png]]
Sampleren karakteriseres ved den sampleinterval $T$ eller samplefrekvensen $f_s=\frac{1}{T} \text{[Hz]}$
Ved impulssampling er samplesignalet defineret som:
$$p(t) = \sum_{n=-\infty}^{\infty} \delta(t-nT)$$
 Det samplede signal $x_s(t)$ er dermed:
 $$x_s(t)=x(t) \cdot p(t) = x(t) \sum_{n=-\infty}^{\infty} \delta(t-nT)$$
 Samplesignalet $p(t)$ er periodisk med frekvens $f_S$, og kan dermed skrives som en uendelig kompleks Fourierrække:
 $$p(t)=\sum_{m=-\infty}^{\infty} c_me^{jm\omega_st}$$
 Hvor $\omega_s = 2 \pi f_s \text{ [rad/s]}$    
 $c_m=\frac{1}{T}$ 
 Det impulssamplede $x_s(t)$ kan dermed skrives:
 $$x_s(t)=\frac{1}{T} \sum_{m=-\infty}^{\infty} x(t)e^{jm \omega _st}$$ Signalets spektrum bliver så:
 $$X_s(\omega) = \frac{1}{T} \sum_{m=-\infty}^{\infty} X(\omega - m \omega_s)$$
 Hvilket også kan skrives:
 $$X_s(f) = \frac{1}{T} \sum_{m=-\infty}^{\infty} X(f - m f_s)$$
 Det kan ses at det oprindelige spektrum $X(f)$ er gentaget uendelig mange gange med afstand $f_s$ og at amplituden er skaleret med $1 \over T$ 
 ![[Pasted image 20230921084509.png]]
Det originale spektrum kan så genskabes med et lavpasfilter der kun lader det originale spektrum passere.
### Nyquist-Shannon Sætning
#Nyquist #Shannon #Nyquist-Shannon
![[Pasted image 20230921084951.png]]
Denne skal følges for at undgå overlap mellem gentagelserne af spektret.

## Pulssampling
#Puls #Pulssampling 
Impulssampling kan ikke realiseres i praksis, da pulsbredden vil blive større end nul. Det vil nærmere se således ud:
![[Pasted image 20230921090123.png]]
Her er $T$ sampleintervallet og $\tau$ er pulsbredden.
En pulssampler er modelleret (matematisk) ved at kombinere en impulssampler og et holdekredsløb:
![[Pasted image 20230921090256.png]]
Det vides at spektrumfunktionen for en rektangulærpuls er:
$$F(\omega)=\tau sinc(\omega \frac{\tau}{2})$$
Holdekredsløbets spektrumfunktion bliver dermed:
$$H(\omega)=\tau sinc(\omega \frac{\tau}{2}) e^{-j\omega \frac{\tau}{2}}$$
Dutyfaktoren for det pulssamplede signal er defineret som $d=\frac{\tau}{T}$ 
Frekvensspektrum for det pulssamplede signal er:
$$X'_s(f) = X_s(f)H(f) = \frac{1}{T} \sum_{m=-\infty}^{\infty} X(f - m f_s) \tau sinc(\pi d \frac{f}{f_s})e^{-j \pi d \frac{f}{f_s}}$$
Amplitudespektrum bliver så:
$$\vert X'_s(f) \vert = d \vert sinc(\pi d \frac{f}{f_s}) \vert \sum_{m=-\infty}^{\infty} X(f - m f_s) $$
Det har følgende konsekvens for amplitudespektrummet:
![[Pasted image 20230921091404.png]]
