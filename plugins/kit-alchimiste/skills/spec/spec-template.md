# Spec — <titre>

| | |
|---|---|
| Source | <réunion, transcript ou issue : titre, date, participants> |
| Statut | Brouillon, à valider |
| Validée par | <nom de l'humain qui relit> |

## Contexte

<2 à 4 phrases : le problème métier, pour qui, et pourquoi maintenant.>

## 1. Ce que ça fait

- <comportement attendu, vu de l'utilisateur>

## 2. Comment on saura que ça marche

| Contrôle | Comment | Résultat attendu |
|---|---|---|
| <ex. : CA de mars 2025> | <recalcul indépendant à partir des données brutes> | <identique au centime> |
| <ex. : nouveau calcul> | <test qui échoue avant le changement> | <passe après> |

## 3. Ce que ça ne doit pas casser

- <parcours, données ou comportement existant à préserver>

## Hors périmètre

| Demande | Raison |
|---|---|
| <ex. : marge> | <les données ne contiennent pas les coûts> |
| <ex. : export> | <reporté au prochain point> |

## Hypothèses

- <ce qu'on suppose faute d'information, et comment le vérifier>

## Questions ouvertes (3 maximum)

1. <question, à qui, et ce qui bloque sans réponse>

## Tâches

| # | Tâche | Fichiers | Dépend de | Critère d'acceptation |
|---|---|---|---|---|
| 1 | <fondation> | <dossiers> | — | <contrôle de la section 2> |
| 2 | <…> | <…> | 1 | <…> |
| 3 | <…> | <…> | 2 | <…> |

### Tâche 1 — <titre>

**Prompt pour l'agent :** Lis la spec `docs/specs/<fichier>.md`. <objectif unique, fichiers concernés, ce qu'il ne faut pas toucher.>
**Test qui doit échouer avant le changement :** <description>
**Critère d'acceptation :** <description>
