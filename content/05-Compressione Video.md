---
tags:
  - Multimedia/Video
---
# Formati di Compressione
 
Nel tempo sono emersi vari formati di compressione video, associati a diversi standard: 

- ITU-T Standard:
	- H.261 (1984)
	- H.263, H.263+, H.263++ (1992-2000~)
- Joint ITU-T / MPEG Standard:
	- H.262/MPEG-2 (1994)
	- [[H.264]] (2004)
- MPEG Standard:
	- MPEG-1 (1991)
	- MPEG-4 (1998)

Tratteremo brevemente MPEG-1, 2 e 4, per poi approfondire più in dettaglio H.264.


> [!note] MP3 != MPEG-3
> Nota Bene: il popolare formato MP3 <ins>non è</ins> MPEG-3, che non è mai arrivato ad esistere ed è successivamente stato inglobato in MPEG-4, ma bensì **MPEG-1 Audio Layer III**

# Classificazione dei Frame

Per la compressione video, sfruttiamo la ridondanza temporale innata dei video. Essendo sequenze di immagini, supponiamo che ci siano frame simili tra loro.
## I-Frame

Intra, Indipendent Frames (alias: Key-Frames). 

I fotogrammi sono codificati senza alcun riferimento ad altri fotogrammi. Rappresentano perciò uno "snapshot" della scena in un determinato istante. 

Un I-Frame può essere generato da un encoder per creare un punto di accesso casuale: Ossia permettono ad un decodificatore di avviare il processo di decodifica in maniera corretta, partendo da zero in quella posizione del video. 

Gli encoder inseriscono periodicamente I-Frame in un flusso video proprio per avere dei punti di ancoraggio nel video.

> [!example] Accesso Casuale Video
> In altre parole, avere I-Frame nel mezzo di una sequenza video permette di evitare un accesso sequenziale al video. Per esempio, nei servizi di streaming video, questo rende possibile la scelta di andare avanti e indietro nel video con un click a nostro piacimento.

In genere, gli I-Frame richiedono più bit per essere codificati rispetto ad altri tipi di frame. Sono usati come riferimento per la decodifica di altre immagini nel flusso video.
Si possono usare altri algoritmi di compressione per rappresentare gli I-Frame in maniera più efficiente (come ad esempio la DCT).
## P-Frame

Predicted, Previous-dependent frame. 

Ha una dipendenza temporale da quello che è avvenuto prima nel video: devo aver decodificato tutti i frame precedenti, per poter decodificare un P-Frame. 

Può contenere:
- I dati del fotogramma;
- Gli spostamenti (i [[motion vector]]) rispetto al fotogramma da cui dipende;
- Oppure una combinazione dei due.
In generale dunque, un P-Frame contiene solo le differenze rispetto al frame precedente, e per questo motivo richiede meno bit per la codifica rispetto ad un I-Frame. 
 
In un flusso video, i P-Frames sono tipicamente posizionati in mezzo ad I-Frames. La sequenza inizia con un I-Frame, seguita da una serie di P-Frames.

## B-Frame

Bidirectional Predicted, Bidirectional-dependent frames. 

Possono dipendere anche da frame successivi rispetto alla loro posizione, o in altre parole, dipendono da un intorno di frames.  

Hanno il miglior rapporto di compressione. 

Un B-Frame richiede la precedente decodifica di altri frames prima di essere decodificato. 

Può contenere gli stessi dati di un P-Frame.

Inserire in un fotogramma informazioni che si riferiscono ad un fotogramma successivo è possibile solo **alterando l'ordine** in cui i fotogrammi vengono archiviati all'interno del file video compresso.
 

I B-Frame possono essere posizionati in mezzo a I-Frames e P-Frames.
## Memorizzazione Frame


> [!warning] Interdipendenza Frame
> In generale, evito interdipendenza tra frame.
> Ad esempio, un P-Frame può dipendere da I-Frames o anche da altri P-Frames, ma non da B-Frames.
> Un B-Frame può dipendere sia da P-Frames che I-Frames.

Consideriamo la sequenza di frame (f) con relativi macroblocchi (ma):

![[05-Compressione Video-20240111183614933.webp|512]]

> [!example]- Esempio Memorizzazione (possibile domanda esame):
> - i $\text{ma}$ del f1 sono tutti codificati come Intra-Frame
> - i $\text{ma}$ del f2 cercheranno i blocchi simili nel f1 (I) e nel f4 (P)
> - i $\text{ma}$ del f3 cercheranno i blocchi simili nel f1 (I) e nel f4 (P)
> - i $\text{ma}$ del f4 cercheranno i blocchi simili nel f1 (I)
> - i $\text{ma}$ del f5 cercheranno i blocchi simili nel f4 (P) e nel f7 (P) 
> - i $\text{ma}$ del f6 cercheranno i blocchi simili nel f4 (P) e nel f7 (P)
> - i $\text{ma}$ del f7 cercheranno i blocchi simili nel f4 (P)
> - i $\text{ma}$ del f8 cercheranno i blocchi simili nel f7 (P) e nel f10 (P)
> - i $\text{ma}$ del f9 cercheranno i blocchi simili nel f7 (P) e nel f10 (P)
> - i $\text{ma}$ del f10 cercheranno i blocchi simili nel f7
> - i $\text{ma}$ del f11 cercheranno i blocchi simili nel f10 (P) e nel f13 (I)
> - i $\text{ma}$ del f12 cercheranno i blocchi simili nel f10 (P) e nel f13 (I)
> - i $\text{ma}$ del f13 sono tutti codificati come Intra-Frame. 
>
>
> La sequenza è conclusa.

Ma come fanno i frame B a riferirsi a frame che "devono ancora arrivare" nel flusso video? 

L'Encoder e il decoder processano i frame in ordine diverso da quello iniziale. I frame vengono riordinati per evitare di eseguire "salti" quando incontro B-Frame nel flusso video. 

La sequenza precedente viene infatti così riordinata:
![[05-Compressione Video-20240111184921379.webp|512]]

Come regola generale 'euristica', assolutamente non ufficiale e non verificata: I B-Frame vanno sempre dopo i frame da cui dipendono nel "futuro" nella sequenza iniziale.

In altre parole, sposto "di dietro" ai B-Frames i P-Frames e gli I-Frames.

# MPEG-1

# MPEG-2

# MPEG-4 (cenni)

# H.264

## Premessa

## Miglioramenti

## Codifica VLC

## Blocchi e Macroblocchi

## Slice

## Codifica Intra

## Codifica Inter

### Tree Structured Motion Compensation
## Trasformata DCT

## Quantizzazione

## Filtro Anti-Blocchettizzazione

## Applicazioni