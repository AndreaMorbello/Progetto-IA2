# Progetto-IA2
Progetto Esame IA2 - Morbello Venezia Dicapua - Università Sapienza di Roma

## Descrizione breve:
Il progetto ha come obiettivo di addestrare un modello di regressione capace di stimare il punteggio ELO di un giocatore data una sua partita di scacchi.
Prende ispirazione dalla serie 'Guess The Elo' del noto youtuber americano 'GothamChess' (youtube.com/@GothamChess).

## Dataset 
**Fonte**: Kaggle
**Link**: https://www.kaggle.com/datasets/datasnaek/chess
Inizialmente il dataset era composto da 20,058 osservazioni e 16 features, fra cui *white_rating* scelto come target.
Una volta rimosse 945 osservazioni duplicate, le rimanenti 19,113 sono state divise in training set (80%) e test set (20%)
(random state=42). 
Durante la fase di Analisi Esplorativa dei Dati sono state analizzate le distribuzioni delle variabili e le correlazioni tra feature.
Sono state rimosse 9 delle features iniziali, dalle quali però sono state estratte 5 features aggiuntive.
Il dataset finale è dunque composto da 6 features numeriche (contando il target) e 5 categoriali, per un totale di **11 features** quali:
1. turns
2. black_rating
3. opening_ply (numero di mosse nella fase di apertura)
4. black_captures_rate
5. black_checks_rate
6. white_castled (T/F)
7. black_castled (T/F)
8. victory_status
9. winner
10. opening_category (tipo di apertura)
11. **white_rating (target)**

## Preprocessing
I valori mancanti (NaN) sono stati gestiti tramite imputazione con la media della variabile, calcolata esclusivamente sul training set al fine di evitare data leakage.
Le variabili numeriche sono poi state standardizzate tramite StandardScaler.
Tutte le trasformazioni sono state implementate all’interno di una pipeline, garantendo che il fitting delle trasformazioni avvenisse unicamente sui dati di training e venisse poi applicato in modo coerente al test set.

## Modelli testati


## Struttura
- notebook.ipynb → notebook principale
- src/ → codice Python riutilizzabile
- reports/ → relazione finale, grafici
