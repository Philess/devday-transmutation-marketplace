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

Ajoute ensuite le hors périmètre (avec sa raison), les hypothèses et au plus 3 questions restantes. La spec tient sur une page.

## 4. Découper en tâches pour les agents

- Une tâche = un agent = une PR, avec un seul objectif. Vise 2 à 5 tâches.
- Déclare les dépendances. Les tâches dépendantes forment une pile de PR (stacked PRs), des fondations vers l'interface.
- Deux tâches qui touchent les mêmes fichiers ne tournent pas en parallèle : fusionne-les ou empile-les.
- Pour chaque tâche, donne : l'objectif, les fichiers ou dossiers concernés, ce dont elle dépend, le critère d'acceptation et le test qui doit échouer avant le changement.
- Rédige chaque tâche comme un prompt autonome. Un agent doit pouvoir l'exécuter sans lire cette conversation ; il commence par « Lis la spec `docs/specs/…` ».

## 5. Livrer et s'arrêter

- Enregistre la spec dans `docs/specs/AAAA-MM-JJ-<sujet>.md`. Dans un projet Copilot, ajoute-la aussi à la Library du projet.
- Présente un résumé : le périmètre, les tâches dans l'ordre, les limites et les questions.
- **Arrête-toi là.** Ne lance aucune session et ne crée ni branche ni PR tant qu'un humain n'a pas validé la spec. Sa relecture est l'étape qui rapporte le plus dans tout le flux.
