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


$$

\begin{align}
& Y = 0.3R+0.6G+0.1B \\
& U = (K_{u})(B-Y) \\
& V = (K_{v})(R-Y)
\end{align}

$$
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

Il segnale ricevuto deve essere demodulato, cioè bisogna scomporre le componenti che sono state multiplexate insieme. Alcuni range di frequenze infatti sono sovrapposti:
- Cross-Color;
- Cross-Luminance.
Notiamo infatti dei fenomeni di *cross-talk*.

![[01-Formati Video-20240117170818711.png|512]]

### Vantaggi e Svantaggi

#### Vantaggi

- Non è richiesto il cambiamento di fase (dato che è già presente uno sfasamento di 90°), che semplifica la realizzazione di circuiti;
- Fa un uso ottimale della larghezza di banda per la crominanza, riservando la maggiorparte di questa per i colori che l'occhio umano percepisce meglio.
#### Svantaggi

- Nel caso di errori nei colori ed eventuale correzione, il processo di sync tra le due sottoportanti diviene complesso.

è proprio questo svantaggio dell'**instabilità cromatica** (e anche motivi politici) che porta allo sviluppo degli altri standard seguenti.

## PAL

Phase Alternating Line

|Caratteristiche PAL |Valori|
|---|---|
|Scan-lines|625, interlacing 2:1 |
|Line Rate|15625 Hz |
|Frequenza di semiquadro|50 Hz (50 semiquadri al secondo, **25** FPS Hz per quadro) |
|Formato delle immagini|4:3 o 16:9|
|Spazio di Colore|**YUV** |
|Scansione Immagine|Orizzontale da in alto a sinistra a in basso a destra|
|Sincronismo colore|4.43 MHz (sottoportante di crominanza) |
|Modulazione|**QAM** (Quadrature Amplitude Modulation)|

### Rappresentazione del Colore
 
Sistema di modulazione simile a NTSC (a parte la diversa frequenza della sottoportante della crominanza), tuttavia ad ogni riga (alternandosi) il segnale V ha uno sfasamento di 180°

- Questo risolve i problemi di instabilità cromatica NTSC, ma;
- richiede una sync per distinguere la "PAL Line" dalla "NTSC Line"

![[01-Formati Video-20240117171307407 1.png]]
### Vantaggi e Svantaggi

#### Vantaggi

- L'errore di fase che causa distorsioni cromatiche è automaticamente eliminato;

#### Svantaggi

- Nel sistema PAL sono necessari la commutazione elettronica della fase e l'identificazione del segnale, che rende più difficile e costosa la progettazione dei circuiti.

## SECAM

SÉquentiel Couleur À Mémoire.

| Caratteristiche SECAM | Valori |
| ---- | ---- |
| Scan-lines | 625, interlacing 2:1 |
| Line Rate | 15625 Hz |
| Frequenza di semiquadro | 50 Hz (50 semiquadri al secondo, **25** FPS Hz per quadro) |
| Formato delle immagini | 4:3 o 16:9 |
| Spazio di Colore | **YDbDr** |
| Scansione Immagine | Orizzontale da in alto a sinistra a in basso a destra |
| Sincronismo colore | 4.43 MHz (sottoportante di crominanza) |
| Modulazione | **FM** (Frequency Modulation) |
### Versioni

- SECAM $\mathtt{I}$, 1961
- SECAM $\mathtt{II}$, SECAM $\mathtt{III}$(A,B),
- SECAM $\mathtt{IV}$, $\mathtt{V}$, o noto anche come NIR-SECAM, per l'unione sovietica. 
### Rappresentazione del Colore e Trasmissione

- Si usa lo spazio di colore YDbDr:

$$
\begin{align}
& D_{b}=3.059U \\
& D_{r}=-2.169V
\end{align}
$$
- E si applica una modulazione sulla **frequenza**
- La differenza principale tra NTSC/PAL e SECAM è la seguente:
	- Ogni linea contiene **solo uno** dei due segnali della crominanza Db o Dr, in maniera alternata.

### Vantaggi e Svantaggi

#### Vantaggi

- La modulazione in frequenza con segnali di crominanza alternati è più resistente ai rumori (no cross-color/luminance);
- L'informazione cromatica mancante dalla linea precedente è ripristinata con un buffer chiamato **Delay Line**, da cui il nome "sequenziale con memoria"

#### Svantaggi

- È necessaria l'identificazione del segnale per distinguere le linee che contengono il segnale Db da quelle che contengono Dr;
- Poiché c'è solo una sottoportante per ogni linea del segnale cromatico anziché due, si perde metà dell'informazione sul colore, quindi la risoluzione verticale originale del colore è dimezzata

# Formati TV Digitali

## ATSC

### Standard di compressione compatibili

Prevede diverse modalità di funzionamento relative al framerate, alla risoluzione, agli standard di compressione compatibili ([[05-Compressione Video#MPEG-2|MPEG-2]] ,[[H.264]]) e retrocompatibilità con i formati analogici. 

Nonostante H.264 consenta formati di qualità visiva più elevata, la maggiorparte delle TV in commercio contiene solamente codec MPEG-2.

## DVB-T

Standard europeo per la TV digitale, pubblicato nel 1997. 

### Caratteristiche Principali
 

Permette la trasmissione di una grande quantità di dati garantendo alta definizione, successore di PAL/SECAM. 

Utilizza i codec MPEG-2 o H.264. 

- Come sistema di trasmissione, usa *Orthogonal Frequency Division Multiplexing* (**OFDM**).
	- Sistema di multiplexing multi-portante, in cui le sottoportanti sono tra loro ortogonali.
	- Buona resa anche in condizioni non ottimali del canale.
	- Garantisce un'attenuazione costante e dunque stimabile e correggibile.

![[01-Formati Video-20240117173430652.png]]


## ISDB-T, DTMB

Standard simili al DVB-T.
- Il primo è diffuso in Giappone e sud-America,
- il secondo in Cina.