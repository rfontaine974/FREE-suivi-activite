# Suivi-d-intervention — Déploiement GitHub + Vercel

Ce dépôt contient une application front-end statique (`index.html`) pour le suivi des ordres de travaux.

Pré-requis
- Un compte GitHub
- Un compte Vercel (connecté à votre compte GitHub)

Étapes recommandées pour déployer sur GitHub + Vercel

1) Préparer l'URL du backend (Google Apps Script)

- Si vous avez un script Apps Script qui expose les données, récupérez l'URL de déploiement (format `https://script.google.com/macros/s/XXXX/exec`).
- Créez un fichier `config.js` à la racine du projet (ne pas committer si privé) ou copiez `config.example.js` et mettez-y l'URL :

```javascript
// config.js (exemple)
window.__CONFIG__ = { WEB_APP_URL: 'https://script.google.com/macros/s/XXXXX/exec' };
```

2) Initialiser Git (si pas déjà fait) et pousser vers GitHub

Ouvrez PowerShell et exécutez :

```powershell
cd "c:\Users\rfont\Documents\GitHub\Suivi-d-intervention"
git init
git add .
git commit -m "Prepare project for Vercel deploy"
git branch -M main
git remote add origin https://github.com/<votre-username>/Suivi-d-intervention.git
git push -u origin main
```

Remplacez `<votre-username>` par votre nom d'utilisateur GitHub.

3) Déployer sur Vercel

- Connectez-vous sur https://vercel.com, cliquez sur **New Project**, puis **Import Git Repository**.
- Sélectionnez le repo `Suivi-d-intervention` et importez.
- Vercel détectera une application statique; gardez les valeurs par défaut.

4) Variables d'environnement et `config.js`

- Pour que le front appelle votre Apps Script, vous pouvez soit :
  - Commiter un `config.js` (pas recommandé pour URLs privées).
  - Ou ajouter l'URL dans Vercel et injecter la variable via un build step. Pour ce dépôt simple (sans builder), la méthode la plus directe est de créer `config.js` contenant `window.__CONFIG__`.

5) Déploiement automatique

- À chaque push sur `main`, Vercel reconstruira et redéployera automatiquement.

Support & Sécurité
- Ne commitez pas d'URL sensibles ou de clés dans le dépôt public.
- Si vous voulez une intégration plus avancée (serverless, variables injectées côté build), je peux ajouter un petit `package.json` et un script de build qui injecte les variables d'environnement de Vercel au moment du build.
