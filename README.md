# labrassee-humeur

**L'humeur du boss** — vote anonyme client + slide TV cuisine + widget site.

Owner : Apollon-Marketing · Idée Cédric 2026-05-21.

## Pages

- `/` — page de vote mobile (scan QR → vote → feedback)
- `/tv` — slide TV cuisine plein écran (humeur live + QR permanent)
- `/widget` — bandeau iframable pour intégration `labrassee.cafe`

## Backend

Projet Supabase `xjlpttrziisldlclhsth` (`inventaire-labrassee`).

- Table `humeur_votes` — votes anonymes du jour (médiane = humeur officielle)
- Table `humeur_boss_etat` — toggle absent (Cédric depuis dashboard hub)
- Vue `humeur_boss_jour` — agrégats du jour
- Edge Function `humeur-vote` (POST) — insert vote, retourne stats à jour
- Edge Function `humeur-statut` (GET, cache 20s) — lecture publique

## Garde-fous

- 1 vote / device / jour (device_hash localStorage + UNIQUE en BD)
- Anonyme total (pas de courriel, pas d'auth)
- Données 7 jours rolling (fonction `humeur_cleanup_old_votes()` à brancher pg_cron)
- Logo Maïa visible partout
- QR omniprésent (slide TV, affiche, posts) → `humeur.labrassee.cafe` (DNS Joshua) ou `labrassee-humeur.vercel.app` (fallback)
- Déploiement **uniquement via git push** (jamais CLI Vercel)

## Ton

Autodérision assumée. L'humeur du boss = sujet de conversation au comptoir, pas plainte client.

## Échelle

| 0 🐻 Mode ours | 1 😤 Pas parlable | 2 ⚡ Trop speed | 3 😎 Cool | 4 🤩 Euphorique |
|---|---|---|---|---|
