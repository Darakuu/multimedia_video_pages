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



### Modello a 4 parametri

### Modello a 6 parametri

## Rappresentazione del Movimento

# Criteri di Stima del Movimento

## Displaced Frame Difference (DFD)

## Block Matching Algorithm (BMA)

### BMA Esaustivo (EBMA)

### Three-Step Search


> [!warning] RISPOSTA DOMANDA ESAME❗ :

$L=\log_{2}R_{0}+1$ formula fondamentale da ricordare.

## Features from Accelerated Segment Test (FAST)

### High-Speed Test

## Perché Stimare il movimento?