---
tags:
  - Multimedia/Video
---
# H.264

## Premessa

Formato di compressione video rilasciato nel 2003, noto anche come (MPEG-4) AVC (Advanced Video Coding), o parte 10 del sottostandard di MPEG-4. 

Applica un metodo di compressione lossy, anche se è possibile rendere talmente impercettibile la perdita da considerarlo lossless. 

## Miglioramenti

- Miglioramento della codifica entropica (tipo Huffman), tramite una codifica a lunghezza variabile;
- Applicazione della trasformata DCT su blocchi più piccoli
- Miglioramenti relativi alla valutazione e alla compensazione del movimento;
- Filtro di ricostruzione nella fase di decodifica per ridurre l'effetto di blocchettizzazione.

## Codifica VLC (Variable Length Encoding)

I simboli che rappresentano i parametri relativi ai modi di codifica e predizione, i motion vectors e i coefficienti della trasformata vengono codificati con VLC, codici a lunghezza variabile. 

- VLC è basata su tabelle di assegnazione da trasmettere insieme ai frame;
- VLC sfrutta le sequenze di zero, +1 e -1, e la correlazione fra il numero di coefficienti non nulli di un blocco e quello nei blocchi adiacenti.

## Blocchi e Macroblocchi

I **blocchi** sono costituiti da **4x4** pixel. La dimensione dei blocchi è quindi ridotta a $\dfrac{1}{4}$ rispetto a MPEG-2. 

I **macroblocchi** hanno una dimensione di 16x16 campioni (pixel) per la luminanza, e 8x8 campioni per ciascuna delle due componenti della crominanza (spazio di colori: YCbCr). 


> [!warning] Dimensione minima blocco
> La dimensione minima di un blocco è **4x4**. 2x2, ad esempio, non è una dimensione valid

## Slice

I macroblocchi sono raggruppati in **slices**: uno slice è un sottoinsieme di un'immagine decodificabile indipendentemente dalle altre. 

L'ordine di trasmissione delle slice (e quindi dei macroblocchi) non è necessariamente quello originario dell'immagine, ma è invece indicato dal codificatore in una mappa apposita: la <ins>Macroblock Allocation Map</ins>. 

Sono definiti 5 differenti tipi di slice:

I primi tre sono analoghi ai precedenti formati MPEG: I/P/B-Frames. Le predizioni sono ottenute a partire dalle slice precedentemente codificate. 
 

Se le slice sono tutte di tipo I, è come se fosse un "reset" delle dipendenze. Non dipendiamo più da slice precedenti.

> [!NOTE] Nota:
> In H.264 più slice possono essere utilizzate per le predizioni, e pertanto encoder e decoder memorizzano le slice utilizzate per le predizioni in una apposita memoria (multipicture buffer), e il controllo per la gestione del buffer è specificato nel flusso dati.
> 
> 
> Precedendemente, si poteva fare riferimento al più ad altri 2 frame.
>

Inoltre, H.264 definisce due ulteriori tipi di slice, denominati SI (Switching I) e SP (Switching P), che consentono un'efficiente commutazione tra flussi di dati a bit-rate differente, senza rinunciare al massimo sfruttamento della ridondanza temporale. 

Ad esempio, nello streaming via internet spesso lo stesso video è codificato a bitrate differenti, e il decoder tenta di accedere al flusso dati con bitrate più elevato possibile, ma nel caso in cui le condizioni del canale non lo permettono, commuta al flusso con bit-rate più basso. 
 
  

#### Funzionamento SP
![[05-Compressione Video-20240112000853729.png|512]]
 

Ogni SP è unico per $n$ flussi.
## Codifica Intra

Nella codifica intra è sfruttata solo la correlazione spaziale all'interno dello stesso macroblocco. 

Per aumentare l'efficienza vengono codificate le differenze fra i pixel del macroblocco e i pixel precedentemente codificati, tipicamente quelli posizionati sopra a sinistra. 

Insomma, osservo le relazioni che ci sono nei pixel nel macroblocco.  

Di solito, non c'è correlazione tra blocchi nello stesso macroblocco. In ogni caso, stiamo ragionando a pixel nella codifica intra, e non a blocchi.

## Codifica Inter
 

Nella codifica inter si sfrutta invece la correlazione **temporale** fra uno o due frame precedentemente codificati. 

La predizione può essere ottenuta mediante una stima ed una compensazione del movimento (motion compensated prediction).

### Tree Structured Motion Compensation
 

A differenza degli standard precedenti, la dimensione del blocco su cui si effettua la predizione può variare da 16x16 fino a 4x4. 

La Tree Structured Motion Compensation è la segmentazione dei macroblocchi (di luminanza) al fine della compensazione del movimento. 

Prevede 4 modi di segmentazione: 16x16 (0 segmentazioni), 16x8 (segmentazione orizzontale), 8x16 (verticale), oppure 8x8. 

Se viene scelta la modalità 8x8, ciascuna delle 4 partizioni così ottenute può essere ulteriormente suddivisa in sottopartizioni, nello stesso modo. (andando così ad ottenere un albero...)

![[05-Compressione Video-20240112003924176.png|512]]

Le molteplici scelte hanno implicazioni differenti sul numero di bit necessario a codificare i motion vectors e le differenze residue. 

In genere, dimensioni elevate del blocco sono convenienti in aree piatte, mentre in aree ricche di dettagli si può trarre vantaggio dall'uso di aree ridotte.
## Trasformata DCT
 
Il tipo di trasformata è la DCT, leggermente modificato affinché le operazioni richiedano somme e scalamenti effettuabili con numeri interi a 16 bit in modo da non avere perdita di precisione effetuando la trasformazione diretta seguita da quella inversa.

## Quantizzazione
 
Esistono 52 opzioni di quantizzazione (fattore di scala), e questa ampia gamma di valori permette all'encoder di raggiungere il miglior compromesso fra qualità e bitrate: 

- 0 è lossless;
- 23 è il valore di default;
- 51 è il valore peggiore possibile, totalmente lossy.
 

I valori accettabili sono nel range **18-28**, e possiamo anche considerare il valore 18 come un valore visivamente senza perdita, o quasi.

## Filtro Anti-Blocchettizzazione

L'effetto di **blocchettizzazione** è uno dei degradamenti caratteristici delle tecniche di compressione che operano su blocchi: è particolarmente visibile, fastidioso e inoltre potrebbe interferire con algoritmi di edge-detection. 

H.264 introduce un filtro apposito che è applicato prima della trasformata inversa sia nell'encoder, che nell'encoder. 

Si ottengono due principali vantaggi:
- Una minore visibilità dei bordi dei blocchi;
- Una migliore predizione inter con compensazione del movimento.

## Applicazioni

H.264 trova spazio in differenti scenari, soprattutto grazie alla possibilità di aumentare il bit-rate:
- HDTV;
- Web Streaming in HD;
- Blu-Ray Disk