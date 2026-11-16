# Plugins IA d'Ostra

Ce dépôt est la marketplace Claude Code d'Ostra. Il contient un plugin, `ostra`, qui branche Claude Code sur Ostra, la mémoire d'entreprise de votre organisation, et lui apprend à s'en servir. Il ne contient aucun secret : seulement l'adresse publique du connecteur d'Ostra et une skill.

## Ce que fait le plugin `ostra`

- Il déclare le connecteur MCP d'Ostra, `https://api.ostra-tech.fr/mcp`. Claude lit Ostra avec vos droits Ostra, dans une seule organisation : celle que vous choisissez à la connexion.
- Il ajoute la skill « travailler avec Ostra » : quand chercher dans Ostra, comment citer, ce que le connecteur ne fait pas.
- Il donne accès aux ressources d'Ostra, à joindre avec `@` : `ostra://organisation`, `ostra://referentiel` et `ostra://documents/<identifiant>`.
- Il donne accès à quatre prompts, à lancer avec `/` : préparer une réponse à un appel d'offres, faire le point sur un projet, vérifier une affirmation, échéances à venir.

## Prérequis

- Un compte Ostra, membre de l'organisation à consulter, et l'accès « depuis Claude ou ChatGPT » allumé pour cette organisation (Ostra le règle).
- Claude Code 2.1.275 ou plus récent, pour l'installation en une ligne.

## Installer dans Claude Code

```
/plugin install ostra --marketplace Ostra-Tech/ia-plugins
```

Ou, en deux temps :

```
/plugin marketplace add Ostra-Tech/ia-plugins
/plugin install ostra@ostra
```

Ensuite, ouvrez `/mcp`, choisissez `plugin:ostra:ostra`, puis « Authenticate ». Le navigateur s'ouvre sur Ostra : connectez-vous, choisissez l'organisation, acceptez. `claude mcp list` affiche alors `plugin:ostra:ostra … ✔ Connected`.

Premier essai : « Demande à Ostra ce que nous savons de <sujet> ».

Si Claude Code montre aussi un autre serveur Ostra (le connecteur « Ostra » de votre compte claude.ai), coupez-en un dans `/mcp` : sinon, Claude voit deux fois les mêmes outils.

## Lancer un prompt dans Claude Code

Claude Code coupe les arguments d'un prompt sur les espaces : seul le premier mot arriverait. Lancez donc le prompt sans argument, par exemple `/mcp__plugin_ostra_ostra__faire_le_point_projet`, puis collez votre texte quand Claude vous le demande. Dans un client qui présente un formulaire, le texte y passe en entier.

## Autre adresse

Le plugin se branche toujours sur la production. Pour une autre adresse (staging, stack locale), ajoutez un serveur à part, par exemple :

```
claude mcp add --transport http --scope local ostra-dev http://localhost:8000/mcp
```

Chaque adresse a sa propre connexion : Claude Code garde une autorisation par adresse. Coupez l'un des deux serveurs dans `/mcp`, sinon Claude voit deux fois les mêmes outils.

## Mettre à jour, désinstaller, révoquer

- Mettre à jour : `/plugin marketplace update ostra`, puis redémarrer Claude Code.
- Désinstaller : `/plugin uninstall ostra@ostra`.
- Retirer l'accès donné à Claude Code : dans Ostra, « Applications connectées ».

## Sans plugin : Claude Desktop, claude.ai, ChatGPT

Ces clients se branchent directement sur l'adresse du connecteur, sans ce plugin. La skill est propre à Claude Code ; la consigne essentielle (chercher dans Ostra dès qu'on le nomme) est portée par le connecteur lui-même.

L'adresse est `https://api.ostra-tech.fr/mcp`.

- claude.ai et Claude Desktop : Paramètres, Connecteurs, « Ajouter un connecteur personnalisé », avec cette adresse. « Se connecter » ouvre Ostra. Selon votre offre Claude, l'ajout peut être réservé aux administrateurs de l'espace.
- ChatGPT : activez le mode développeur, puis créez un connecteur avec cette adresse et l'authentification OAuth. ChatGPT se sert des outils `search` et `fetch`.

## Ce que le connecteur ne fait pas

- Il ne rédige pas : Claude rédige, avec les passages d'Ostra sous les yeux.
- Il ne lit que ce que vous pouvez lire dans Ostra, dans une seule organisation.
- Il ne supprime rien et ne va chercher aucune page web.
- Il ne dépose pas de document tant qu'aucun outil de dépôt n'est ouvert pour vous.

## Données

Ce que Claude lit dans Ostra part chez Anthropic, et chez OpenAI pour ChatGPT. C'est pourquoi l'accès est éteint par défaut et s'ouvre organisation par organisation. Ce que le plugin envoie à Ostra, outil par outil, est décrit dans [`plugins/ostra/README.md`](plugins/ostra/README.md) ; la politique de confidentialité d'Ostra est sur https://ostra-tech.fr/fr/legal/.

## Maintenir ce dépôt

Toute modification du plugin relève `version` dans `plugins/ostra/.claude-plugin/plugin.json` : les postes déjà installés gardent leur copie tant que cette valeur ne change pas. Le plugin est listé dans l'annuaire de Claude depuis `plugins/ostra` : `plugins/ostra/README.md` est la page que l'annuaire affiche, et les champs `documentationUrl`, `privacyPolicyUrl` et `supportUrl` de `plugin.json` sont lus par lui. Ne mettez pas de `version` dans `.claude-plugin/marketplace.json`. Avant de pousser : `claude plugin validate --strict .` et `claude plugin validate --strict ./plugins/ostra`.

## Licence

MIT, voir `LICENSE`.
