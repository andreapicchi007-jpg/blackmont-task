# Blackmont Broker Task — messa online

Ci vogliono circa 15 minuti. Ti servono un account Supabase gratuito (database) e un account Vercel gratuito (hosting).

## 1. Database (Supabase)
1. Vai su supabase.com → **New project** (scegli la regione EU, ad esempio Frankfurt).
2. Apri **SQL Editor** e incolla tutto `schema.sql`. Prima di eseguirlo, modifica in fondo al file le email e i nomi del team (`admin` = chi scrive le task, `support` = chi le spunta). Poi premi **Run**.
3. Vai su **Authentication → Users → Add user → Create new user** e crea un utente per ogni persona, con la **stessa email** inserita nella tabella team e una password. Spunta *Auto Confirm User*.
4. Vai su **Project Settings → API** e copia **Project URL** e la chiave **anon public**.

## 2. Configurazione
Apri `config.js` e incolla i due valori:
```js
SUPABASE_URL: "https://xxxx.supabase.co",
SUPABASE_ANON_KEY: "eyJhbGciOi..."
```
La chiave anon è fatta per stare nel browser. Le regole di sicurezza nel database fanno sì che solo chi è nella tabella `team` possa vedere e modificare le task. **Non usare mai la chiave service_role.**

## 3. Online (Vercel)
- **Metodo veloce:** su vercel.com → **Add New → Project**, trascina la cartella `blackmont-task`, oppure caricala su un repo GitHub e importala. Framework: *Other*. Nessun build command.
- **Da terminale:** `npx vercel` dentro la cartella.

Avrai un indirizzo del tipo `blackmont-task.vercel.app`.

## Gestire il team
- **Nuovo membro:** aggiungi una riga nella tabella `team` (Table Editor) e crea il suo utente in Authentication.
- **Rimuovere un membro:** cancella la sua riga da `team`. Da quel momento non vede più nulla.
- **Cambiare ruolo:** modifica la colonna `role`.

## Prova senza database
Se `config.js` resta vuoto, aprendo `index.html` il sito parte in **modalità demo**: le task vengono salvate solo nel browser. È utile per vedere la grafica.
