# Apprendimento Trasferire Profondo (SDTL) per la Stima Cross-Scenario dello SOH delle Batterie agli Ioni di Litio

## I. Introduzione

Con la crescita esplosiva dei veicoli elettrici e dei sistemi di accumulo di energia, la stima accurata dello **Stato di Salute (State of Health, SOH)** delle batterie agli ioni di litio è cruciale per garantire la sicurezza del sistema e prolungare la durata della batteria.

Tuttavia, nelle applicazioni pratiche, affrontiamo due sfide principali:

- **Ambiente Complesso e Variabile**: Diversi materiali catodici (come NCM, NCA), fluttuazioni drammatiche della temperatura ambiente e diversi protocolli di carica-scarica.
- **Silos di Dati e Scarsità di Campioni**: Le nuove batterie hanno dati estremamente limitati durante il periodo di servizio iniziale, mentre i tradizionali modelli di apprendimento profondo spesso richiedono dati etichettati massicciamente per ottenere una buona capacità di generalizzazione.

Per affrontare queste sfide, un articolo pubblicato sulla prestigiosa rivista *Journal of Power Sources* intitolato ***Deep transfer learning enabled online state-of-health estimation of lithium-ion batteries under small samples across different cathode materials*** presenta i risultati della ricerca più recente: un metodo di **Apprendimento Trasferiere Profondo (SDTL)** basato su un **Meccanismo di Auto-Attenzione**.

## II. Framework SDTL

Lo studio propone un efficiente sistema SDTL con tre componenti principali: **estrazione delle caratteristiche**, **pre-addestramento** e **ottimizzazione fine**:

<p align="center">
  <img src="/fig1.png" style="width: 100%; margin: 0 auto; display: block;">
</p>
<p align="center" style="color: grey">Architettura del Sistema di Apprendimento Trasferiere Profondo (SDTL) Basato su Meccanismo di Auto-Attenzione</p>

### 1. Estrazione di Indicatori di Salute Multi-Sorgente (HI)

I ricercatori hanno estratto **18 indicatori di salute** da tensione/corrente di carica, tensione/corrente di scarica e curve di capacità incrementale (IC). Utilizzando il **Coefficiente di Correlazione di Pearson (PCC)** per filtrare le caratteristiche altamente correlate con SOH (come HI3, HI5, HI11, ecc.), hanno assicurato l'interpretabilità fisica e la capacità di rappresentazione dei dati di input.

<p align="center">
  <img src="/fig2.png" style="width: 100%; margin: 0 auto; display: block;">
</p>
<p align="center" style="color: grey">Analisi del Coefficiente di Correlazione di Pearson (PCC) tra gli Indicatori di Salute Estratti (HI) e SOH</p>

### 2. Meccanismo di Auto-Attenzione

A differenza dei tradizionali RNN o LSTM, SDTL impiega un **Meccanismo di Auto-Attenzione Multi-Testa**. Cattura dipendenze globali in diverse posizioni nella serie temporale e assegna automaticamente pesi alle caratteristiche di degrado più critiche, consentendo un'identificazione più accurata dei modelli di degrado della batteria in diverse condizioni di funzionamento.

<p align="center">
  <img src="/fig3.png" style="width: 100%; margin: 0 auto; display: block;">
</p>
<p align="center" style="color: grey">Diagramma dell'Architettura del Modulo di Auto-Attenzione Multi-Testa</p>

### 3. Apprendimento Trasferiere Profondo

- **Pre-addestramento (Offline)**: Utilizzo di grandi quantità di dati storici delle batterie (dominio sorgente) per il pre-addestramento, consentendo al modello di apprendere modelli generali di degrado della batteria.
- **Ottimizzazione Fine (Online)**: Per nuovi compiti di batteria (dominio target), sono necessari solo i dati dei primi cicli iniziali al 10% per completare l'adattamento online. Congelando i strati di estrazione delle caratteristiche di livello inferiore e aggiornando solo i parametri dello strato di output, viene raggiunto il trasferimento cross-scenario rapido ed economico.

## III. Validazione Sperimentale

Per verificare la prestazione di generalizzazione di SDTL, i ricercatori hanno condotto test sperimentali estremamente rigorosi:

<p align="center">
  <img src="/fig8.png" style="width: 100%; margin: 0 auto; display: block;">
</p>
<p align="center" style="color: grey">Risultati della Stima dello SOH del Modello SDTL sui Dati delle Batterie Sperimentali</p>

- **Copertura Completa del Dataset**: Include dataset di batterie NCM auto-costruite (tassi 1C/2C) e dataset di batterie NCA pubblicamente disponibili dalla NASA (che coprono temperature ambiente di 24°C e 4°C).
- **Risultati delle Prestazioni**: I risultati sperimentali mostrano che anche in condizioni difficili come temperatura bassa (4°C) e tassi di scarica elevati, SDTL dimostra un'accuratezza di stima estremamente elevata e robustezza.
- **Vantaggi Comparativi**: Rispetto ai tradizionali algoritmi di apprendimento profondo e ad altri metodi di apprendimento trasferiere, SDTL mostra vantaggi chiari negli scenari con pochi campioni, eliminando l'alto costo dell'addestramento dei modelli da zero.

<p align="center">
  <img src="/fig9.png" style="width: 100%; margin: 0 auto; display: block;">
</p>
<p align="center" style="color: grey">Confronto delle Prestazioni di Previsione tra SDTL e Modelli Mainstream (CNN-LSTM, GRU, ResNet)</p>

## IV. Conclusione

I contributi del articolo si riflettono principalmente in:

- **Efficienza**: L'adattamento online rapido può essere ottenuto con solo il 10% dei dati.
- **Ampia Applicabilità**: Può gestire diversi materiali catodici (NCM vs NCA) e variazioni della temperatura ambiente.
- **Valore Ingegneristico**: Fornisce una soluzione di stima online dello SOH pratica, leggera e ad alta precisione per BMS (Battery Management Systems).


## Informazioni di Riferimento

- **Titolo**: Deep transfer learning enabled online state-of-health estimation of lithium-ion batteries under small samples across different cathode materials, ambient temperature and charge-discharge protocols
- **Journal**: Journal of Power Sources (2025)
- **DOI**: 10.1016/j.jpowsour.2025.237503
- **Link**: [https://doi.org/10.1016/j.jpowsour.2025.237503](https://doi.org/10.1016/j.jpowsour.2025.237503)
