# Marketplace « for-the-people »

Marketplace d'exemple pour le DevDay : distribuer des plugins, skills et serveurs MCP aux développeurs, installables depuis la **GitHub Copilot app** ou la **Copilot CLI**.

## Contenu

```text
.github/plugin/marketplace.json     catalogue « for-the-people »
plugins/kit-alchimiste/
├── plugin.json                     nom, description, version 1.1.0
├── mcp.json                        Work IQ (optionnel)
└── skills/
    ├── spec/                       SKILL.md et spec-template.md
    ├── code-review/                règles [BLOQUANT] et [CONSEIL]
    └── donnees-ventes/             règles du domaine ventes
```

| Skill | Rôle |
|---|---|
| `spec` | Du besoin (transcript, issue, échange) à une spec vérifiable, puis à des tâches ordonnées pour des agents. S'arrête avant tout code. |
| `code-review` | Revue en français à deux niveaux : **[BLOQUANT]** (résultat faux, sécurité, perte de données, test qui ne prouve rien) et **[CONSEIL]**. |
| `donnees-ventes` | Règles du domaine : centimes USD, prix historique, panier moyen, pas de marge, boutique en ligne distincte, localStorage. |

## Installer

### Depuis la Copilot app

1. **Customize** dans la barre latérale, puis le réglage des marketplaces à côté du sélecteur de marketplace.
2. Ajouter `Philess/devday-transmutation-marketplace`.
3. Chercher **kit-alchimiste** dans **Browse**, puis **Install**.

### Depuis la CLI

```sh
copilot plugin marketplace add Philess/devday-transmutation-marketplace
copilot plugin install kit-alchimiste@for-the-people
```

Mise à jour après une nouvelle version : `copilot plugin marketplace update for-the-people`, puis `copilot plugin update kit-alchimiste`.

## Work IQ (optionnel)

`mcp.json` déclare le serveur MCP [Work IQ](https://github.com/microsoft/work-iq) (`npx -y @microsoft/workiq@latest mcp`, Node.js requis). La skill `spec` s'en sert pour lire le transcript d'une réunion Teams.

Sans accès à Work IQ, désactive ce serveur (`copilot mcp` ou l'onglet MCP de **Customize**) : la skill `spec` travaille alors à partir d'un fichier texte ou d'un texte fourni.

## Ajouter ou modifier une skill

1. Créer `plugins/kit-alchimiste/skills/<nom>/SKILL.md` (le `name` du frontmatter est le nom du dossier).
2. Mettre à jour `version` dans `plugins/kit-alchimiste/plugin.json` et dans `.github/plugin/marketplace.json`.
3. Pousser sur `main`, puis lancer la mise à jour côté client.

Les plugins suivent le format [Agent Plugins 1.0](https://github.com/agentplugins/agent-plugins-spec) : `plugin.json` à la racine du plugin, skills dans `skills/`, MCP dans `mcp.json`.

## Licence

[MIT](LICENSE)
