# Fantasy Football Demo App ⚽

Una demo funzionante di un'app di fantacalcio con funzionalità distintiva: **Allenatore Personale** che commenta i risultati delle partite.

## 🎯 Caratteristiche Principali

### ✅ Funzionalità Implementate

- **Creazione Lega**: Crea leghe private con squadre mock
- **Creazione Squadra**: Seleziona giocatori con budget limitato
- **Gestione Budget**: Sistema di budget in tempo reale
- **Visualizzazione Formazione**: Campo da calcio stilizzato con i tuoi giocatori
- **Classifica**: Ranking automatico delle squadre
- **Persistenza Dati**: Salvataggio automatico con localStorage

### 🌟 Funzionalità Distintiva: Allenatore Personale

Ogni squadra può scegliere un allenatore con personalità unica che commenta i risultati:

- **Il Filosofo** 🧙‍♂️ - Riflessivo e profondo
- **Il Tattico** 📋 - Ossessionato dagli schemi
- **Il Corto Muso** 💪 - Pratico e diretto
- **Il Motivatore** 🔥 - Sempre positivo ed energico
- **L'Ironico** 😏 - Sarcastico e pungente
- **Lo Scaramantico** 🍀 - Superstizioso e prudente

Ogni allenatore ha frasi diverse per:
- ✅ Vittoria
- ⚖️ Pareggio
- ❌ Sconfitta

### 📊 Dati Reali Serie A (Opzionale)

Integrazione con **API-Football** per visualizzare:
- Classifica Serie A in tempo reale
- Partite in programma e risultati
- Partite LIVE

## 🚀 Come Iniziare

### 🌐 Demo Online (GitHub Pages)

**La demo è disponibile online!**

👉 **[Apri la Demo Live](https://xtruel.github.io/fantacalciorepo/)**

Puoi condividere questo link con il cliente per mostrare l'anteprima.

### 1. Installazione Base

Nessuna installazione richiesta! Basta aprire `index.html` nel browser.

```bash
# Clona la repository
git clone https://github.com/xtruel/fantacalciorepo.git

# Apri index.html nel browser
# Oppure usa un server locale:
python -m http.server 8000
# Poi vai su http://localhost:8000
```

### 2. Configurazione API (Opzionale)

Per abilitare i dati reali della Serie A:

1. **Registrati gratuitamente** su [API-Football](https://www.api-football.com/)
   - Piano gratuito: 100 richieste/giorno
   - Nessuna carta di credito richiesta

2. **Ottieni la tua API Key** dal dashboard

3. **Configura l'API Key** in `script.js`:
   ```javascript
   const FootballAPI = {
       apiKey: 'LA_TUA_API_KEY_QUI', // Sostituisci con la tua key
       // ...
   }
   ```

4. **Ricarica l'app** e clicca su "Serie A Live" nella home

> **Nota**: Senza API key, l'app usa dati mock ma funziona perfettamente!

## 📱 Come Usare l'App

### Flusso Completo

1. **Crea una Lega**
   - Vai su "Crea Lega"
   - Inserisci nome e numero squadre
   - Le squadre avversarie vengono generate automaticamente

2. **Crea la Tua Squadra**
   - Vai su "Crea Squadra"
   - Scegli il tuo **Allenatore Personale**
   - Seleziona giocatori rispettando il budget (500 crediti)
   - Salva la squadra

3. **Simula una Giornata**
   - Clicca sul pulsante ⚽ in basso a destra
   - Guarda il risultato della partita
   - Il tuo allenatore commenterà il risultato!

4. **Visualizza Classifica**
   - Vai su "Classifica"
   - La tua squadra è evidenziata in blu

5. **Dati Reali Serie A** (se configurato)
   - Vai su "Serie A Live"
   - Visualizza classifica e partite reali

## 🎨 Design

L'app è ispirata esteticamente a **Leghe.Fantacalcio.it** con:
- Design mobile-first responsive
- Colori vivaci (blu, verde, arancio)
- Card arrotondate
- Animazioni smooth
- Bottom navigation stile app nativa

## 🛠️ Tecnologie

- **HTML5** - Struttura semantica
- **CSS3** - Styling moderno con gradients e animazioni
- **JavaScript Vanilla** - Nessuna dipendenza esterna
- **LocalStorage** - Persistenza dati lato client
- **API-Football** - Dati reali Serie A (opzionale)

## 📂 Struttura File

```
fantacalciorepo/
├── index.html          # Struttura HTML principale
├── style.css           # Tutti gli stili
├── script.js           # Logica applicazione
└── README.md           # Questo file
```

## 🔮 Roadmap Futura (Non in questa demo)

- [ ] Sistema voti reale (statistico + pagellista)
- [ ] Asta real-time
- [ ] Chat tra utenti
- [ ] Notifiche push
- [ ] Statistiche avanzate
- [ ] Modalità multiplayer
- [ ] App mobile nativa (React Native)
- [ ] Backend con database
- [ ] Sistema di pagamento

## 🐛 Troubleshooting

### L'app non salva i dati
- Controlla che il browser supporti localStorage
- Verifica che non sia in modalità incognito

### API Serie A non funziona
- Verifica di aver inserito la API key corretta
- Controlla di non aver superato il limite di 100 richieste/giorno
- L'app funziona comunque con dati mock!

### Il popup allenatore non appare
- Assicurati di aver selezionato un allenatore
- Assicurati di aver creato una lega e una squadra
- Clicca sul pulsante ⚽ per simulare una partita

## 📄 Licenza

Questo è un progetto demo. Tutti i nomi di giocatori sono fittizi.
Non utilizza dati reali di giocatori o squadre senza permesso.

## 👥 Contributi

Questo è un progetto demo per validare il concept.
Per contributi o suggerimenti, apri una issue su GitHub.

## 📞 Contatti

Repository: [github.com/xtruel/fantacalciorepo](https://github.com/xtruel/fantacalciorepo)

---

**Buon divertimento con il tuo Fantacalcio! ⚽🏆**
