---
tags:
  - Multimedia/Video
---
# Formati Video

- A cosa ci si riferisce quando si parla di formati video?
> [!check]- Risposta
 > Un Formato Video è una raccolta di metodi standard di codifica, memorizzazione e riproduzione usati nei dispositivi video.
 > Includono informazioni su:
 > - Connettori fisici (numero di canali e tipo di dati da essi trasmessi)
 > - Display (Color space, risoluzione e refresh rate) 

- Cosa si utilizza per l'acquisizione e il display del segnale video? E per la trasmissione? 
> [!check]- Risposta
> Wip

- In NTSC, cos'è il cross-talk effect? Quando si verifica?
> [!check]- Risposta
> - La diafonia (cross-talk) è un qualsiasi fenomeno mediante il quale un segnale trasmesso su un circuito o un canale di un sistema di trasmissione crea un effetto indesiderato in un altro circuito o canale
> - Si verifica se due circuiti sono vicini (cioè quando è possibile avere sovrapposizione tra i segnali)
> - In NTSC il segnale deve essere <ins>demodulato</ins>, cioè bisogna scomporre le componenti multiplexate insieme; alcuni range di frequenza sono sovrapposti:
>	- Cross-Color
>	- Cross-Luminance
 
- Indicare vantaggi e svantaggi della NTSC 
> [!check]- Risposta
 
- Tentando di leggere un video in formato PAL come se fosse NTSC, cosa succede alla velocità di esecuzione? 
> [!check]- Risposta
 
- Che modulazione usano PAL/NTSC e SECAM?
> [!check]- Risposta 
> PAL NTSC usa modulazione in ampiezza, SECAM usa una modulazione in frequenza 

- Che differenze ci sono tra SECAM e PAL/NTSC? 
> [!check]- Risposta
> 

- Descrivere il Formato Digitale DVB-T. 
> [!check]- Risposta
> 

- Che sistema di registrazione si usa sui nastri magnetici?
> [!check]- Risposta
> Sistema Elicoidale wip 

- Parlare dei Sistemi di Scansione, Progressiva e Interlacciata  
> [!check]- Risposta

- Tramite quale tecnica è possibile ridurre lo sfarfallio nei monitor a tubo catodico? Quale tecnica risulta allo stesso tempo utile nei monitor a cristalli liquidi? 
> [!check]- Risposta
> wip



# Artefatti Video

- Come avviene la **registrazione** e la **riproduzione** su nastro magnetico?
> [!check]- Risposta
> wip
 
- Come vengono chiamati gli errori nei video su nastro magnetico?
> [!check]- Risposta
> wip 

- Quali errori sono dovuti ad una perdita di informazione?
> [!check]- Risposta
> wip 


- Quali sono le tipologia di errore analogico?
> [!check]- Risposta
>  

- Qual è l'errore dovuto all'interferenza tra Luminanza e Crominanza?
> [!check]- Risposta
>  Dot Crawl 

- A cosa sono dovuti gli errori digitali?
> [!check]- Risposta
>  wip
# Stima Movimento Video

- Descrivi le caratteristiche della telecamera prospettica e ortogonale
> [!check]- Risposta
>  

- Cosa si fa per evitare che l'immagine risulti capovolta?
> [!check]- Risposta
>  

- Quali sono i vantaggi del modello CAHV?
> [!check]- Risposta
>  

- Riportare graficamente i motion field tipici rispetto ai seguenti movimenti della camera: Zoom-In, Pan verso destra, Rotazione in senso orario.
> [!check]- Risposta
> wip

- Zoom e Dolly sono gli stessi?
> [!check]- Risposta
>  No, nello zoom si conservano le coordinate spaziali
>  Wip

- Cosa si intende con trasformazione Geometrica?
> [!check]- Risposta
>  

- Che cos'è la DFD?
> [!check]- Risposta
>  

- Descrivi gli algoritmi di stima del movimento basati su Block-Matching:
> [!check]- Risposta
>  big wip

- Descrivi gli algoritmi di stima del movimento basati su Features
> [!check]- Risposta
>  wip

# Stabilizzazione Video

- Qual è lo scopo principale della fase di filtraggio del movimento?
> [!check]- Risposta
>  wip 

- Perché in FPS (Frame Position Smoothing) si confronta la posizione assoluta di un frame (rispetto al primo frame) con quella calcolata applicando un filtro passa basso?
> [!check]- Risposta
>  wip  

- Come si individuano i frame in cui potrebbe essere necessario applicare un filtraggio del movimento?
> [!check]- Risposta
>  Punti ad alta frequenza nel dominio delle frequenze.

 
- Descrivi il filtro di Kalman: funzionamento e fasi di predizione/correzione applicato ad un tracciatore Bayesiano
> [!check]- Risposta
>  wip  


# Compressione Video

- Data la qui presente sequenza di frame memorizzati, etichettare ciascun frame in base all'ordine di codifica:
	-  \[**I**, B, P, B, B, P, B, P, P, B, B, B, **I**, P, **I**, B, **I**, P, B, **I**]
> [!check]- Risposta
>  wip  

- Descrivi le caratteristiche di I-Frame, P-Frame, e B-Frame
> [!check]- Risposta I-Frame
>  wip  

> [!check]- Risposta P-Frame
>  wip  

> [!check]- Risposta B-Frame
>  wip  

- H.264 a cosa serve la Macroblock Allocation Map?
> [!check]- Risposta
>  wip  

- H.264 - Codifica Inter: descrivere la Tree Structured Motion Compensation, specificando tutte le configurazioni possibili
> [!check]- Risposta
>  wip  

- H.264 - Quand'è che non conviene usare una configurazione con molta segmentazione dei macroblocchi?
> [!check]- Risposta
>  wip  
