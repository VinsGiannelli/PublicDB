# PublicDB — Salesforce Dashboard

Repository pubblico di distribuzione dello snapshot JSON per la dashboard Salesforce.

## Endpoint di lettura

Quando il file `dashboard.json` sarà pubblicato nel branch `main`, il contenuto sarà leggibile via GET da:

`https://raw.githubusercontent.com/VinsGiannelli/PublicDB/main/dashboard.json`

Dopo aver attivato GitHub Pages in **Settings → Pages → Build and deployment → Deploy from a branch → main / (root)**, l'indirizzo statico sarà:

`https://vinsgiannelli.github.io/PublicDB/dashboard.json`

**Nota:** questi URL non devono essere considerati attivi finché il file non è realmente presente e la relativa distribuzione non è verificata.

## Contratto del JSON

Oggetto radice completo, senza wrapper:

```json
{
  "generatedAt": "2026-10-22T00:00:00.000Z",
  "timezone": "Europe/Rome",
  "games": {
    "status": "ok",
    "title": "Giochi gratuiti e inclusi",
    "items": []
  },
  "sports": {
    "status": "ok",
    "title": "Eventi",
    "period": {
      "from": "2026-10-22",
      "to": "2026-11-05"
    },
    "items": []
  }
}
```

L'esempio sopra è illustrativo e NON è uno snapshot reale: non pubblicarlo come `dashboard.json`.

## Regole di aggiornamento

- Pubblicare quotidianamente l'intero snapshot, con entrambe le sezioni `games` e `sports`.
- Calcolare da zero la finestra temporale nel fuso Europe/Rome: oggi → oggi + 14 giorni inclusi.
- Validare schema, fonti, date, link, categorie, blacklist e regole di offerta prima di sovrascrivere il file.
- Pubblicare aggiornando il file sulla branch `main`, usando la SHA attuale per evitare conflitti.
- Verificare la presenza di `generatedAt` aggiornato e dei dati attesi nella risposta GET.
- Se l'estrazione fallisce gravemente, preservare il precedente snapshot valido invece di sostituirlo con dati inventati o vuoti.
