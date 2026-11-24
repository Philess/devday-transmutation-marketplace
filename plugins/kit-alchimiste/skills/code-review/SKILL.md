---
name: code-review
description: "Règles de revue de code en français avec deux niveaux, [BLOQUANT] et [CONSEIL] : résultats faux, sécurité, perte de données, tests et checks qui ne prouvent rien, fichiers générés, conformité à une spec. À utiliser pour relire une pull request, une diff ou du code, ou quand on demande une revue."
---

# Revue de code

Rédige tes commentaires en français. Commence chaque commentaire par **[BLOQUANT]** ou par **[CONSEIL]**.

## Deux niveaux, pas plus

**[BLOQUANT]** est réservé à quatre cas :
- un résultat faux (calcul, filtre, agrégat, cas limite) ;
- une faille de sécurité, ou un secret dans le code ;
- une perte ou une corruption de données existantes, localStorage compris ;
- un nouveau mécanisme sans test qui échouerait s'il cassait.

**[CONSEIL]** couvre tout le reste : lisibilité, nommage, style, performance non critique. L'auteur corrige ou répond ; un conseil ne déclenche pas de nouveau tour de revue.

## Conformité à la spec

- Si la PR référence une spec dans `docs/specs/`, vérifie chaque point de « Comment on saura que ça marche » et de « Ce que ça ne doit pas casser ».
- Signale en [CONSEIL] toute modification qui sort du périmètre de la tâche.

## Règles du domaine

- Si le code touche aux ventes (montants, chiffre d'affaires, panier moyen, marge), applique aussi la skill `donnees-ventes` : une règle non respectée est un [BLOQUANT].

## Des tests et des checks qui prouvent quelque chose

- [BLOQUANT] Un test qui passerait encore si on annulait le changement.
- [BLOQUANT] Un test, une assertion ou une valeur attendue affaiblis, supprimés ou ignorés (`skip`, `only`, seuil relâché) pour faire passer la CI, sans justification dans la PR.
- [BLOQUANT] Une boucle d'assertions sur une liste dont la taille n'est pas vérifiée d'abord : sur zéro cas, le test passe toujours.
- [BLOQUANT] Un script ou un workflow qui masque un code de sortie : `commande | tail`, `|| true`, `continue-on-error` sur une étape de vérification.
- [CONSEIL] Un check qui n'indique pas combien d'éléments il a vérifiés.

## Fichiers générés

- [BLOQUANT] Une modification à la main d'un fichier produit par `scripts/generate-sales-data.mjs` : on régénère, on n'édite pas.

## Apprendre des erreurs

- Si une erreur de la PR risque de se reproduire, propose en [CONSEIL] la règle courte à ajouter dans `.github/instructions/` ou dans la skill concernée.
- Les fichiers d'instructions et les skills restent courts : chaque ligne coûte des tokens à chaque exécution.
