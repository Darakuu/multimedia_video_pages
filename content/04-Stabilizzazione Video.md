---
tags:
  - Multimedia/Video
---
# Stabilizzazione

Un sistema di stabilizzazione dell'immagine ha come scopo quello di attenuare i movimento della camera da una sequenza di immagini:
- Padding: movimenti intenzionali, da mantenere nel video;
- **Jitter**: movimenti non intenzionali, da eliminare.
 
Esistono dei sistemi di stabilizzazione analogici, come accelerometri, giroscopi, ammortizzatori meccanici, etc... 

Noi analizziamo sistemi di stabilizzazione digitali.
## Sistemi di Stabilizzazione Digitale

Un esempio, dove la linea rettilinea indica che la sequenza di frame è stabile, mentre quella curva indica una sequenza stabile:

![[04-Stabilizzazione Video-20240117131850459.png]]

- Individuo la tipologia di jitter presente nella sequenza di frame scegliendo un **punto di riferimento**.
- "Sposto" il video in maniera opposta al jitter, in modo da contrastarlo.
- Questo processo mi farà perdere dettagli sui bordi (indicato dalle bande nere nell'esempio), quindi poi eseguo un crop al video, ed infine un'interpolazione.
 

I sistemi di Digital Image Stabilization possono essere real-time, o post-processing (offline).
 
Abbiamo tre fasi:

### Fase 1: Stima del Movimento

Si esegue dapprima la [[03-Stima Movimento|stima del movimento]], usando algoritmi di block matching o features extraction. 

### Fase 2: Filtraggio del Movimento

Filtraggio, o correzione. 

L'idea di base è di usare i metodi della fase 1 per stimare dei motion vector locali (LMV) affidabili, per ogni blocco. 

Dato che è la camera che 'jittera', torna utile calcolare il motion vector globale (GMV).
- Il GMV può essere calcolato a partire dai LMV;
- Chiamiamo il GMV dell'**Anchor Frame** $V_{act}(n)$.


Se si suppone che la camera debba restare immobile la stabilizzazione risulta piuttosto semplice: infatti, si possono tracciare uno o più punti e applicare le trasformazioni inverse al GMV in modo che tali punti (e tutti gli altri) vengano riportati sempre nella stessa posizione. 

Se invece la camera si muove, dobbiamo distinguere i movimenti intenzionali (padding) da quelli casuali o involontari (jitter). 

Vediamo tre algoritmi:
- FPS: Frame Position Smoothing, un algoritmo offline;
- MVI: Motion Vector Integration, un algoritmo online;
- Filtro Kalman: Riesce a predire dove un oggetto sarà arrivato avendo l'inizio, utile per gestire occlusioni. Di fatto è un filtro ricorsivo che valuta lo stato di un sistema dinamico a partire da una serie di misure soggette a rumore.

#### Frame Position Smoothing (FPS)

Idea di base per calcolare il MV correttore: 


- $\Large V_{c}(n)=X_{lpf(n)}-X_{act(n)}$
- $\large X_{act}(n):$ posizione in cui si trova il punto di interesse al frame $n$, cioè la posizione effettiva (*actual*);
- $\large X_{lpf}:$ posizione corretta (stimata), ottenuta:
	- Usando la **trasformata di Fourier** sul segnale costituito dalla variazione delle coordinate di un punto rispetto al tempo;
	- applicando un filtro passa basso, e infine;
	- tornando al dominio temporale.
	- Di fatto dove sarebbe stato il frame senza il movimento involontario.

![[04-Stabilizzazione Video-20240117133305152.png|384]]

Passare dal dominio temporale al dominio delle frequenze ha lo svantaggio di richiedere un'elaborazione **offline**. 
FPS può essere utilizzato online, a patto che venga introdotto un buffer di delay. La formula, ad esempio, diventa:

- $\Large V_{c}(n) = X_{lpf}(n+25)-X_{act}(n)$

#### Motion Vector Integration (MVI)

Tecnica di stabilizzazione real time, l'idea è di "integrare", cioè stimare un Motion Vector che rappresenterà la variazione di movimento rispetto al target frame.
- $\Large V_{int}(n)=\delta \cdot V_{int}(n-1)+V_{act}(n)$
	- $0<\delta \leq 1$ è il **damping factor**, ossia il fattore di smorzamento, pesa il grado di casualità del movimento presente (valori comuni: $[0.875,0.995]$);
	- $V_{int}(n)$ è il motion vector che vogliamo stimare al frame n;
	- $V_{act}(n)$ è il vettore che indica il movimento del punto di interesse tra il frame $n$ e $n-1$.

Un $\delta=0$ indica che tutti i movimenti sono involontari. $\delta$ non varia durante l'esecuzione dell'algoritmo.

MVI si basa sulle seguenti relazioni:

- Ridefiniamo $V_{act}(n)$ rispetto al punto X:
	- $V_{act}(n) = V_{initial}(n)-V_{initial}(n-1)$
- Rispetto alla posizione iniziale, X dovrebbe trovarsi nella posizione corretta:
	- $X_{c}(n)= X_{initial}(n)-V_{int}(n)$ nell'anchor-frame;
	- $X_{c}(n-1) = V_{initial}(n-1)-V_{int}(n-1)$ nel target frame;
- Infine, definiamo il vettore di correzione:
	- $V_{c}(n)=X_{c}(n)-X_{c}(n-1)=V_{act}(n)-V_{int}(n)+V_{int}(n-1)$

Il vettore di correzione corregge il movimento, mentre i vettori di integrazione correggono la posizione. 

Le $X_{initial}$ potrebbero essere errate, dato che stiamo analizzando un video con jitter.


> [!example] Esempio

![[04-Stabilizzazione Video-20240117135951375.png|384]]

#### Filtro di Kalman (Cenni)

### Fase 3: Post-Processing