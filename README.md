# Jet HR – Proiezione Netto (Product Builder Task)

Prototipo di calcolatore stipendio: partendo da una RAL lorda annuale, simula il netto (mensile e annuale) e mostra il dettaglio di tutte le trattenute, con logiche semplificate per un dipendente a tempo indeterminato residente a Milano, anno fiscale 2024.

## Cosa fa

- Input: RAL lorda annuale + numero di mensilità (13/14)
- Output: netto mensile, netto annuale, dettaglio trattenute (INPS, IRPEF lorda, detrazioni, addizionale regionale Lombardia, addizionale comunale Milano)
- Un pannello "Jet AI Insight" con un suggerimento testuale legato alla fascia di reddito

## Semplificazioni assunte

- Dipendente a tempo indeterminato
- Residenza fiscale a Milano
- Nessuna agevolazione fiscale particolare (no detrazioni per carichi familiari, no regimi agevolati, no welfare aziendale già in essere)

## Logiche fiscali implementate (2024)

- INPS: 9,19% sulla RAL
- IRPEF: 3 scaglioni (23% fino a 28.000€, 35% fino a 50.000€, 43% oltre)
- Detrazioni lavoro dipendente: formula a scaglioni ex art. 13 TUIR
- Addizionale regionale Lombardia: aliquote progressive per scaglioni (1,23% / 1,58% / 1,72% / 1,73%)
- Addizionale comunale Milano: 0,8%, con esenzione totale per imponibile fino a 23.000€

## Prossimi step (fuori scope per questo prototipo)

Il pannello "Jet AI Insight" oggi usa una logica a regole (if/else su fasce di RAL), scelta deliberatamente per restare un output deterministico e verificabile in ogni suo passaggio.

Uno sviluppo naturale sarebbe sostituirlo con una chiamata a un modello linguistico specializzato, per generare suggerimenti realmente dinamici e personalizzati sul singolo caso (es. combinazioni di welfare, fringe benefit, timing di eventuali bonus). Questo richiederebbe però:

- un backend/proxy (es. Cloudflare Worker o Vercel Function) per non esporre la API key lato client, dato che l'app è oggi statica
- gestione di errori/latenza/costi per chiamata
- test per evitare che il modello generi consigli fiscalmente scorretti (serve comunque un livello di validazione sopra l'output del modello)

Per un prototipo che deve dimostrare comprensione e controllo delle logiche di business, la versione a regole è la scelta corretta; l'integrazione AI resta un'estensione valida per una versione di prodotto più matura.
