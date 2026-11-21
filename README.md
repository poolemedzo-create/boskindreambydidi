# Boskindreambydidi — boutique statique

Boutique HTML/CSS/JavaScript (aucun PHP ni SQL), prête à déployer sur GitHub Pages ou Vercel. Catalogue de démonstration, panier local, commande WhatsApp, page d'administration `/didi`.

## Démarrage rapide

- Ouvre `index.html` localement, ou déploie le dossier entier sur Vercel.
- Page admin : `/didi/`
- Identifiant initial (mode local) : `Didishop`
- Mot de passe initial (mode local) : `commande`
- WhatsApp : `221777562403` (format international sans +)

**Mode local :** l'administration sauvegarde catalogue et paramètres dans le `localStorage` du navigateur. Elle permet de créer/modifier/supprimer des produits, prix, promotions, stocks, catégories et images. Les produits de démonstration sont fictifs. Les changements ne se partagent pas entre visiteurs et appareils. Export/import JSON permet de sauvegarder ou transférer le catalogue.

## Déploiement Vercel

1. Extrais le ZIP.
2. Crée un dépôt GitHub et téléverse tous les fichiers et dossiers (la racine du dépôt doit contenir `index.html`, `assets/`, `didi/`).
3. Sur Vercel, `Add New → Project`, importe le dépôt.
4. Framework preset : **Other**. Build command : vide. Output directory : `.` (racine). Déploie.
5. La boutique sera sur ton domaine Vercel et l'admin à `/didi/`.

Le site est également compatible avec une ouverture locale via un serveur HTTP simple (Live Server par exemple). Les scripts ES modules peuvent être bloqués si tu ouvres le fichier par `file://` selon le navigateur.

## Images et produits

Les produits démo sont définis dans `assets/js/demo-products.js`. Dans l'administration, un produit peut recevoir une URL image ou un fichier image (redimensionné/compressé en JPEG). Pour garder un catalogue exportable léger, préfère les images de taille modérée. Les images importées dans le catalogue JSON peuvent rendre celui-ci volumineux.

## Synchronisation cloud facultative (Firebase — sans PHP/SQL)

Pour que les modifications effectuées dans `/didi` soient publiées pour tous les visiteurs, configure Firebase. La version statique ne peut pas écrire dans des fichiers du site hébergé, donc le mode local seul n'est pas partagé.

1. Crée un projet Firebase sur https://console.firebase.google.com/.
2. Ajoute une application Web et copie sa configuration dans `assets/js/config.js` (remplace les champs vides).
3. Active **Authentication → Email/Password**.
4. Dans Authentication, crée un compte admin avec l'adresse `admin@boskindreambydidi.com` et le mot de passe `commande` (l'adresse est un identifiant technique, pas besoin de boîte mail pour l'authentification email/password).
5. Active Firestore Database.
6. Copie les règles de `firebase-firestore.rules` dans Firestore → Rules. Pour une protection stricte, remplace `ADMIN_UID_A_REMPLACER` par l'UID du compte admin visible dans Authentication.
7. Redeploie sur Vercel. La connexion `/didi` utilisera Firebase Auth et la boutique lira le catalogue Firestore.

Dans le mode cloud, l'identifiant `Didishop` est traduit en email technique `admin@boskindreambydidi.com` pour Firebase Auth. Les identifiants initiaux ne sont pas un mot de passe de sécurité à conserver : change-le dans Firebase après la mise en place.

### Règles Firestore

Le fichier `firebase-firestore.rules` fourni autorise la lecture publique du catalogue/settings et restreint les écritures au UID de l'administrateur. Ne laisse pas les règles en mode test.

## Configuration boutique

Dans `/didi → Paramètres`, modifie le WhatsApp, nom et TikTok. En mode local, paramètres gardés dans le navigateur; en cloud, sauvegardés dans Firestore.

## Contenu

- `index.html` : boutique
- `didi/index.html` : administration
- `assets/css/` : styles
- `assets/js/app.js` : boutique, panier, checkout WhatsApp
- `assets/js/admin.js` : gestion catalogue/admin
- `assets/js/demo-products.js` : catalogue fictif de départ
- `assets/js/config.js` : configuration Firebase facultative
- `firebase-firestore.rules` : règles Firebase
