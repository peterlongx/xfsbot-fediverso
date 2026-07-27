# xfsbot-fediverso â€” elenco di riserva

Questo deposito contiene **un solo file utile**: [`fediverso-bootstrap.json`](fediverso-bootstrap.json).

## A cosa serve

Le istanze di **XFS Bot** si trovano fra loro da sole: ogni dominio pubblica
`GET /api/v1/fed/bootstrap` con la lista dei domini che conosce, e una installazione
nuova parte dai semi compilati nel binario, ne contatta uno, e da lÃ¬ la scoperta
prosegue in autonomia.

Questo file entra in gioco **solo se tutti i domini di fabbrica sono irraggiungibili
nello stesso momento**. Ãˆ un paracadute, non un registro:

* nessuno deve iscriversi qui per entrare nella rete;
* chi compare in questo elenco non ha alcun privilegio;
* appena il bot raggiunge **un solo** dominio vivo, questo file smette di contare.

## Come si usa

Nel `.env` dell'istanza:

```
FEDIVERSE_BOOTSTRAP_URL=https://raw.githubusercontent.com/peterlongx/xfsbot-fediverso/main/fediverso-bootstrap.json
```

Si possono indicare piÃ¹ indirizzi separati da uno spazio. Con `no`, `0`, `none` oppure
`off` il recupero viene disattivato del tutto. In alternativa si usa l'impostazione
`fediverse_bootstrap_url` dal pannello.

Il file viene letto una volta a 20 secondi dall'avvio e poi ogni 24 ore, con un tetto
di 512 KB e 500 voci.

## Formato

```json
{
  "protocol": 1,
  "software": "XFS Bot",
  "updated": "2026-07-27T19:10:00Z",
  "domains": [
    { "domain": "https://esempio.tld", "name": "Nome leggibile" }
  ]
}
```

Sono accettate anche due forme piÃ¹ povere: un array diretto di oggetti, oppure un
array di sole stringhe con gli indirizzi.