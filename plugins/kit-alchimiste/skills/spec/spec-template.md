# Spec — <titre>

| | |
|---|---|
| Source | <réunion, transcript ou issue : titre, date, participants> |
| Statut | Brouillon, à valider ; décisions à obtenir avant le lancement |
| Validée par | <nom de l'humain qui relit> |

## Contexte

<2 à 4 phrases : le problème métier, pour qui, et pourquoi maintenant.>

## 1. Ce que ça fait

- <comportement attendu, vu de l'utilisateur>

## 2. Comment on saura que ça marche

| Contrôle | Comment | Résultat attendu |
|---|---|---|
| <comportement attendu> | <vérification indépendante du code testé> | <résultat mesurable> |
| <nouveau comportement> | <test qui échoue avant le changement> | <passe après> |

## 3. Ce que ça ne doit pas casser

- <parcours, données ou comportement existant à préserver>

## Hors périmètre

| Demande | Raison |
|---|---|
| <demande impossible> | <données nécessaires indisponibles> |
| <demande reportée> | <raison du report> |

## Hypothèses

- <ce qu'on suppose faute d'information, et comment le vérifier>

## Questions ouvertes (3 maximum)

1. <question, à qui, et ce qui bloque sans réponse>

## Organisation : développement parallèle, intégration empilée

| Ordre | Tâche | Dépend de | Base de la PR |
|---|---|---|---|
| 1 | <fondation et contrat> | — | <branche cible du projet> |
| 2 | <couche suivante> | <dépendances> | Branche de la PR 1 |
| 3 | <couche suivante, si nécessaire> | <dépendances> | Branche de la PR 2 |

| Phase | Acteur | Contenu | Mode |
|---|---|---|---|
| 0 | Coordinateur | Après validation humaine et décisions, publier le contrat figé sur `<sujet>/0-contrat` | Avant lancement |
| 1 | Sessions des tâches | Développer et tester depuis le contrat dans leurs fichiers attribués | Parallèle |
| 2 | Sessions dans l'ordre de la pile | Rebase sur la couche parente, vérifications adaptées au projet, PR | Séquentiel |

La première PR inclut le contrat et vise la branche cible ; chaque PR suivante vise la branche précédente.

### Phase 0 — Contrat partagé

<Types, signatures, interfaces ou squelettes nécessaires, et chemins de leurs fichiers. Le contrat est figé avant le lancement : toute modification doit être demandée au coordinateur.>

### Propriété des fichiers

| Fichiers | Propriétaire |
|---|---|
| <spec, contrat et fichiers partagés concernés> | Coordinateur, en phase 0 |
| <fichiers de la tâche 1 et leurs tests> | Session 1 |
| <fichiers de la tâche 2 et leurs tests> | Session 2 |
| Tous les autres fichiers | Aucun : ne pas modifier |

## Tâches

### PR 1 — <titre>

**Prompt pour l'agent :** Lis la spec `docs/specs/<fichier>.md` depuis la branche `<sujet>/0-contrat`. <objectif unique, fichiers possédés, ce qu'il ne faut pas toucher.>
**Phase 1 (parallèle) :** <travail indépendant des autres tâches>
**Phase 2 (après rebase) :** <travail et vérifications dépendant de la couche parente, le cas échéant>
**Test qui doit échouer avant le changement :** <description>
**Critère d'acceptation :** <contrôle de la section 2>

### PR 2 et suivantes — <titre>

<Même structure pour chaque tâche.>

## Décisions à obtenir avant la phase 0

1. <règle non tranchée> : <responsable, blocage et endroit du contrat où consigner la décision>

Ne pas inventer ces règles : aucune session de développement ne démarre avant leur consignation, la validation humaine de la spec et la publication du contrat figé.
