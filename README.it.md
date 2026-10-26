# Luma Home — Dashboard multilingue per Home Assistant

[English](README.md) | [Français](README.fr.md) | [Italiano](README.it.md)

Versione derivata non ufficiale di Aurora Glass v3, adattata da Fonkyup con un’interfaccia in italiano, francese e inglese.

> Convenzione attuale: il tipo di scheda è `custom:luma-home-card`. Il file JavaScript mantiene il nome `aurora-v3.js`. Per l’installazione manuale descritta qui sotto, i file vengono copiati in `www/luma-home/`. La cartella sorgente del repository rimane `luma-home/www/aurora-v3/`: copia il suo contenuto nella cartella di destinazione, senza presumere che i due nomi debbano coincidere.

## Origine del progetto e contributi

Luma Home si basa su Aurora Glass v3, creato da DomotikPro.it (Luca Pinelli).

Avviso originale conservato: © 2026 DomotikPro.it (Luca Pinelli).

Adattamento e traduzioni: Fonkyup.

I contributi comprendono:
- aggiunta delle traduzioni francese e inglese dell’interfaccia;
- adattamento dei testi e dei messaggi dinamici;
- aggiunta della documentazione e degli esempi tradotti;
- adozione del nome pubblico Luma Home e del tipo di scheda `custom:luma-home-card`.

Documentazione aggiornata il 26 ottobre 2026. Le date delle modifiche sono riportate anche negli avvisi dei sorgenti e nella cronologia del repository.

La lingua italiana del progetto originale è mantenuta. Questa versione non è una pubblicazione ufficiale del progetto originale e non viene presentata come approvata da DomotikPro.it o Luca Pinelli.

## Risorse del progetto originale

I seguenti collegamenti riguardano Aurora Glass v3, non necessariamente questa versione derivata:

- Demo originale: https://domotikpro.it/aurora-glass-v3-demo/index.html
- Guida illustrata originale: https://domotikpro.it/progetti/aurora-glass-v3
- Video dell’autore originale: https://www.youtube.com/@domotikproit
- Repository originale: https://github.com/lucalux00/aurora-glass-v3

Le istruzioni tecniche della versione derivata riportate qui sotto possono differire da quelle della guida originale.

## Funzionalità

Funzionalità ereditate dal progetto originale:
- 10 mondi animati e 11 effetti meteorologici e atmosferici: pioggia, neve, temporali, lucciole, petali, fuochi d’artificio…
- Cielo, sole e luna che seguono l’ora reale.
- 50 immagini e GIF per i pulsanti di luci, scene, sensori, allarme e clima.
- Pannello allarme, controllo del clima e telecamere.
- Vista Energia con potenza, consumi in kWh e costi calcolati come kWh × tariffa.
- Scheda distribuita come file JavaScript, senza compilazione necessaria per l’installazione manuale.

Questa versione aggiunge la selezione della lingua tramite `language: it`, `language: fr` o `language: en`.

## Privacy e collegamenti esterni

Secondo la documentazione originale, la scheda funziona localmente e carica i caratteri Google Fonts Manrope e Sora tramite una richiesta esterna. L’autore originale dichiara che la scheda non raccoglie né invia dati.

Questa descrizione non costituisce una verifica indipendente della sicurezza o del traffico di rete. Le integrazioni Home Assistant utilizzate dai dispositivi possono avere collegamenti esterni propri.

## Guide ed esempi

Guide brevi:
- [Italiano](luma-home/LEGGIMI.txt)
- [Français](luma-home/LISEZMOI.fr.txt)
- [English](luma-home/README.en.txt)

Esempi in italiano:
- [Plancia completa](luma-home/dashboard-esempio.yaml)
- [Opzioni dettagliate della scheda](luma-home/scheda-esempio.yaml)
- [Contatori di energia facoltativi](luma-home/aurora-energia.yaml)

Gli esempi devono usare `custom:luma-home-card`. Per l’installazione manuale descritta qui sotto, il percorso delle immagini deve essere `/local/luma-home/btn/`.

## Installazione manuale

### 1. Copiare i file

Dalla cartella `luma-home/www/aurora-v3/` del repository, copia il file `aurora-v3.js` e la cartella completa `btn` in una cartella chiamata `luma-home`, all’interno della cartella `www` della configurazione di Home Assistant.

Il risultato deve essere:

```text
www/
└── luma-home/
    ├── aurora-v3.js
    └── btn/
        └── immagini e GIF dei pulsanti
```

Il percorso sorgente e quello di destinazione sono volutamente diversi:

```text
Sorgente nel repository:
luma-home/www/aurora-v3/aurora-v3.js

Destinazione in Home Assistant:
www/luma-home/aurora-v3.js
```

Usa il JavaScript e le immagini della stessa versione. La cartella `dist` contiene la copia di distribuzione: non mescolare file provenienti da revisioni diverse.

Se la cartella `www` è appena stata creata, riavvia Home Assistant una volta.

Apri nel browser:

```text
<indirizzo di Home Assistant>/local/luma-home/aurora-v3.js
```

Dovrebbe comparire il testo JavaScript.

### 2. Aggiungere o aggiornare la risorsa

Attiva la Modalità avanzata nel tuo profilo.

Impostazioni → Plance → menu ⋮ → Risorse → Aggiungi risorsa:

- URL: `/local/luma-home/aurora-v3.js?v=1`
- Tipo: Modulo JavaScript.

Aumenta il numero dopo `?v=` a ogni aggiornamento. Se la risorsa esiste già, aggiornala invece di aggiungerne una seconda. Evita di caricare più versioni della stessa scheda.

### 3. Creare la plancia

Impostazioni → Plance → Aggiungi plancia → Nuova plancia da zero.

Titolo suggerito: `Luma Home`.

### 4. Inserire la configurazione

L’esempio completo originale è [dashboard-esempio.yaml](luma-home/dashboard-esempio.yaml). Le opzioni dettagliate sono descritte in [scheda-esempio.yaml](luma-home/scheda-esempio.yaml).

Gli esempi di questa versione devono utilizzare `custom:luma-home-card` e il percorso delle immagini previsto per l’installazione scelta.

L’esempio dettagliato descrive una singola scheda, non un’intera plancia. Non incollarlo direttamente alla radice della configurazione della dashboard.

Su una nuova plancia, apri l’Editor di configurazione testuale e usa una configurazione minima come questa:

```yaml
title: Luma Home
views:
  - title: Casa
    path: casa
    icon: mdi:home-heart
    panel: true
    cards:
      - type: custom:luma-home-card
        language: it
        assets: /local/luma-home/btn/
```

Salva una copia della configurazione prima di sostituire una plancia esistente.

### 5. Collegare le entità

Strumenti per sviluppatori → Stati: individua gli identificatori delle tue entità.

Aggiungi `entities` alla configurazione della scheda, allo stesso livello di `type`, `language` e `assets`:

```yaml
type: custom:luma-home-card
language: it
assets: /local/luma-home/btn/
entities:
  lights:
    salotto: light.salotto
```

`light.salotto` è un esempio da sostituire con la tua entità. Mantieni le chiavi previste dalla scheda, come `salotto`, `cucina` e `ingresso`.

Lingue disponibili:
- `it`: italiano;
- `fr`: francese;
- `en`: inglese.

Il codice attuale usa l’italiano quando la lingua non è specificata.

### 6. Energia e tariffa — facoltativo

La configurazione dell’energia appartiene a `entities.energy`:

```yaml
type: custom:luma-home-card
language: it
assets: /local/luma-home/btn/
entities:
  energy:
    power: sensor.potenza_casa
```

Sostituisci `sensor.potenza_casa` con il tuo sensore di potenza in watt.

Per i contatori di energia, consulta [aurora-energia.yaml](luma-home/aurora-energia.yaml). Sostituisci il sensore segnaposto con il tuo sensore di energia cumulativa in kWh, non con un sensore di potenza in W.

Installa una sola variante del file energia: italiana, francese oppure inglese. Le varianti definiscono gli stessi contatori e non devono essere installate insieme.

Nella vista Energia imposta la tariffa per kWh. I costi sono stime basate sui consumi e sulla tariffa configurati.

## Migrazione di un’installazione esistente

Prima di abbandonare la vecchia struttura:

1. Salva una copia del JavaScript funzionante e della configurazione YAML.
2. Copia il JavaScript e le immagini in `www/luma-home/`.
3. Aggiorna la risorsa esistente a `/local/luma-home/aurora-v3.js?v=…`.
4. Usa il tipo `custom:luma-home-card`.
5. Imposta `assets: /local/luma-home/btn/`.
6. Ricarica il browser e verifica immagini, lingue e comandi.
7. Elimina la vecchia risorsa o cartella soltanto quando non è più utilizzata altrove.

Rinominare una cartella nel repository GitHub non sposta i file in Home Assistant.

Non rinominare gli identificatori dei sensori di energia o le chiavi di archiviazione del browser durante questa migrazione dei percorsi.

## Installazione con HACS

La procedura del progetto originale che indica `lucalux00/aurora-glass-v3` installa il progetto originale, non questa versione derivata.

La validazione HACS riuscita di un commit non equivale alla pubblicazione automatica nel catalogo HACS né alla verifica completa di un’installazione. Prima di documentare una procedura HACS definitiva per Luma Home, occorre verificare la versione effettivamente distribuita e i file installati.

I percorsi `/local/luma-home/` descrivono l’installazione manuale. Con HACS usa i percorsi effettivi dei file installati; non sostituire automaticamente gli URL `/hacsfiles/` con quelli dell’installazione manuale.

Il JavaScript distribuito è `dist/aurora-v3.js`. Il campo `filename` di `hacs.json` rimane `aurora-v3.js` finché questo nome viene mantenuto.

## Risoluzione dei problemi

- `Custom element doesn't exist`: verifica la risorsa, il file caricato e il tipo `custom:luma-home-card`, quindi ricarica completamente il browser.
- Immagini assenti: per l’installazione manuale descritta, verifica `assets: /local/luma-home/btn/`, compresa la barra finale. Per altre installazioni, adatta il percorso alla posizione reale delle immagini.
- Luci grigie: verifica l’identificatore e la disponibilità dell’entità.
- Costi a zero: verifica tariffa e sensori di consumo.
- Lingua errata: verifica `language` e la versione JavaScript caricata.
- Testi precedenti dopo un aggiornamento: aumenta `?v=` nella risorsa e ricarica il browser.

## Disinstallazione

Elimina la plancia interessata e la risorsa solo se non sono utilizzate altrove. Rimuovi `www/luma-home` solo se nessun’altra installazione la usa.

Questi passaggi non cancellano automaticamente le preferenze memorizzate nel browser né i contatori configurati separatamente.

## Stato e limiti delle verifiche

Il manutentore ha confermato il funzionamento della versione provata in Home Assistant e la visualizzazione delle traduzioni francese e inglese. Questo non equivale alla verifica di ogni messaggio raro o di ogni percorso dell’interfaccia.

I controlli automatici verificano i requisiti HACS, la sintassi JavaScript e l’identità tra il file di riferimento e quello di distribuzione nelle revisioni controllate. Non sostituiscono le prove funzionali dell’installazione finale. Le modifiche agli URL delle risorse, ai percorsi di installazione o al tipo di scheda richiedono una nuova prova.

Il README originale indica test dell’autore su Home Assistant 2026.9; tale indicazione non certifica questa versione derivata.

Per problemi relativi all’adattamento, apri una issue nel repository che distribuisce questa versione, indicando lingua, versione caricata e passaggi per riprodurre il problema.

## Licenza e attribuzione

Il software derivato è distribuito con [licenza GNU GPL versione 3](LICENSE).

Puoi usare, studiare, modificare e ridistribuire il software, anche a fini commerciali, nel rispetto delle condizioni della licenza. Le versioni modificate distribuite devono, tra gli altri obblighi, conservare gli avvisi applicabili, indicare modifiche e date e rispettare le condizioni relative alla licenza e al codice sorgente corrispondente.

Avviso originale conservato: © 2026 DomotikPro.it (Luca Pinelli).

I contributi di Fonkyup non sostituiscono i diritti e i crediti del progetto originale. Restano applicabili eventuali condizioni specifiche dei componenti di terze parti.

Il nome Aurora Glass e il marchio DomotikPro.it sono citati per identificare il progetto originale. Non vengono rivendicati diritti sui marchi né un’approvazione degli autori originali. Il nome pubblico della versione derivata è Luma Home.

Il software è fornito senza garanzia, nei limiti della licenza e della legge applicabile. Questa sezione è un riepilogo: per le condizioni complete consulta LICENSE.

Conserva senza modifiche il testo della GPL nel file LICENSE. Inserisci gli avvisi relativi al progetto e ai contributi nella documentazione e nei sorgenti, non nel testo della licenza.

---

Progetto originale: [DomotikPro.it](https://domotikpro.it) — Luca Pinelli.

Adattamento multilingue non ufficiale: Fonkyup.
