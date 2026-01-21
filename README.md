# QUICK SORT VISUALIZATION

## 🏗️ 1. Struttura e Grafica (HTML/CSS)

* **Flexbox Container:** Il `#array-container` usa `display: flex` e `align-items: flex-end`. Questo è cruciale per far sembrare le barre appoggiate sul fondo, anche se l'altezza cambia.
* **Barre Dinamiche:** Le barre sono `<div>` generati via JS.
* **Altezza:** `style.height` determina l'aspetto visivo.
* **Testo:** `innerText` mostra il numero alla base (centrato grazie a flexbox interno alla barra).
* **Larghezza:** Calcolata come `100 / numBars %` per adattarsi allo schermo.



## 🎵 2. Motore Audio (Web Audio API)

Il suono viene generato in tempo reale per evitare file esterni e latenza.

* **Oscillatore:** Crea un'onda sinusoidale (`type = 'sine'`).
* **Frequenza:** Calcolata come `200 + (valore * 2)`. Barre più alte = Suoni più acuti.
* **Anti-Distorsione (Envelope):** Per evitare il suono "gracchiante" (clipping), il volume non è costante:
1. **Attack (0ms -> 10ms):** Il volume sale da 0 a 0.05 (fade-in rapido).
2. **Release (10ms -> 100ms):** Il volume scende esponenzialmente a 0.
*Questo crea un effetto "campana" morbido invece di un "click" digitale.*



## ⚡ 3. Algoritmo Quick Sort (Logica JS)

L'algoritmo è **ricorsivo** e segue la strategia *Divide et Impera*.

### A. Funzione `partition(start, end)`

È il cuore dell'animazione:

1. **Scelta Pivot (Giallo):** Prende l'ultimo elemento (`bars[end]`) come riferimento.
2. **Scansione (Rosso):** Cicla da `start` a `end`.
* Confronta ogni elemento con il Pivot.
* Se l'elemento è minore del Pivot, lo scambia con l'elemento all'indice `i` (zona dei numeri piccoli).


3. **Posizionamento Pivot (Verde):** Alla fine, il Pivot viene messo tra i numeri piccoli e quelli grandi. **Quella è la sua posizione definitiva.**

### B. Funzione `quickSort(start, end)`

Gestisce la ricorsione:

1. Chiama `partition` per trovare l'indice di divisione.
2. Chiama se stessa sulla parte sinistra (numeri minori del pivot).
3. Chiama se stessa sulla parte destra (numeri maggiori del pivot).

### C. Gestione `async/await`

* Ogni scambio o confronto è seguito da `await sleep(ms)`.
* Senza questo, il browser eseguirebbe tutto il calcolo in un istante e vedresti solo l'array finale già ordinato senza animazione.
