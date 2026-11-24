---
name: donnees-ventes
description: Règles du domaine pour les données de ventes (centimes USD, chiffre d'affaires, panier moyen, marge, boutique en ligne, localStorage). À utiliser pour écrire, modifier ou relire du code qui calcule, agrège, filtre ou affiche des montants, des commandes ou des ventes.
---

# Données de ventes : règles du domaine

Ces règles valent pour écrire le code comme pour le relire. Ne pas les respecter donne un résultat faux, donc un [BLOQUANT] en revue.

- Les montants des lignes de commande sont des entiers en **centimes USD**. Calcule et agrège en centimes entiers. Ne convertis en dollars (÷ 100, 2 décimales) qu'au moment d'afficher ou d'exporter.
- Ne mélange jamais centimes et dollars dans un même calcul ou une même comparaison. Un écart d'un facteur 100 en est le symptôme typique.
- Chiffre d'affaires d'une ligne = quantité × prix unitaire historique de la ligne. Jamais le prix catalogue actuel de l'album.
- Panier moyen = chiffre d'affaires ÷ nombre de commandes, sur le même périmètre filtré.
- La marge ne se calcule pas : les données ne contiennent pas les coûts. N'affiche aucune marge, même estimée.
- Une corrélation saisonnière n'est pas une causalité : aucun libellé ne doit l'affirmer.
- La boutique en ligne reste distinguable des magasins physiques dans tous les agrégats et tous les filtres.
- localStorage : préserve les données existantes et affiche clairement les erreurs de lecture, de validation ou d'écriture.
- L'application reste entièrement frontend : pas de backend, pas de service externe.

## Exemple

```ts
// Faux : prix catalogue actuel, et dollars mélangés aux centimes
const revenue = lines.reduce((sum, line) => sum + line.quantity * album.price / 100, 0)

// Juste : prix historique de la ligne, agrégé en centimes entiers, converti à l'affichage
const revenueCents = lines.reduce((sum, line) => sum + line.quantity * line.unitPrice, 0)
const revenueLabel = formatUsd(revenueCents / 100)
```
