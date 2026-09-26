# 🍷 Vinprovningen – GitHub Pages + Supabase

## 1. Skapa databasen
Skapa ett projekt på Supabase och kör hela `schema.sql` i **SQL Editor**.

## 2. Skapa admin
I Supabase: **Authentication → Users → Add user**. Skapa ett e-post/lösenord som du använder i Adminläget.

## 3. Koppla appen
Öppna `index.html` och ändra:

```js
const URL="YOUR_SUPABASE_URL",KEY="YOUR_SUPABASE_PUBLISHABLE_KEY";
```

till din Project URL och Publishable key (äldre projekt kan kalla den `anon`). Lägg **aldrig** service_role/secret key i filen.

## 4. GitHub Pages
Lägg `index.html` och `schema.sql` i root på `main`-branchen. GitHub → **Settings → Pages** → **Deploy from a branch** → `main` → `/ (root)` → Save.

GitHub Pages letar efter `index.html` i toppen av den valda publiceringsmappen.

## Funktioner
- Gemensam central databas för alla svar.
- Åtta deltagare: Pelle, Sanna, Nordborg, Katta, Fredrik, Anna, Johan, Karin.
- Tre viner, land, pris, smak och favorit.
- 1 poäng för rätt land och 1 poäng för rätt pris.
- Admin kan fylla i facit, låsa provningen och radera deltagarsvar.
- Resultatsidan visar Johans favorit och hur många andra som valde samma vin.
- Resultat publiceras till alla först när admin låser provningen.

## Säkerhet
Databasen använder Supabase Row Level Security. Deltagare kan skicka in svar men får inte läsa rådata från andra deltagare. Resultatet går via `get_results()` och blir publikt först efter låsning. Publishable/anon key är avsedd för frontend med RLS; service_role/secret key ska aldrig exponeras.
