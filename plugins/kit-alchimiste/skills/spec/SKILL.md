---
name: spec
description: Transforme un besoin exprimé à l'oral ou à l'écrit (réunion Teams, transcript, issue, échange) en spec markdown, puis en tâches ordonnées prêtes à confier à des agents. À utiliser quand on demande de cadrer un besoin, d'écrire une spec, de préparer ou de découper des tâches pour des agents, ou avant toute évolution non triviale.
---

# Spec : du besoin aux tâches pour les agents

Règle de base : pas de code sans spec écrite d'abord. Une demande floue produit du code plausible qui fait la mauvaise chose. Ici, tu produis la spec et le découpage, jamais le code.

## 1. Récupérer le besoin à la source

- Si le connecteur Work IQ est disponible, retrouve la réunion concernée (titre, date, participants) et lis son transcript. Sinon, utilise le fichier ou le texte fourni. Si aucune source n'est accessible, dis-le et demande-la : n'invente rien.
- Classe ce qui a été dit en trois catégories : **décidé**, **reporté**, **question ouverte**. Seul le décidé entre dans le périmètre.
- Reprends les critères de vérification formulés par les participants (« on recalcule un mois à la main ») : ce sont les meilleurs critères d'acceptation.

## 2. Confronter le besoin au code et aux données

- Lis les types, les contrats de données et les services concernés avant d'écrire. Ne modifie aucun fichier.
- Vérifie les unités et les formats réels : centimes ou unités, devise, fuseau horaire, prix historique ou prix courant.
- Pour chaque demande, indique si les données permettent d'y répondre. Une demande impossible devient une limite écrite dans la spec, jamais un calcul approximatif.
- Tranche les questions ouvertes que le code permet de trancher, en citant le fichier.

## 3. Écrire la spec

Suis `spec-template.md`, dans le dossier de cette skill. Les trois sections obligatoires doivent être vérifiables :

1. **Ce que ça fait** : le comportement attendu, du point de vue de l'utilisateur.
2. **Comment on saura que ça marche** : des contrôles concrets, par exemple une valeur de référence calculée indépendamment du code testé, ou un test qui échoue avant le changement et passe après. « Le build passe » n'est pas un critère.
3. **Ce que ça ne doit pas casser** : les comportements, données et parcours existants à préserver.

Ajoute ensuite le hors périmètre (avec sa raison), les hypothèses et au plus 3 questions restantes. Garde la spec concise ; référence les fichiers de contrat si leur contenu ne tient pas sur une page.

## 4. Découper en tâches pour les agents

- Une tâche = un agent = une PR, avec un seul objectif. Vise 2 à 5 tâches.
- **Développement en parallèle, intégration en pile.** Après validation humaine et obtention des décisions nécessaires, le coordinateur publie sur une branche `<sujet>/0-contrat` un **contrat partagé et figé** adapté au projet (types, signatures, interfaces ou squelettes nécessaires). Chaque tâche démarre de cette branche dans sa propre session et développe en parallèle contre ce contrat.
- Déclare les dépendances et l'ordre d'intégration. La première PR contient aussi le contrat et vise la branche cible du projet ; chaque PR suivante vise la branche de la PR précédente. Après le développement parallèle, rebases, vérifications et intégration se font séquentiellement, des fondations vers les couches dépendantes.
- **Un seul propriétaire par fichier.** Fournis une table de propriété couvrant les fichiers et leurs tests. Le coordinateur possède les fichiers partagés (contrat, configuration ou manifestes concernés) en phase 0 ; les agents ne modifient que leurs fichiers attribués. Si le contrat doit changer, l'agent s'arrête et demande une décision au coordinateur avant de reprendre.
- Pour chaque tâche, donne : l'objectif, les fichiers possédés, les dépendances, ce qui peut se faire en parallèle et ce qui attend le rebase, le critère d'acceptation et le test qui doit échouer avant le changement. Choisis les vérifications adaptées au projet.
- Rédige chaque tâche comme un prompt autonome. Un agent doit pouvoir l'exécuter sans lire cette conversation ; il commence par « Lis la spec `docs/specs/…` ».

## 4 bis. Décisions avant le lancement

- Toute règle que ni la source ni le code ne tranche devient une **décision à obtenir**, avec son responsable et l'endroit du contrat où elle sera consignée. Ne l'invente pas.
- Aucune session de développement ne démarre tant que les décisions nécessaires ne sont pas prises et consignées, que la spec n'est pas validée par un humain et que le contrat n'est pas publié et figé.

## 5. Livrer et s'arrêter

- Enregistre la spec dans `docs/specs/AAAA-MM-JJ-<sujet>.md`. Dans un projet Copilot, ajoute-la aussi à la Library du projet.
- Présente un résumé : le périmètre, le contrat, la propriété des fichiers, les tâches et leur ordre d'intégration, les limites et les décisions à obtenir.
- **Arrête-toi là.** Pose les décisions à obtenir et attends les réponses. Ne lance aucune session et ne crée ni branche ni PR tant qu'un humain n'a pas validé la spec. Sa relecture est l'étape qui rapporte le plus dans tout le flux.
