# Ostra pour Claude

Ostra est la mémoire d'entreprise de votre organisation : contrats, procédures, réponses passées, dossiers de projet et références, indexés et consultables au même endroit. Ce plugin branche Claude sur Ostra, avec vos propres droits Ostra, et lui apprend quand chercher dans Ostra, comment citer ses sources et ce qu'il ne doit pas faire.

## Ce que contient le plugin

- **Le connecteur MCP d'Ostra**, à l'adresse `https://api.ostra-tech.fr/mcp`. C'est le seul serveur que le plugin contacte.
- **La skill « travailler avec Ostra »** : chercher dans Ostra avant de répondre sur l'organisation, citer chaque document par son titre et son lien, ne rien présenter comme venant d'Ostra qu'aucun passage ne dit, ne déposer ou n'enrichir que sur demande explicite.

Le plugin n'exécute aucun programme sur votre poste : ni hook, ni script, ni serveur local. Il ne lit ni vos fichiers ni vos variables d'environnement.

## Prérequis

Un compte Ostra, membre d'une organisation pour laquelle Ostra a allumé l'accès « depuis Claude ou ChatGPT ». Cet accès est éteint par défaut. L'écriture demande en plus l'option d'écriture de l'organisation et le rôle adéquat : contributeur ou administrateur pour déposer, administrateur pour le graphe et les fiches de connaissance.

## Installer

Dans Claude Code 2.1.275 ou plus récent :

```
/plugin install ostra --marketplace Ostra-Tech/ia-plugins
```

## Se connecter

Après l'installation, dans Claude Code : `/mcp`, choisir `plugin:ostra:ostra`, puis « Authenticate ». Le navigateur s'ouvre sur Ostra : connectez-vous, choisissez l'organisation, cochez les droits que vous accordez, acceptez. Claude ne lit alors que ce que vous pouvez lire dans Ostra, dans cette seule organisation.

## Ce que le plugin envoie à Ostra

Tout passe par le connecteur, après votre autorisation dans Ostra. Selon l'outil que Claude appelle, Ostra reçoit :

- **pour lire** : vos questions et termes de recherche, les identifiants des documents ou des entités à lire, et les filtres de la demande (type, état, dates, profondeur, pagination) ;
- **pour déposer**, seulement si votre organisation l'a ouvert et que vous avez coché « Déposer des documents » : le nom et le texte du document (200 000 caractères au plus) et sa visibilité ;
- **pour enrichir la connaissance**, seulement pour un administrateur qui l'a accepté : les noms, alias et liens des entités du graphe, leurs relations, les concurrents ajoutés, et les fiches de connaissance proposées (créées en brouillon, qu'une personne valide dans Ostra) ;
- **pour signaler une réponse** : la question, votre commentaire, le document visé et jusqu'à dix extraits en cause, que les administrateurs de l'organisation lisent dans Ostra.

Ostra traite vos questions avec les modèles d'IA de sa plateforme (Mistral AI par défaut) et conserve ce que vous déposez dans l'espace de votre organisation. Ce que Claude lit dans Ostra part chez Anthropic. Rien ne peut être supprimé par le connecteur. Vous retirez l'accès à tout moment dans Ostra, « Applications connectées ».

## Confidentialité

Politique de confidentialité d'Ostra, section 11 « La plateforme Ostra et ses connecteurs d'IA » : https://ostra-tech.fr/fr/legal/

## Support

jean-michel@ostra-tech.fr

## Licence

MIT, voir `LICENSE` à la racine du dépôt.
