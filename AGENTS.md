# AGENTS.md — Ninja Creami Tracker

Consignes pour les agents de code (Claude Code, Codex, Cursor…). Interface en **français**.

## Le projet en bref
Application web d'une seule page pour suivre des recettes de glaces Ninja Creami : ingrédients disponibles (« frigo »), recettes réalisables, préparations en cours, notes et étoiles, mode sombre.

- Tout est dans **`index.html`** (HTML, CSS et JavaScript en ligne). Aucune dépendance, aucun build, aucun serveur.
- Pour tester : ouvrir `index.html` dans un navigateur.

## Organisation du fichier
- `<style>` : variables CSS dans `:root` et `body.dark-mode`. Réutiliser ces variables plutôt que des couleurs en dur.
- `<script>` : données (`ingredientsMap`, `recipesData`), puis fonctions par zone (`renderFrigo`, `updateRecipes`, `createRecipeCard`, `rateRecipe`, `markPrepared`, `markConsumed`, `archiveRecipe`, `toggleDarkMode`…). Point d'entrée : `init()`.

## Données et stockage
- L'état est sauvegardé dans le `localStorage` du navigateur : clé `ninjaCreami` (`selectedIngredients`, `recipes`) et clé `darkMode`.
- **Piège** : au chargement, `recipes = data.recipes || recipesData`. Une recette ajoutée dans `recipesData` n'apparaît donc pas chez un utilisateur qui a déjà une sauvegarde. Si on ajoute ou modifie des recettes, prévoir une fusion (par identifiant de recette) entre la sauvegarde et `recipesData`, sans perdre les notes, étoiles et préparations de l'utilisateur.
- Ne jamais changer la forme des données sauvegardées sans gérer les anciennes sauvegardes.

## Règles
- Garder un **fichier unique** sans dépendance externe, sauf demande explicite.
- L'interface doit rester utilisable sur téléphone et en mode sombre.
- **Dépôt public** : ne rien committer de personnel (clé, email, donnée privée).
