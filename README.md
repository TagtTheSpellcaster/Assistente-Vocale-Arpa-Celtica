# Assistente Vocale Arpa Celtica (PWA)

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Platform](https://img.shields.io/badge/platform-Web%20%7C%20PWA-orange)
![Accessibility](https://img.shields.io/badge/accessibility-WCAG%20AAA-purple)

Un'applicazione web progressiva (PWA) progettata specificamente con criteri di accessibilità elevati per musicisti e arpinisti non vedenti o ipovedenti. Permette di consultare verbalmente e a mani libere le configurazioni delle levette (semitoni) dell'arpa celtica per diverse tonalità maggiori e minori.

## Descrizione

L'arpa celtica con accordatura standard (tutte le levette abbassate in Mi♭ maggiore) richiede di alzare o abbassare specifiche levette per modificare la tonalità.

Questa applicazione:

1. Ascolta il comando vocale dell'utente (es. "La minore", "Sol maggiore", "Mi bemolle").
2. Identifica la tonalità (con priorità algoritmica e normalizzazione dei termini per prevenire errori fonetici).
3. Risponde ad alta voce usando la sintesi vocale del dispositivo, elencando chiaramente quali levette sollevare con dizione scandita e senza congiunzioni che possano confondere l'ascolto.

## Struttura dei File del Progetto

Il progetto si compone dei seguenti file da inserire nella medesima cartella sul server web:

```
├── index.html       # Applicazione principale e interfaccia utente
├── manifest.json    # File di configurazione PWA (meta-dati)
├── sw.js            # Service Worker per la gestione della cache offline
└── README.md        # Documentazione del progetto
```

## Funzionalità e Accessibilità

* Schermo come unico pulsante gigante: L'intera superficie della pagina funge da area di contatto. Un tocco in qualsiasi punto attiva l'ascolto vocale.
* Supporto Tastiera / Pedale USB: Premendo la Barra Spaziatrice si avvia l'ascolto a mani libere.
* Dizione scandita e distaccata: I nomi delle note da sollevare sono separati da un punto e virgola (;) anziché dalla congiunzione "e", favorendo una scansione ritmica netta da parte dei lettori di schermo.
* Temporizzazione intelligente anti-sovrapposizione: Il microfono viene attivato esclusivamente al termine del messaggio vocale guida dell'app ("In ascolto..."), evitando che l'altoparlante interferisca con il microfono.
* Selezione prioritaria delle voci naturali: Il sistema rileva e seleziona automaticamente le voci italiane femminili e naturali disponibili sul sistema operativo (es. Microsoft Elsa su Windows, Alice/Federica su iOS/macOS, o voci ad alta qualità su Android).

## Compatibilità Browser e Piattaforme

Il funzionamento del riconoscimento vocale (Web Speech API) varia in base al motore di trascrizione sottostante utilizzato da ciascun browser e sistema operativo.

### Tabella di Compatibilità

| Piattaforma | Browser Consigliato | Stato | Note e Funzionamento |
|---|---|---|---|
| **iOS (iPhone / iPad)** | Safari | **Piena** | Sfrutta l'engine nativo Apple (Siri). Riconosce perfettamente la lingua italiana, i modi minori e le alterazioni (*Fa diesis minore*). **Piattaforma di riferimento per la PWA.** |
| **Android** | Chrome / Brave / APK | **Piena** | Utilizza *Google Speech Services* di sistema. Elabora la dizione italiana locale senza troncare le parole composte. |
| **macOS** | Safari | **Piena** | Utilizza il motore di dettatura nativo di macOS. |
| **Windows / macOS** | Chrome / Edge | **Parziale** | Invia l'audio ai server Cloud di Google. Il post-processing in italiano tende a scartare o convertire erratamente i termini musicali isolati (es. *"minore"* o *"bemolle"*). |
| **Qualsiasi OS** | Brave (Desktop) | **Non supportato** | L'API `SpeechRecognition` è disabilitata nativamente dal browser per politiche di privacy. |
| **Qualsiasi OS** | Firefox (Desktop) | **Non supportato** | L'API `SpeechRecognition` non è abilitata di default nei sorgenti del browser. |

### Dettagli Tecnici sui Motori Vocali

* **Engine Nativo Apple (Safari su iOS/macOS):** L'elaborazione audio avviene a livello di sistema operativo ed è ottimizzata per la dizione naturale e i termini compositi italiani. È l'ambiente ideale per l'uso a mani libere da parte di utenti ipovedenti o non vedenti tramite **VoiceOver**.
* **Engine Nativo Android (Chrome/Brave su Android):** Sia il browser che l'APK installato si appoggiano ai servizi vocali integrati del dispositivo, garantendo la corretta normalizzazione dei comandi vocali.
* **Engine Cloud Google (Chrome/Edge su Desktop):** L'audio viene inviato ai server web di Google, il cui filtro linguistico per il desktop rischia di scambiare aggettivi musicali come *"minore"* per punteggiatura o rumore di fondo.

## Come Installare e Usare

### Requisiti di Sistema

Per accedere alle API vocali e consentire l'installazione PWA, la pagina deve essere ospitata su un server HTTPS (es. GitHub Pages, Netlify, Vercel o server proprio con SSL).

### Installazione su Smartphone (Android / iOS)

1. Apri il link dell'applicazione nel browser (Chrome su Android o Safari su iOS).
2. Su Android (Chrome): Tocca il banner "Aggiungi a schermata Home" o seleziona dal menu "Installa applicazione".
3. Su iOS (Safari): Tocca l'opzione di condivisione e seleziona "Aggiungi alla schermata Home".
4. Avvia l'app toccando l'icona creata sulla schermata iniziale.

### Modalità d'Uso Vocale

1. Tocca lo schermo (o premi la barra spaziatrice).
2. Attendi che la voce guida dica "In ascolto. Pronuncia la tonalità."
3. Pronuncia la tonalità desiderata.
   * Esempi validi:
     * "Do maggiore" oppure semplicemente "Do"
     * "La minore"
     * "Mi bemolle"
     * "Sol minore"
     * "Fa diesis minore"
4. L'assistente leggerà la configurazione delle levette.

## Configurazione Tonalità (Accordatura Standard Mi♭)

| Tonalità | Note con levetta SU (sollevata) |
| --- | --- |
| Mi♭ Maggiore / Do Minore | Tutte le levette GIÙ |
| Si♭ Maggiore / Sol Minore | La |
| Fa Maggiore / Re Minore | Mi ; La |
| Do Maggiore / La Minore | Mi ; La ; Si |
| Sol Maggiore / Mi Minore | Mi ; Fa ; La ; Si |
| Re Maggiore / Si Minore | Do ; Mi ; Fa ; La ; Si |
| La Maggiore / Fa♯ Minore | Do ; Mi ; Fa ; Sol ; La ; Si |
| Mi Maggiore / Do♯ Minore | Tutte le levette SU |

## Licenza

Questo progetto è distribuito sotto Licenza MIT (versione 1.0.0). Libero di essere utilizzato, modificato e redistribuito.
