# AQI_taly - Mappa intelligente della qualità dell'aria per l'Italia 🇮🇹

Un sistema intelligente di monitoraggio della qualità dell'aria per l'Italia che fornisce dati sull'inquinamento in tempo reale, previsioni e informazioni ambientali contestuali.

**[Link Presentazione](https://canva.link/o9kh9phlb0qnts9)**

## 🌟 Funzionalità

### Funzionalità principali
- **Monitoraggio della qualità dell'aria in tempo reale**: Dati PM10 e PM2.5 in tempo reale dalle stazioni di monitoraggio in tutta Italia
- **Mappa interattiva**: Mappa basata su Leaflet con visualizzazione intuitiva dei livelli di inquinamento
- **Previsioni basate sull'IA**: Previsioni di serie temporali basate su Prophet per le previsioni di inquinamento
- **Livelli contestuali**:

- Monitoraggio degli incendi attivi (integrazione con incendioggi.it)

- Mappatura degli impianti industriali con analisi dell'impatto dell'inquinamento
- Filtro spaziale BBOX per prestazioni ottimizzate

### Funzionalità intelligenti
- **Analisi delle fonti di inquinamento**: Identificazione basata sull'IA delle fonti di inquinamento per ogni stazione di monitoraggio
- **Stati delle icone intelligenti**: Feedback visivo che mostra quali industrie contribuiscono all'inquinamento
- **Aggiornamenti della mappa con debounce**: Chiamate API ottimizzate attivate solo all'interazione con la mappa (zoom/pan)
- **Lazy Loading**: Caricamento efficiente dei dati per popup e dettagli

### Visualizzazione dei dati
- **Doppia modalità di visualizzazione**: Passa dai dati in tempo reale alle previsioni Visualizzazioni
- **Stazioni con codifica a colori**: indicatori di qualità dell'aria verde (buona), giallo (moderata), rosso (scarsa)
- **Dettagli completi delle stazioni**: dati storici, tendenze e analisi dell'inquinamento
- **Cronologia delle previsioni**: cronologia interattiva per esplorare le previsioni future sull'inquinamento

## 🏗️ Architettura

### Backend (Python/Flask)
- **Framework**: Flask con Flask-CORS e Flask-Caching
- **Fonti dati**:

- ARPA (Agenzie regionali per la protezione ambientale)

- API OpenWeatherMap per i dati sulla qualità dell'aria

- incendioggi.it per il monitoraggio degli incendi

- Database E-PRTR per gli impianti industriali
- **Previsioni**: Facebook Prophet per la previsione di serie temporali
- **Caching**: cache di 30 minuti per prestazioni ottimali

### Frontend (React)
- **Framework**: React 18 con Hooks
- **Mappatura**: React-Leaflet per la visualizzazione interattiva mappe
- **Gestione dello stato**: Contesto React e stato locale
- **Componenti UI**: Interfaccia utente flottante personalizzata con design professionale
- **Ottimizzazione**: Memoizzazione e debouncing per prestazioni fluide

## 📦 Installazione

### Prerequisiti
- Python 3.8+
- Node.js 14+
- npm o yarn

### Configurazione del backend

```bash
cd backend

# Crea un ambiente virtuale
python -m venv venv
source venv/bin/activate # Su Windows: venv\Scripts\activate

# Installa le dipendenze
pip install -r requirements.txt

# Crea il file .env
cp .env.example .env
# Modifica il file .env e aggiungi la tua chiave API di OpenWeatherMap

# Avvia il backend
python app.py
```

Il backend verrà avviato su `http://localhost:5000`

### Configurazione del frontend

```bash
cd frontend

# Installa le dipendenze
npm install

# Avvia il server di sviluppo
npm start
```

Il frontend si avvierà su `http://localhost:3000`

## 🔧 Configurazione

### Variabili d'ambiente del backend

Crea un file `.env` nella directory `backend`:

```env
OWM_API_KEY=la_tua_chiave_API_openweathermap_qui
FLASK_ENV=development
FLASK_DEBUG=True
```

### Chiavi API

- **API di OpenWeatherMap**: Ottieni la tua chiave API gratuita su [openweathermap.org](https://openweathermap.org/api)

## 🚀 Utilizzo

1. **Avvia il backend**: Esegui 1. Eseguire `python app.py` nella directory backend
2. **Avviare il Frontend**: Eseguire `npm start` nella directory frontend
3. **Aprire il browser**: Accedere a `http://localhost:3000`
4. **Esplorare la mappa**:

- Fare clic sulle stazioni per visualizzare informazioni dettagliate

- Passare da PM10 a PM2.5

- Passare da dati giornalieri a dati orari

- Abilitare i layer contestuali (incendi, industrie)

- Passare alla modalità previsione per visualizzare le previsioni

## 📊 Endpoint API

### Endpoint principali
- `GET /api/map-base` - Dati base della mappa con tutte le stazioni
- `GET /api/realtime-details` - Dati orari in tempo reale
- `GET /api/forecast-maps` - Dati di previsione per la visualizzazione della mappa
- `GET /api/map-layers` - Layer contestuali (incendi, industrie) con filtro BBOX

### Dettagli stazione
- `GET `/api/station/<station_id>` - Informazioni dettagliate sulla stazione
- `GET /api/pollution-analysis` - Analisi delle fonti di inquinamento basata sull'intelligenza artificiale

### Dati contestuali
- `GET /api/industry-details/<industry_id>` - Dettagli sugli impianti industriali
- `GET /api/fire-details/<fire_id>` - Dettagli sugli incendi

## 🧪 Test

### Test del backend
```bash
cd backend
pytest
```

### Test del frontend
```bash
cd frontend
npm test
```

## 🎨 Funzionalità in dettaglio

### Filtro spaziale BBOX
Ottimizza le prestazioni della mappa filtrando industrie e incendi in base alla visuale visibile:
- Calcolo automatico del BBOX durante il movimento sulla mappa
- Debounce di 500 ms per prevenire lo spam delle API
- Filtro spaziale lato server
- Gradleful degrado in caso di fallimento del filtraggio

### Stati delle icone intelligenti
Sistema di feedback visivo per le fonti di inquinamento:
- **Stato neutro**: opacità del 50%, nessun bordo (fonti non inquinanti)
- **Stato attivo**: opacità del 100%, bordo rosso con animazione a impulsi (fonti inquinanti)
- Aggiornamenti reattivi basati sull'analisi dell'inquinamento

### Analisi delle fonti di inquinamento
Analisi basata sull'IA che identifica:
- Emissioni industriali
- Modelli di traffico
- Incidenti da incendio
- Condizioni meteorologiche
- Fornisce informazioni utili per ogni stazione

## 📁 Struttura del progetto

```
AQI_taly/
├── backend/
│ ├── app.py # Applicazione Flask principale
│ ├── context/
│ │ ├── industry_checker.py # Logica per gli impianti industriali
│ │ └── fire_fetcher.py # Logica per il monitoraggio degli incendi
│ ├── requirements.txt # Dipendenze Python
│ └── .env # Variabili d'ambiente
├── frontend/
│ ├── src/
│ │ ├── App.js # Componente React principale
│ │ ├── components/ # Componenti React
│ │ ├── hooks/ # Hook React personalizzati
│ │ └── index.js # Punto di ingresso
│ ├── package.json # Dipendenze Node
│ └── public/ # Risorse statiche
├── AnalisiGeodatabase/ # Strumenti di analisi del GeoDatabase
└── README.md # Questo file
```

## 🤝 Contributi

I contributi sono benvenuti! Non esitate a inviare una Pull Request.

1. Effettua il fork del repository
2. Crea il tuo branch di funzionalità (`git checkout -b feature/AmazingFeature`)
3. Esegui il commit delle modifiche (`git commit -m 'Aggiungi una funzionalità straordinaria'`)
4. Esegui il push sul branch (`git push origin feature/AmazingFeature`)
5. Apri una Pull Request

## 📝 Licenza

Questo progetto è rilasciato sotto licenza MIT - consulta il file LICENSE per i dettagli.

## 🙏 Ringraziamenti

- **Fonti dei dati**:

- ARPA (Agenzie regionali per la protezione ambientale)

- OpenWeatherMap

- incendioggi.it

- Database E-PRTR
- **Librerie**:

- Ecosistemi Flask e React

- Facebook Prophet per le previsioni

- Leaflet per la mappatura

- Hypothesis per i test basati sulle proprietà

---

Realizzato con ❤️ per un'aria più pulita in Italia
