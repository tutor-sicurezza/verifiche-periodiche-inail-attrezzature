# Verifiche periodiche INAIL/ASL — Attrezzature di lavoro (Allegato VII D.Lgs 81/08)

Dataset JSON delle attrezzature di lavoro sottoposte a verifica periodica obbligatoria ai sensi dell’**Allegato VII del D.Lgs 81/08** e del **D.M. 11 aprile 2011**, con periodicità (anni) della prima verifica e delle verifiche successive, autorità competente (INAIL per la prima verifica, ASL/ARPA o soggetto abilitato per le successive), riferimenti normativi.

> **English summary** — JSON dataset of work equipment subject to mandatory periodic inspections under Annex VII of Italian Legislative Decree 81/2008 and Ministerial Decree 11/04/2011. Includes inspection frequency (years), competent authority (INAIL for first inspection, regional health/environmental agency for subsequent ones), and regulatory references. Useful for compliance dashboards, maintenance scheduling, and asset-management systems in Italy.

## Cosa contiene

- `data/attrezzature-allegato-vii.json` — elenco delle attrezzature dell’Allegato VII con: categoria, tipologia, periodicità prima verifica, periodicità verifiche successive, soggetto competente, eventuali note (settori specifici, soglie tecniche), riferimento normativo.
- `data/scadenze-tipiche.json` — tabella sintetica machine-readable delle scadenze più frequenti per attrezzature di uso comune (carriponti, PLE, gru a torre, ascensori da cantiere, generatori di vapore, recipienti a pressione, ecc.).

## Tabella sintetica

| Attrezzatura | Periodicità verifiche successive | Autorità |
|--------------|----------------------------------|----------|
| Carriponti / gru fisse | 1 anno | ASL/ARPA o soggetto abilitato |
| Gru a torre per edilizia | 1 anno | ASL/ARPA o soggetto abilitato |
| Autogru, gru su autocarro | 1 anno | ASL/ARPA o soggetto abilitato |
| PLE (piattaforme elevabili) | 1 anno | ASL/ARPA o soggetto abilitato |
| Ascensori/montacarichi da cantiere | 1 anno | ASL/ARPA o soggetto abilitato |
| Ponti sospesi / argani | 2 anni | ASL/ARPA o soggetto abilitato |
| Idroestrattori centrifughi | 2 anni | ASL/ARPA o soggetto abilitato |
| Generatori di vapore d’acqua | 2 anni | ASL/ARPA o soggetto abilitato |
| Forni industria chimica | 2 anni | ASL/ARPA o soggetto abilitato |
| Recipienti liquidi surriscaldati ≠ acqua | 3 anni | ASL/ARPA o soggetto abilitato |
| Riscaldamento acqua surriscaldata (>110 °C) | 3 anni | ASL/ARPA o soggetto abilitato |
| Recipienti gas compressi (PS·V > 50 bar·L) | 4 anni (funzionamento) | ASL/ARPA o soggetto abilitato |
| Tubazioni vapore/gas cat. >I PED | 5 anni (funzionamento) | ASL/ARPA o soggetto abilitato |
| Generatori calore impianti centrali (>116 kW, <110 °C) | 5 anni | ASL/ARPA o soggetto abilitato |

Per i valori puntuali e le note tecniche vedi `data/attrezzature-allegato-vii.json`.

## Esempio uso

```ts
import data from "./data/scadenze-tipiche.json";

const annuali = data.scadenze.filter((s) => s.periodicita.startsWith("1 anno"));
console.log(`${annuali.length} categorie con verifica annuale`);
```

```python
import json
with open("data/attrezzature-allegato-vii.json") as f:
    data = json.load(f)

ple = next(a for a in data["attrezzature"] if "PLE" in a["tipologia"])
print(ple["verifica_successiva"]["periodicita_anni"])  # 1
```

## Principi normativi

- **Prima verifica:** INAIL entro 60 giorni dalla richiesta del datore di lavoro. Trascorso il termine, il datore può rivolgersi a soggetti pubblici o privati abilitati iscritti nell’elenco del Ministero del Lavoro (D.D. 22/05/2012 e s.m.i.).
- **Verifiche successive:** ASL/ARPA territorialmente competenti entro 30 giorni dalla richiesta. Trascorso il termine, il datore può rivolgersi ai soggetti abilitati.
- **Onere economico:** a carico del datore di lavoro secondo le tariffe del D.M. 11/04/2011.

## Disclaimer

Dataset informativo: le periodicità qui riportate si riferiscono al testo dell’Allegato VII del D.Lgs 81/08 come da ultimo aggiornato e alle circolari INAIL applicabili. Per applicazioni operative consultare sempre la versione vigente del decreto su Normattiva, le schede tecniche INAIL e le indicazioni dell’ASL/ARPA competente.

## Risorse correlate

Per il calcolo automatico delle scadenze formazione operatori (carrelli elevatori, PLE, gru, trattori, escavatori, ecc.) ex Accordo Stato-Regioni 22/02/2012 vedi il [calcolatore di 123Formazione](https://123formazione.com/strumenti/calcolatore-scadenze).

## Licenza

- Dati (`data/`): **CC BY-SA 4.0** — vedi `LICENSE-CC-BY-SA`.
- Eventuale codice/snippet di esempio: **MIT** — vedi `LICENSE-MIT`.

## Citazione

Vedi `CITATION.cff`.
