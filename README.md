# Cartographie interactive — Restructuration Chaingy–Dambron

Application **statique** compatible GitHub Pages, construite dans la même arborescence, avec la **taxonomie identique**, les styles et la physique du réseau du modèle public `Zoruohorse/cartographies_celtic` (branche `main`, état novembre 2026). Deux vues complémentaires partagent les mêmes référentiels JSON.

## Installer dans un nouveau dépôt GitHub

1. Créer un dépôt vide (par exemple `cartographies_Chaingy_Dambron`) ; aucune création de dépôt n'est effectuée automatiquement par le ZIP.
2. **Extraire le ZIP** puis déposer **son contenu à la racine du dépôt**, pas le dossier parent et pas le fichier ZIP lui-même. `index.html` doit être voisin de `apps/`, `assets/`, `config/`, `data/`, `audit/` et `validate.py`.
3. Dans **Settings → Pages**, choisir **Deploy from a branch**, branche `main`, dossier `/(root)`. Une fois publié, visiter `https://<utilisateur>.github.io/<nom-du-depot>/`.
4. Pour une vérification locale, exécuter `python -m http.server 8000` à la racine, puis ouvrir `http://localhost:8000/`. Ne pas ouvrir `index.html` directement avec `file://` (les navigateurs bloquent souvent `fetch` des JSON).
5. Avant modification des données, exécuter `python validate.py` : l'attendu est **PASS**, sans doublons ni références cassées.

## Vues et parité avec Celtic

- `apps/cards/` : mêmes familles de filtres, affichage par cartes, dialogue de détail, recherche, synthèse des griefs, vigilances et liens documentaires ; les preuves **multiples** sont affichées.
- `apps/network/` : même interface, mêmes couleurs de type Fouju, même placement initial en couronnes, mêmes paramètres physiques (attraction, répulsion et attraction centrale), mêmes interactions (zoom, pan, drag, centrage, filtre, survol, surlignage et relations).
- **Adaptation nécessaire** : le modèle Celtic masque les acteurs sans `claim`. Ici ils restent visibles, avec le libellé *Position non documentée* et leurs preuves de **fonction**, sans leur attribuer artificiellement une position `neutral`.

## Fichiers métiers

| Chemin | Fonction |
|---|---|
| `data/actors.json` | Identités, catégories, rôles, preuves de fonction et éléments contextuels |
| `data/claims.json` | Positions explicites sur la **ligne RTE uniquement** (valeurs `favorable`, `opposed`, `neutral`) |
| `data/evidence.json` | Preuves, citations ou faits rapportés, identifiant de la source et ligne Excel |
| `data/relations.json` | Liens entre entités, avec preuves et certitude |
| `data/sources.json` | Ressources citées, URL, date de trouvaille, statut de qualification |
| `data/meta.json` | Caractéristiques techniques, chronologie, synthèses et vigilances documentées |
| `config/taxonomy.json` | Taxonomie **non modifiée** du dépôt Celtic |
| `audit/corpus-review.json` | Décision prise pour chacune des 50 ressources Excel, y compris exclusions et doublons |
| `audit/validation.json` | Résultat du contrôle du référentiel |

## Base documentaire et périmètre

- Source exclusivement : `Carto Chaingy-Dambron.xlsx`, feuille « Informations qualifiées », 50 ressources.
- Dernière **date de trouvaille** : **10 août 2026**. La date de trouvaille n'est **pas** systématiquement la date de publication.
- Les URL proviennent du fichier Excel ; aucun accès direct aux pages externes n'est revendiqué. Les URL `news.google.com/rss/...` sont marquées **agrégateurs**, et **ne constituent pas** des liens canoniques aux articles d'origine.
- Le projet central est la ligne **RTE Chaingy–Dambron**. Le projet de batteries **Enertrag à Dambron** est identifié comme projet *distinct*, sans transfert des positions ou responsabilités.
- L'article « Les Ormes » (Vienne, 86) est un **faux positif** pour Ormes (Loiret, 45) et n'entre pas dans les entités.
- Un résultat électoral n'est **pas** une preuve de position sur la ligne. Les fonctions de maire non confirmées par le document sont signalées comme telles.
- Deux prévisions de démarrage de travaux coexistent (2028 et juin 2027). La DUP définitive et la puissance du projet en MW ne sont **pas** établies par ce corpus.
- Les données budgétaires municipales du tableur sont **exclues** des coûts du projet électrique : elles ne financent pas nécessairement RTE.

## Mettre à jour

Ne modifier que les objets ayant une preuve explicite ; préserver les identifiants, attribuer des nouveaux IDs séquentiels, mettre plusieurs preuves documentaires lorsque disponibles et exécuter `python validate.py`. Les synthèses dans `meta.json` affichent leurs pièces justificatives dans la vue cartes.
