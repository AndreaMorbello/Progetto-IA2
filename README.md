# Progetto-IA2
Progetto Esame IA2 - Morbello Venezia Di Capua - Università Sapienza di Roma

## Descrizione breve:
Il progetto ha come obiettivo l'addestramento di un modello di regressione capace di stimare il punteggio ELO di un giocatore data una sua partita di scacchi.
Prende ispirazione dalla serie 'Guess The Elo' del noto youtuber americano 'GothamChess' (youtube.com/@GothamChess).

## Dataset 
**Fonte**: Kaggle
**Link**: https://www.kaggle.com/datasets/datasnaek/chess
Inizialmente il dataset era composto da 20,058 osservazioni e 16 features, fra cui *white_rating* scelto come target.
Una volta rimosse 945 osservazioni duplicate, le rimanenti 19,113 sono state divise in training set (80%) e test set (20%)
(random state=42). 
Durante la fase di Analisi Esplorativa dei Dati sono state analizzate le distribuzioni delle variabili e le correlazioni tra feature.
Sono state rimosse 9 delle features iniziali, dalle quali però sono state estratte 5 delle features finali.
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
Per valutare successivamente altri modelli sono stati presi 2 modelli come baseline naive:
1. Il primo si limita a restituire come output la media della variabile target
2. Il secondo utilizza "black_rating" come unica feature

Dopodiché sono stati addestrati 3 modelli lineari:
1. Linear Regression
2. Ridge Regression (α = 1.0)
3. Lasso Regression (α = 1.0)

##Risultati
La valutazione dei modelli è stata fatta attravero MAE, RMSE e R²

| Modello                  |    MAE |   RMSE |     R2 |
|---------------------------|-------:|-------:|-------:|
| Media White Rating        |   ∼290 |   ∼290 |  0.0000 |
| Black Rating              |   ∼190 |   ∼250 |  ∼0.29 |
| Linear Regression         |  152.50 | 204.14 | 0.5065 |
| Ridge Regression          |  152.50 | 204.14 | 0.5065 |
| Lasso Regression          |  152.58 | 204.34 | 0.5055 |

##Conclusioni
Come inizialmente ipotizzato *black_rating* è la feature più informativa, ciononostante i risultati ottenuti mostrano il contributo delle altre features ad una stima più accurata.
I modelli lineari presentano prestazioni nettamente superiori rispetto alla baseline, spiegando circa il 50% della variabilità del white_rating
La regolarizzazione, però, quantomeno con α = 1.0, non ha prodotto risultati significativamente diversi, il che suggerisce che probabilmente il plateau nella performance dei modelli lineari è dovuto al loro limite espressivo piuttosto che ad overfitting o ad instabilità delle features.

##Sviluppi futuri
- L'analisi dei residui mostra possibili pattern non lineari che modelli più complessi, come Random Forest o Gradient Boosting, potrebbero essere in grado di catturare
- Cross-validation
- Feature engineering avanzato: analisi approfondita delle mosse tramite motori scacchistici
- Hyperparameter tuning: ottimizzazione dell'iperparametro α nei modelli di regressione Ridge e Lasso

## Struttura
- notebook.ipynb → notebook principale
- src/ → codice Python riutilizzabile
- reports/ → relazione finale, grafici
- requirements.txt → librerie utilizzate
