## But rapide
Ce dépôt est un site statique (thème "Freelancer" de Start Bootstrap) — pas de build ni de dépendances node/py visibles. Les modifications portent essentiellement sur HTML/CSS/JS et les assets image.

## Vue d'ensemble (big picture)
- Fichiers HTML principaux à la racine : `index.html`, `portfolio.html`, `a_propos.html`, `contact.html` — ce sont les pages servies par GitHub Pages.
- CSS principal compilé : `css/styles.css` (contient Bootstrap + règles du thème). Les surcharges/custom sont dans `css/heading.css` et `css/body.css`.
- JS principal : `js/scripts.js` (comportements du thème : scroll, modales, navbar). Le site s'appuie sur jQuery + Bootstrap via CDN.
- Assets images : `assets/img/portfolio/*` et `assets/img/*.png`.

## Points opérationnels et workflows
- Pas de `package.json` ni tâche de build : pour tester localement ouvrez `index.html` dans un navigateur ou démarrez un serveur local :

  - Python (port 8000) : `python -m http.server 8000`
  - Ou utilisez l'extension Live Server de VS Code.

- Déploiement : GitHub Pages depuis la branche `main` (site statique).

## Conventions projet — ce qu'un agent doit respecter
- Ne pas modifier `css/styles.css` sauf pour corrections urgentes : ce fichier contient la version vendored/Bootstrap — préférez ajouter/éditer règles dans `css/body.css` ou `css/heading.css` pour les overrides.
- JS thème centralisé : les interactions sont dans `js/scripts.js` (Start Bootstrap). Évitez de dupliquer la logique JS sans vérifier les événements existants (ex : `.js-scroll-trigger`, `#mainNav`, modales `portfolio-modal`).
- Images du portfolio : optimisées pour les vignettes. Le code HTML impose via CSS inline une hauteur de 220px pour `.portfolio-item img` (voir `portfolio.html`) — utilisez `object-fit: cover` pour conserver l'apparence.

## Intégrations et points d'attention
- Le site charge les bibliothèques (jQuery, Bootstrap, Font Awesome, Bootstrap Icons) depuis des CDN dans les pages HTML. Vérifier la connectivité si un élément JS/CSS ne fonctionne pas.
- Référence à des scripts de formulaire de contact : `assets/mail/jqBootstrapValidation.js` et `assets/mail/contact_me.js` sont référencés dans les pages mais le répertoire `assets/mail` n'existe pas dans le dépôt actuel — les formulaires peuvent échouer localement/production tant que ces fichiers ne sont pas ajoutés ou remplacés (ex : intégrer une solution externe comme Formspree ou ajouter les fichiers manquants).

## Exemples concrets utiles
- Pour changer le style du titre principal : éditer `css/heading.css` (les h1/h2 héritent de `SB Heading`).
- Pour ajuster la grille du portfolio, modifier `portfolio.html` (les vignettes utilisent `.portfolio-item` et ouvrent des modales identifiées `#portfolioModalN`).
- Pour tweaks JS (scroll, collapse navbar) : `js/scripts.js` contient la logique ; rechercher `.js-scroll-trigger` et `navbarCollapse`.

## Règles d'édition recommandées pour un agent
1. Lire la page HTML ciblée (ex : `portfolio.html`) pour comprendre la structure DOM utilisée par les CSS/JS.
2. Préférer les ajouts dans `css/body.css` ou `css/heading.css` plutôt que d'éditer `css/styles.css` vendored.
3. Si vous ajoutez des JS tiers, préférez charger via CDN ou documenter l'ajout dans un nouveau fichier sous `js/` (ex : `js/custom.js`) et le référencer dans les pages.
4. Avant tout changement d'image, vérifier `assets/img/portfolio/` pour éviter les doublons et garder des images optimisées (taille raisonnable, webp/optimized PNG).

## Questions ouvertes / points à valider avec le mainteneur
- Confirmer la destination souhaitée pour la logique du formulaire de contact (ajouter les fichiers `assets/mail/*` vs utiliser un service externe).
- Voulez-vous externaliser Bootstrap/Font Awesome locaux au lieu des CDNs ?

Si une section est trop sommaire ou si vous souhaitez que j'ajoute des snippets de PR/commit types (ex : correction CSS précise), dites quelles pages/éléments je dois prioriser.
