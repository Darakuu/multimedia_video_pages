---
tags:
  - Multimedia/Video
---

> [!def] Formato Video
> Con formati video ci si riferisce ai metodi standard di codifica, memorizzazione e riproduzione utilizzati nei dispositivi video. 

Uno Standard video include informazioni su:
- Connettori fisici: numero di canali e tipo di dati da essi trasmessi;
- Display: spazio di colori utilizzato, risoluzione, refresh rate.
 
Si distinguono due formati: Analogico e Digitale. 

# Formati TV Analogici

Per l'**acquisizione** e il **display** del segnale video tutti i sistemi usano RGB (o XYZ). 

$$
\begin{align}
\begin{bmatrix}
X \\
Y \\
Y \\

\end{bmatrix} = \begin{bmatrix}
2.365 &-0.515 &0.005 \\
-0.897 & 1.426 & -0.014 \\
-0.468 & 0.089 & 1.009
\end{bmatrix} \begin{bmatrix}
R \\
G \\
B
\end{bmatrix}
\end{align}
$$

Per la trasmissione si usa uno spazio di coordinate luminanza/crominanza (YUV), **perché richiede una larghezza di banda minore**.
$$\begin{align}
& Y = 0.3R+0.6G+0.1B \\
& U = (K_{u})(B-Y) \\
& V = (K_{v})(R-Y)
\end{align}$$
## NTSC

National Television Systems Committee.

| Caratteristiche NTSC | Valori |
| ---- | ---- |
| Scan-lines | 525 (480 visibili) interlacing 2:1 |
| Line Rate | 15750 Hz |
| Frequenza di semiquadro | 60 Hz (60 semiquadri al secondo, **27,97** FPS $\iff$ Hz per quadro) |
| Formato delle immagini | 4:3 o 16:9 |
| Spazio di Colore | **YIQ** |
| Scansione Immagine | Orizzontale da in alto a sinistra a in basso a destra |
| Sincronismo colore | 3,58 MHz (sottoportante di crominanza) |
| Modulazione | **QAM** (Quadrature Amplitude Modulation) |

### Rappresentazione del Colore YIQ

La crominanza è rappresentata tramite:

- I: In-Phase;
- Q: Quadrature-Phase.

$$
\begin{flalign}
& I = 0.60R - 0.32G - 0.28B \\
& Q= 0.21R - 0.52G +0.31B
\end{flalign}
$$
I e Q hanno la stessa frequenza ma con una differenza di fase di 90°. 

Si applica una modulazione in ampiezza di sottoportante (ASMC). 



### Problemi di trasmissione

### Vantaggi e Svantaggi

#### Vantaggi

#### Svantaggi

## PAL

Phase Alternating Line

### Rappresentazione del Colore
 

### Vantaggi e Svantaggi

#### Vantaggi

#### Svantaggi

## SECAM

### Versioni

### Rappresentazione del Colore e Trasmissione

### Vantaggi e Svantaggi

#### Vantaggi

#### Svantaggi

## Riassumendo...

# Formati TV Digitali

## ATSC

### Standard di compressione compatibili

## DVB-T

### Caratteristiche Principali

## ISDB-T

## DTMB