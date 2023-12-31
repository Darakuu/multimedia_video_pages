---
tags:
  - Multimedia/Video
---
1. Quale tra i seguenti è un vantaggio dello standard PAL Rispetto a NTSC?
	- [ ] Risolve il problema dell'instabilità luminosa di NTSC alternando uno sfasamendo del segnale di luminanza Y
	- [ ] Risolve il problema dell'instabilità cromatica di NTSC alternando uno sfasamendo del segnale di crominanza U
	- [x] Risolve il problema dell'instabilità cromatica di NTSC alternando uno sfasamendo del segnale di crominanza V 
	- [ ] Nessuna risposta è corretta 

2. Quale tra i seguenti sistemi d iregistrazione su nastro magnetico garantisce una migliore larghezza di banda?
	- [x] Sistema elicoidale
	- [ ] Sistema trasversale
	- [ ] Sistema Longitudinale
	- [ ] Nessuna delle altre risposte. 

3. Cosa si intende con Dolly, quando si parla di modelli di movimento di una telecamera?
	- [ ] Una variazione della focale della camera
	- [ ] Una rotazione della camera attorno all'asse perpendicolare al piano di formazione dell'immagine
	- [x] Una traslazione della camera lungo l'asse perpendicolare al piano di formazione dell'immagine.
	- [ ] Nessuna è corretta. 

4. Quale delle seguenti affermazioni sul modello di movimento a 4 parametri è $\textcolor{red}{\text{falsa}}$?
	- [ ] Viene anche chiamato geometric mapping
	- [ ] Non permette le rotazioni attorno ad assi arbitrari
	- [x] Permette anche track, boom e dolly   (non permette dolly)
	- [ ] Permette anche lo zoom 

5. Quale tra le seguenti affermazioni sull'algoritmo di Block Matching Three-Step Search è l'unica vera?
	- [ ] I passi di ricerca sono esattamente 3
	- [ ] Ci dà la certezza di trovare il blocco con il più basso errore DFD tra tutti quelli all'interno della regione di ricerca
	- [ ] È veloce perché lavora solo su punti chiave estratti tramite FAST
	- [x] Nessuna è corretta.   

6. Gli algoritmi di stabilizzazione FPS e MVI possono essere usati per stabilizzare un video in real-time?
	- [ ] No, entrami possono essere utilizzati solo quando si ha a disposizione l'intero video offline
	- [ ] Sì, entrambi nascono per stabilizzare video in real time senza richiedere accorgimenti particolari
	- [x] Sì, entrambi possono essere usati per stabilizzare video in real-time, ma FPS richiede un buffer di delay  
	- [ ] Sì, entrambi possono essere usati per stabilizzare video in real-time, ma MVI richiede un buffer di delay 

7. Quale delle seguenti affermazioni sugli algoritmi di stabilizzazione digitale è l'unica $\textcolor{red}{\text{falsa}}$?
	- [ ] Si articolano di norma in tre fasi: stima del movimento, filtraggio del movimento, e correzione delle distorsioni
	- [ ] Uno dei problemi principali è quello di distinguere il jitter dal padding
	- [ ] Obbligano spesso a effettuare dei crop dei frame video che devono poi essere gestiti
	- [x] In generale funzionano peggio quando la telecamera è fissa   

8. Data la sequenza di frame I B B I B P, chiamati rispettivamente $f_{1},f_{2},f_{3},f_{4},f_{5},f_{6}$ qual è l'ordine in cui questi possono essere codificati? I, B e P indicano la tipologia di frame.
	- [x] $f_{1},f_{4},f_{2},f_{3},f_{6},f_{5}$
	- [ ] $f_{1},f_{3},f_{2},f_{4},f_{6},f_{5}$
	- [ ] $f_{2},f_{3},f_{1},f_{4},f_{5},f_{6}$
	- [ ] $f_{1},f_{4},f_{2},f_{3},f_{5},f_{6}$ 

9. Quale delle seguenti affermazioni sull'algoritmo di compressione H.264 è l'unica $\textcolor{red}{\text{falsa}}$?
	- [ ] Prevede l'utilizzo di slice che sono suddivise in macroblocchi.
	- [x] I macroblocchi 16x16 possono essere suddivisi fino a blocchi 2x2, secondi diverse configurazioni   (fino a 4x4)
	- [ ] Prevede delle slice che possono essere di 5 tipi: I, P, B, SI, SP
	- [ ] Prevede 52 opzioni di quantizzazione. 

10. Quali di questi artefatti video può essere causati dalla compressione MPEG-2
	- [x] Mosquito Noise  
	- [ ] DV Head Clog
	- [ ] DV Drop Out
	- [ ] AC Beat
