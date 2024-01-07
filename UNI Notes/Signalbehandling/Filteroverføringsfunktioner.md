Tre filterfunktionstyper:
1. Butterworth
2. Chebyshev
3. Bessel
Disse filtre er allpole filtre, kigger altså kun på poler ikke nulpunkter.
En fjerde type kunne være et epilliptisk filter
![[Pasted image 20230914090706.png]]
![[Pasted image 20230914090803.png]]
## Butterworth filter
#Butterworth
Et butterworth filter har følgende egenskaber:
1.  Tæt på konstant forstærkning i pasbåndet. 
2. Dæmpning på 3 dB ved afskæringsfrekvens og herefter falder forstærkning med 20 dB/dec
3. Filterets fase er ikke konstant  i pasbåndet, hvilket giver ringing ved step-input.
Alle polpar for et butterworthfilter har egenfrekvens der er lig afskæringsfrekvensen.

Det kvadrerede amplituderespons for et N'te ordens Butterworthfilter er:
$$\vert H(j\omega)\vert² = \frac{1}{1+(\omega / \omega_a)^{2N}}$$
Hvor $\omega_a [rad/s]$ er afskæringsfrekvensen.
![[Pasted image 20230913183422.png]]
Alle poler for $H(j\omega)$ ligger i venstre halvplan på en cirkel med radius $\omega_a$ og centrum i origo.
![[Pasted image 20230913183602.png]]
## Chebyshev filter
#Chebyshev
Et Chebyshev filter har følgende egenskaber:
1. Varierende forstærkning i pasbåndet, størrelsen på denne variation kan vælges frit.
2. Dæmpning falder hurtigt omkring afskæringsfrekvensen
3. Fasen er ikke konstant i pasbåndet, hvilket giver ringing ved step-input.

DC-forstærkning (forstærkning ved nul frekvens) er ikke filterets maksimale forstærkning, hvis polantallet er lige.
![[Pasted image 20230914091459.png]]
Det kvadrerede amplituderespons for et N'te ordens Chebyshevfilter er:
$$\vert H(\omega)\vert² = \frac{1}{1+\epsilon²T_N^2(\omega/\omega_a)}$$
Hvor $T_N(\omega)$ er Chebyshev polynomium af grad $N$ givet ved:
$$T_N(\omega) = \cases{cos(Ncos^{-1}(\omega)) & $\vert \omega \vert \leq 1 $\cr
cosh(Ncosh^{-1}(\omega)) & $\vert \omega \vert \gt 1$}$$
Pasbåndsripplens størrelse $\delta$ i dB er givet af $\epsilon$ :
$$\delta = 10\log_{10}(\epsilon²+1)$$

## Bessel filter
#Bessel
Et Bessel filter har følgende egenskaber:
1. Har ikke ripple i pasbåndet, men er ikke lige så konstant som Butterworth filteret.
2. Meget glidende dæmpning. Amplitude karakteristikken er som for første ordens filter for de første 6 dB's dæmpning uanset polantal. 
3. Fasen er næsten lineær med frekvensen inden for pasbåndet.

Overføringsfunktionen for et N'te ordens Besselfilter er:
$$H_N(s) = \frac{b_0}{S^N+b_{N-1}s^{N-1}+...+b_1s+b_0}$$
Hvor
$$b_k=\frac{(2N-k)!}{2^{N-k}k!(N-k)!}$$

## Valg af ordenstal
#ordenstal
Ordenstallet vælges ud fra dæmpning i stopbåndet. 
Alle grafer bliver normeret, dvs. forstærkningen er $Y=20\log \frac{A}{A_{max}}$ og det samme bliver frekvensen, så $X = \frac{\omega}{\omega_a}$ 
Når dette er gjort plottes filterets karakteristik i adskillige ordner, og den laveste orden, der overholder kravene vælges.
![[Pasted image 20230914091731.png]]

### Eksempel
Find polantallet for et lavpasfilter med kravene:
1. Afskæringsfrekvens $f_a = 2 \text{kHz}$ 
2. Stopbåndsfrekvens $f_s=8 \text{kHz}$
3. Stopbåndsdæmpning i forhold til $A_{max}$ på mindst 60 dB
Den normerede stopbåndsfrekvens er $\frac{f_s}{f_a}=4$ 
Man vælger normalt så lavt et ordenstal som muligt, der stadig overholder kravene:
![[Pasted image 20230914091814.png]]
I dette tilfælde et 5. ordens filter
#filtre #filteroverføringsfunktioner #signalbehandling 


