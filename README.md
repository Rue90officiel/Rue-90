# Rue 90 — site statique

Ce dossier est le site Rue 90 complet, prêt à être hébergé tel quel : `index.html`
à la racine, puis `boutique/`, `produit/`, `panier/`, `contact/`, `assets/`,
`404.html` et `.nojekyll`. Les 36 pages sont de vrais fichiers HTML (pré-rendus
puis hydratés) : recherche, filtres, tri, tiroir de navigation, sélecteur de
taille, personnalisateur de maillot et commutateur FR/EN fonctionnent sans
serveur.

## Publier sur GitHub Pages

> **Important : déployez le site à la RACINE du domaine.** Créez un dépôt nommé
> exactement `<votre-compte>.github.io` (par exemple `rue90.github.io`). Le site
> sera en ligne à l'adresse `https://<votre-compte>.github.io/` et tout
> fonctionne sans réglage.
>
> Un dépôt de projet (`https://<votre-compte>.github.io/rue-90/`) sert le site
> dans un sous-dossier : voir « Sous-dossier » plus bas avant de choisir cette
> option.

1. Créez le dépôt `<votre-compte>.github.io` sur GitHub, puis poussez **le
   contenu de ce dossier** (pas le dossier lui-même) :

   ```bash
   cd rue-90-site        # dossier décompressé
   git init && git add -A
   git commit -m "Rue 90 — site statique"
   git branch -M main
   git remote add origin https://github.com/<votre-compte>/<votre-compte>.github.io.git
   git push -u origin main
   ```

2. Sur GitHub : **Settings → Pages → Build and deployment**, source
   **Deploy from a branch**, branche **main**, dossier **/ (root)**. Enregistrez.

3. Après une minute, le site est en ligne à `https://<votre-compte>.github.io/`.

Le fichier `.nojekyll` est déjà présent : ne le supprimez pas (il empêche GitHub
de filtrer les fichiers du dossier `assets/`).

## Sous-dossier (dépôt de projet)

Le site utilise un routeur côté client. À la racine du domaine, rien à faire.
Dans un sous-dossier (`/rue-90/`), il faut reconstruire le site avec le préfixe
du dépôt, depuis `_source/` :

```bash
cd _source
bun install
RUE90_BASE_PATH=/rue-90/ bun run build:static
```

…puis republier le contenu de `static-dist/`. (Cette variante est en cours de
validation : préférez pour l'instant le déploiement à la racine ci-dessus.)

## Où vit le code source

Le dossier **`_source/`** contient le projet qui génère ce site
(TanStack Start + React + Vite + Tailwind) : `src/`, `public/`, `scripts/`,
`package.json`, `vite.config.static.ts` et les configurations. Pour modifier le
site :

```bash
cd _source
bun install
bun run build:static   # régénère static-dist/ et rue90-site.zip
```

- Catalogue (32 produits, prix en dollars canadiens) : `_source/src/data/products.ts`
- Textes français / anglais : `_source/src/lib/i18n.tsx`
- Design (noir, gris foncé, blanc) : `_source/src/styles/app.css`

## Ce qui ne marche pas dans la version statique

- Aucun achat : les boutons produit affichent « À venir » et la page panier est
  un avis « Panier — À venir », comme sur le site publié.
- Le formulaire « Nous Joindre » et l'infolettre sont des démonstrations locales
  (aucun envoi), identiques au site publié.
