---
tags:
  - Multimedia/Video
---
# Stima del Movimento

# Telecamera

Siano:
- F: Lunghezza Focale;
- C: centro focale;
- Z: Profondità
## Prospettica

Assumiamo che:
- L'origine del sistema di coordinate 3D globale sia localizzata in C;
- Il piano XY sia parallelo al piano xy (nel sistema di coordinate dell'immagine);
- Il sistema di riferimento globale e quello dell'immagine usino la stessa unità di misura.

Sistema con Prospettiva: la dimensione di un'oggetto sull'immagine è inversamente proporzionale alla sua distanza.

![[03-Stima Movimento-20240117184241159.png|384]]

$x,y$ piccole rappresentano la posizione della proiezione 2D,
$X,Y,Z$ coordinate nel mondo reale 3D. 


Se la focale F della camera diminuisce, il piano si avvicina a C, e il punto proiettato in 2D si sposta. 

Se aumenta C:
- Il piano si allontana;
- L'oggetto si avvicina.

### Proiezioni Prospettiche

Basate su proporzioni.

- $\dfrac{x}{F}=\dfrac{X}{Z}$ 
- 
- $\dfrac{y}{F}=\dfrac{Y}{Z}$ 
- 
- $x=F\cdot \dfrac{X}{Z}$ 
- 
- $y=F\cdot \dfrac{Y}{Z}$ 

  

## Ortografica

Assumiamo che gli oggetti da rappresentare nell'immagine siano a distanza (Z) molto grande. 

In Ortografia, la dimensione di un oggetto sull'immagine è indipendente dalla sua distanza.

Le proiezioni sono molto semplici:
- $x = X$
- $y = Y$

Dato che non tengo conto della profondità, non mi interessa neanche la focale.

### Note sulle proiezioni

**Invertibilità:** Sia le proiezioni prospettiche che quelle ortografiche stabiliscono una relazione molti-a-uno.
- Per invertire il processo e ricostruire una scena 3D partendo da un'immagine 2D ho bisogno di informazioni aggiuntiva (z-mapping, stereoscopia...);
- Insomma, perdendo la Z, il processo non è facilmente invertibile (al più posso stimare la distanza con regressione).

**Occlusione:** Nell'immagine compaiono solo gli oggetti che intercettano per primi le linee di visioni che partono dal centro focale C, ovviamente.

### Modello CAHV

- $C$ : Centro focale;
- $A$ : Versore Z;
- $H_{0}$ : Versore X;
- $V_{0}$ : Versore Y

Permette una visualizzazione più comoda del sistema di riferimento della videocamera se questa è in movimento, e inoltre, può descrivere un piano dell'immagine non allineato al sistema di riferimento della videocamera (**distorsione del sistema ottico**).

![[03-Stima Movimento-20240117191225297.png|512]]

Dalle formule sulle proiezioni prospettiche, ricaviamo:

$p=\displaystyle\binom{x}{y}=\dfrac{F}{A^T\cdot (P-C)}\cdot \binom{H_{0}^T\cdot (P-C)}{V_{0}^T\cdot (P-C)}$

Dove:

- $P-C$ è la traslazione dall'origine;
- I versori A,H,V sono trasposti perché normalmente troviamo i vettori in colonna, qui li rappresentiamo in riga.

Essenzialmente questo modello applica un cambio di sistema di riferimento, dato che si ha una traslazione dell'origine.

# Movimenti

## Spostamenti in 3D e 2D

![[03-Stima Movimento-20240117192511672.png]]

Siano:
- Posizione iniziale a $t_{1}:$
	- $X = [X,Y,Z]^T$
	   

	- $x=[x,y]^T$
	   

- Posizione finale a $t_{2}:$
	- $X' = [X',Y',Z']^T=[X+D_{X},Y+D_{Y},Z+D_{Z}]^T$
	   

	- $x'=[x',y']^T=[x+d_{x},y+d_{y}]^T$
	   

- Spostamento 3D: $D(X;t_{1},t_{2})=X'-X=[D_{X},D_{Y},D_{Z}]^T$
- Spostamento 2D:  $d(x;t_{1,t_{2}})=x'-x=[d_{x},d_{y}]^T$
- D è il vettore di spostamento, il *displacement*.
### Modelli di movimento in 2D

Quando abbiamo degli istanti $t_{1}$ e $t_{2}$ ben identificati (sempre nei video) allora si può scrivere solo $d(x)$. 

Un altro nome per $d(x)$ displacement è "Vettore di movimento 2D", oppure **Motion Vector** (MV). 

Un'insieme di motion vector per ogni $x$ dell'immagine è detto **Motion Field**.

![[03-Stima Movimento-20240117193222700.png|512]]
 

Esempio di Motion Field.
#### Funzione di mapping

$w(x)=x+d(x)$ 

Ci interessa sapere il movimento di tutti gli elementi della immagine (a seconda della separazione che utilizziamo, pixel, blocchi, etc...).

Ogni pixel contiene un valore diverso da quello iniziale. All'inizio, $d(x)$ potrebbe non essere noto. Di solito infatti si stima un $w'(x)$, perché $w(x)$, cioè il movimento reale, è difficile da stimare correttamente. 

Se ci sono molti elementi $w'(x)\longrightarrow 0$ significa che mi sono avvicinato molto a $w(x)$, e quindi ho stimato correttamente il movimento.

## Movimenti della Telecamera

| Traslazione | Asse Perno | Rotazione |
| :--: | :--: | :--: |
| Tracking | $\textcolor{red}{X}$ | Tilting |
| Booming | $\textcolor{blue}{Y}$ | Panning |
| Dollying | $\textcolor{green}{Z}$ | Rolling |

- Con Z: asse perpendicolare all'immagine (di profondità), e Y: asse altezza.
- Potrebbe non essere immediatamente chiaro nel contesto delle rotazioni: immagina di utilizzare l'asse di rotazione appunto come 'perno' su cui la telecamera ruota.

![[03-Stima Movimento-20240117195242072.png|512]]

> [!warning] Dollying != Zooming

### Tracking, Booming

### Zooming

Zoom($\rho$)

Nell Zooming si conservano le relazioni spaziali

### Tilt, Pan approssimato

### Roll

### Modello a 4 parametri

### Modello a 6 parametri

## Rappresentazione del Movimento

Come rappresentare però i motion field? 

Evitiamo una rappresentazione globale, dato che non funziona bene se nella scene sono presenti più oggetti che si muovono in maniera differente. 

Evitiamo però anche una rappresentazione basata sui singoli pixel che compongono l'immagine, dato che richiede la stima di troppi vettori di movimento. 

I criteri che funzionano sono:
- Rappresentazione basata su regione: segmentiamo l'immagine in regioni con algoritmi di edge detection.
	- Computazionalmente oneroso, potrebbe risultare difficile da generalizzare;
- Rappresentazione basata su **blocchi**:
	- Buon compromesso fra *accuracy* e *complexity*;
	- Problemi di discontinuità solo sul bordo dei blocchi (risolvibile)

Nella rappresentazione basata su blocchi ricordo come si sono spostati i blocchi e la differenza tra la stima effettuata e il movimento reale.

# Criteri di Stima del Movimento

## Displaced Frame Difference (DFD)

Siano: 

- Anchor frame $I_{1}$ a $t_{1}$ il frame iniziale;
- Target Frame $I_{2}$ a $t_{2}$ il frame su cui stimare il relativo movimento:
	- $t_{1}>t_{2}:$ backward motion estimation;
	- $t_{1}<t_{2}:$ forward motion estimation
Il nostro obiettivo sarà minimizzare la differenza. 

Definiamo inoltre una funzione di mapping:
- $w(x;a)=x+d(x;a)$
Dove $a=[a_{1},a_{2},\dots,a_{L}]^T$ sono i parametri di movimento (da stimare!). 

Stiamo essenzialmente tentando di capire che tipo di spostamento è avvenuto.


> [!def] Errore DFD
>$E_{DFD}=\displaystyle\sum_{x \in \Lambda}|I_{2}(w(x;a))-I_{1}(x)|^p$

Dove:
- $\Lambda:$ insieme dei pixel nell'anchor frame $I_{1}$;
- $p:$ intero positivo; casi particolari:
	- $p=1:$ $E_{DFD}$ è detto **mean absolute difference** (MAD)
	- $p=2:$ $E_{DFD}$ è detto **mean squared error** (MSE)
L'errore è calcolato nel frame trasformato e il frame immediatamente prima. 


> [!NOTE] Ragionamento
> Sappiamo che la derivata di una funzione si azzera nei punti di minimo e massimo. Dato che vogliamo minimizzare l'errore, prendiamo la derivata.
> 

Affinchè la stima dei parametri $a$ sia la migliore, si dovra minimizzare $E_{DFD}$ 

- Essendo $a$ un vettore, dovremo in generale imporre che il gradiente $\nabla$ di $E_{DFD}=0$.
- Ad esempio, per $p=2$ (MSE) il gradiente sarà:

$\dfrac{\partial E_{DFD}}{\partial a}=2\displaystyle\sum_{x \in \Lambda}(I_{2}(w(x;a))-I_{1}(x))\dfrac{\partial d(x)}{\partial a}\nabla I_{2}(w(x;a))$

Dove $\dfrac{\partial d(x)}{\partial a}$ è una matrice contenente le derivate parziali di tutti i parametri di movimento, ed è una matrice brutta brutta che vogliamo approssimare (ed analiticamente non si può fare). 



## Block Matching Algorithm (BMA)

Consideriamo la rappresentazione di movimento basata su blocchi.
- I blocchi possono avere qualsiasi forma geometrica, ma per semplicità assumiamo che siano quadrati.
- Devono rispettare le seguenti leggi:
	- $\bigcup_{m \in M}B_{m}=\Lambda$
	- $B_{m} \bigcap B_{n}=\emptyset, m\neq n$
- Cioè l'unione di tutti i blocchi restituisce l'intero frame ( $\Lambda$ ), e l'intersezione di tutti i blocchi restituisce un insieme vuoto (non vi è sovrapposizione tra frame).
- Assumiamo inoltre che tutti i pixel di un blocco $B_{m}$ si muovano nella stessa direzione, con un MV per blocco (modello traslazionale blockwise).
- Dato l'anchor frame(?) $B_{m}$ vogliamo trovare il target frame $B_{m}'$ che minimizza l'errore DFD.

### BMA Esaustivo (EBMA)

Cioè vogliamo minimizzare: 

$E_{m}(d_{m})=\displaystyle\sum_{x \in B_{m}}|I_{2}(x+d_{m})-I_{1}(x)|^p$ 


Per trovare il migliore $d_{m}$ confrontiamo tutti i $d_{m}$ fra l'anchor frame $B_{m}$ e tutti i possibili target frame $B_{m}'$ all'interno di una regione di ricerca. 

Tutto questo processo è molto oneroso computazionalmente. Per ridurre il carico si può usare la Mean Absolute Difference (MAD Error). 

Solitamente si una un passi di ricerca pari a 1 pixel (integer-per-pixel accuracy search.). 

Sia $N\times N$ la dimensione del blocco, e il raggio della regione di ricerca pari a $\pm R$, allora:
- Dovendo fare una sottrazione, un valore assoluto e un'addizione, per ogni blocco ci sono $N^2$ operazioni.
- Numero di operazioni per stimare un MV per blocco: $(2R+1)^2N^2$
- La formula rappresenta tutti i possibili spostamenti di un blocco nella regione di ricerca. Il +1 c'è per gestire il caso in cui rimango fermo.

![[03-Stima Movimento-20240118140011914.png]]

Siano ora $M\times M$ le dimensioni dell'immagine, si avranno $\left( \dfrac{M}{N} \right)^2$ blocchi. 

Avremo quindi $\left( \dfrac{M}{\cancel{ N }} \right)^2\cdot \cancel{ N^2}(2R^2+1)^2$

Il numero totale di operazioni sarà quindi $M^2(2R+1)^2$. 

Questo risultato è interessante perché il carico computazionale è indipendente dalla dimensione dei blocchi. 

Difatti, dipende solo dalla dimensione del frame (dell'immagine), e dalla dimensione della regione di ricerca. 

Resta comunque molto pesante, computazionalmente parlando, quindi serve un metodo più veloce.
### Three-Step Search

Modifichiamo l'EBMA:
- Per trovare il migliore $d_{m}$ confrontiamo i $d_{m}$ fra l'anchor frame $B_{m}$ **e un sottoinsieme** dei possibili target frame $B_{m}'$ all'interno di una regione di ricerca.
- Si inizia con un passo di ricerca $R_{0}$ uguale (o leggermente maggiore) alla metà del raggio di ricerca R;
- Ad ogni passo dell'algoritmo ri riduce il passo di ricerca della metà, finché non sarà pari a 1
- Effettuiamo infine EBMA solo su una ragione molto più piccola (quella probabile).
	- In un intorno di 8 punti, +1 quello in cui mi trovo già.

![[03-Stima Movimento-20240118140859758.png|384]]

- Al primo passo:
	- Si calcola il miglior MV su 9 punti di ricerca entro un raggio di ricerca $R_0$
- Dal secondo passo in poi:
	- Si pone $R_{i+1}=\dfrac{R_{i}}{2}$
	- Si calcola il miglior MV su 8 punti di ricerca entro un raggio di ricerca $R_{i+1}$
	- Se reitera finché $R_{n}=1$

Nota bene: a dispetto del nome, potrebbero esserci più di tre passi di ricerca. In casi particolari potremmo anche non trovare effettivamente il minimo ottimo, ma quanto meno siamo vicini.

> [!warning] RISPOSTA DOMANDA ESAME❗ :
> $L=\log_{2}R_{0}+1$ formula fondamentale da ricordare. 
>
> **Quesito**: Alla fine dell'esecuzione di un'istanza dell'algoritmo di block matching Three-Step-Search si osserva che per un singolo blocco sono stati visitati 73 punti di ricerca. Qual è il passo di ricerca iniziale R0? 
>
> **Procedimento**: 
>
> $L=\log_{2}R_{0}+1$; 
>
> Sappiamo che sono stati visitati 73 punti. In ogni passo di ricerca io visito 8 punti+1, quindi, con $P$ punti di ricerca: 
>
> $P=8L+1$; 
>
> $73=8L+1 \implies L=\dfrac{72}{8}=9$ 
>
> Sostituendo nella formula precedente: 
>
> $9=\log_{2}R_{0}+1$ 
>
> $8=\log_{2}R_{0}$ 
>
> Elevando entrambi i membri, ottengo: 
>
> $\large2^8=\cancel{ 2 }^{\cancel{ \log_{2} }R_{0}}$ 
>
> Che mi restituisce il passo di ricerca iniziale $R_{0}$, quello che stavo cercando. 
>
> $R_{0}=2^8=256$  
>****



## Features from Accelerated Segment Test (FAST)

Algoritmo per estrarre punti chiave "Features from Accelerated Segment Test". 

Individua dei punti salienti (corner) nel frame, da usare come features per tracciare il movimento.
- Si analizza ad ogni passo un insieme di 16 punti con configurazione a cerchio di raggio 3 per classificare se un punto $p$ sia di corner o meno.
- Data l'intensità $l_{p}$ del punto $p$, se per almeno 12 punti contigui con l'intensità $l_{x}$ si ottiene che $|l_{x}-l_{p}|>t$, con $t$ soglia, allora $p$ sarà un punto di corner.
- Quindi, non andiamo a prendere tutti i blocchi, ma individuiamo dei keypoints. 

In altre parole, stiamo confrontando la luminanza del centro con la luminaza dei possibili punti corner. 

Si fanno le differenze in valore assoluto, se almeno **12 punti consecutivi** superano la soglia, allora il punto analizzato ci interessa. 

La soglia $t$ si sceglie arbitrariamente (di solito a seconda di alte differenze percettive). 

Dato un Cerchio di Bresenham di raggio 3:

![[03-Stima Movimento-20240118145050628.png|256]]

Ci devono essere almeno $\dfrac{3}{4}$ punti consecutivi che superano la soglia.

> [!warning] RISPOSTA DOMANDA ESAME❗ :
> Questo punto P è di corner? 
>
>Sì, se ci sono 12 punti consecutivi la cui differenza supera la soglia, altrimenti **no!**
>
>Formula da utilizzare (come sopra):
>
>$|p-'\text{punto da considerare}'|>\text{soglia?}\to \text{si} \to \text{abbiamo 12 'si' consecutivi?}\to \text{allora punto da considerare è di corner}$
>
>Se un qualsiasi passaggio è falso, allora possiamo già escludere il punto.

Inoltre, possiamo semplificare il calcolo: invece di prendere i punti sequenzialmente, eseguiamo il calcolo nei punti che potrebbero interrompere la sequenza consecutiva:

![[03-Stima Movimento-20240118151610323.png|512]]

Un'altra possibile semplificazione è quella di calcolare i punti nell'intorno del primo punto preso in considerazione:

![[03-Stima Movimento-20240118151722904.png|256]]

### High-Speed Test

Questo procedimento di semplificazione si chiama infatti "**High Speed Test**". Formalmente: 

- Verificare $|l_{x}-l_{p}|>t$ per i punti del cerchio in posizioni che potrebbero interrompere la sequenza, ad esempio nei punti 1 e 9, e poi 5 e 13.
- Se per almeno 2 di questi 4 punti il test risulta $l_{x}-l_{p}\leq t$ il punto $p$ non può essere di corner.

FAST + High Speed Test è più veloce di altri metodi, sebbe meno preciso. Questo le rende adatto per applicazioni real time.

## Perché Stimare il movimento?

L'informazione sul movimento della scena torna utile in vari modi:
- [[04-Stabilizzazione Video|Stabilizzazione Video]];
- [[05-Compressione Video|Compressione Video]];
- Ricostruzione della scena 3D a partire dalla proiezione 2D;
- etc...