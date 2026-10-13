# Város-Kép társasházkezelő — Netlify + meglévő Supabase

Modern, mobilbarát React alkalmazás a korábban használt Supabase projekthez. A Supabase URL előre be van írva a `.env.example` fájlba. A publikus kulcsot neked kell bemásolnod.

## Fontos
Ez egy működő alkalmazás-alap és UI, de éles használat előtt ellenőrizni kell a meglévő Supabase adatbázisod pontos oszlopait és RLS-szabályait. A kód a `profiles`, `notices`, `works`, `reports` táblaneveket használja; a korábbi `owners`/`building_managers` kapcsolatok miatt a hibabejelentés beszúrása igényelhet sémához igazítást. Nem írjuk felül automatikusan a meglévő adatbázist.

## Helyi futtatás
1. Node.js 20+ telepítése.
2. Másold `.env.example` → `.env`, majd add meg a publikus Supabase kulcsot.
3. Terminál:
   ```bash
   npm install
   npm run dev
   ```
4. Build ellenőrzése: `npm run build`

## Netlify
- Töltsd fel GitHubra.
- Netlify → Add new site → Import an existing project.
- Build command: `npm run build`
- Publish directory: `dist`
- Netlify Environment variables:
  - `VITE_SUPABASE_URL` = `https://lrznbjhuebcylprtygpm.supabase.co`
  - `VITE_SUPABASE_ANON_KEY` = Supabase publikus anon/publishable kulcs
- Indíts deployt.

## Supabase Auth
Authentication → URL Configuration alatt állítsd be a Netlify URL-t és a helyi `http://localhost:5173/**` URL-t.

## Biztonság
Soha ne használd a `service_role`/secret kulcsot a böngészőben, `.env`-ben `VITE_` változóként vagy GitHubon. A kezelői jogosultságot megbízható adminisztrációból kell kiosztani, nem a kliens által módosítható user metadata alapján. Élesítés előtt teszteld, hogy a lakók csak a saját társasházuk adatait látják.
