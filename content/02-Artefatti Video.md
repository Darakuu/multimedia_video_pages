---
tags:
  - Multimedia/Video
---
# Artefatti Video
Super WIP

- Dato che trattiamo di segnali, l'errore è inevitabile, sia in fase di generazione del segnale, che di trasmissione.


> [!def] Errore
> Un segnale non previsto che va a sommarsi a quello originale dando vita ad un'informazione non più fedele a quella che effettivamente è stata generata in partenza.


## Errori Analogici

- Registrazione e Riproduzione su nastro magnetico avvengono grazie al principio fisico di induzione elettromagnetica.
	- Alterazioni impreviste di frequenza o ampiezza dell’onda elettromagnetica potrebbero modificare l’informazione originale
- Oppure, difetti o usura del mezzo o nelle parti meccaniche dei dispositivi

### Cause Principali

Difetti non prevedibili: 
- Polvere;
- Usura del nastro; 
- Interferenze elettromagnetiche dovute ai cablaggi; 
- Errate configurazioni del dispositivo. 


Gli errori nei video su nastro magnetico sono generalmente chiamati “drop” e possono interessare sia la luminanza che la crominanza, oltre l’audio
### Video Drop Out

### Tracking Error (Mistracking)

### Head Clog

### Skew Error

### Sync-Loss (roll)

### Tape Crease

### Dot Crawl

### AC Beat (Video Hum)

## Errori Digitali

Su nastri magnetici.
### Cause Principali

A differenza degli errori su supporti per la registrazione analogica, i problemi digitali hanno una natura legata soprattutto alla compressione: 
- Compressione lossless: nessuna perdita di informazione in fase di decompressione; 
- Compressione lossy: perdita di dati originali dopo la compressione

### DV Dropout

### DV Head Clog

### Mosquito noise

- Cause: 
	- Compressione basata su DCT (JPEG o MPEG) 
- Conseguenze: 
	- Sgranatura delle aree ad alto contrasto o che presentano edge complessi -
- Soluzioni:
	- Nessuna efficiente 
	- Cambiare codifica 
	- Diminuire il contrasto (con perdita di qualità)

### Block Noise

### Errori dovuti a Digitalizzazione

I difetti presenti nel video originale potrebbero subire diverse modifiche, dalla correzione all’enfatizzazione. 

I dispositivi di conversione possono tentare di correggere errori di registrazione analogici.
 
Talvolta questo provoca la comparsa di nuovi artefatti. (E.G. "Comete")