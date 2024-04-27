# Projet IA

[![dernière version](https://git.unistra.fr/erken/projet-ia/-/badges/release.svg)](https://git.unistra.fr/erken/projet-ia/-/releases/permalink/latest)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit)](https://github.com/pre-commit/pre-commit)

Vous trouverez ici le [projet](https://git.unistra.fr/erken/projet-ia) pour l'UE [Intelligence Artificielle](https://mathinfo.unistra.fr/formations/licence/informatique/parcours-informatique-PR9-18123/cours-intelligence-artificielle-EN26110-18123-PR9) de la licence informatique de l'Université de Strasbourg. Cette UE fait partie du semestre L3IS6P de l'année académique 2023-24.

Voir le [sujet](projet.pdf) du projet pour plus de détails sur ce sur quoi se porte ce projet.

**Table des matières :**

[[_TOC_]]

## Étudiants

| NOM | Prénom | Groupes |
|:-|:-|:-|
| ERKEN | Efe | TD1-TP1 |
| MOULLA | Yanis | ... |

Année : L3IS6 Printemps 2024

## Documents internes

* [Compte-rendu](https://docs.google.com/document/d/1xnsNh7EBjIRRFsLjt1Mlp2BQCLEE34-JLoDGm8FQg-s/edit?usp=sharing)
* [Seafile partagé](https://seafile.unistra.fr/smart-link/b1c0df1f-dcdd-4da2-b4ba-ce51f6787ffc/)

## Environnement de développement

*Pour une utilisation en tant que développeur, un environnement dev*.

### Dépendances

Assurez vous d'être réglé avec les bonnes versions des dépendances de premier niveau dans la liste en dessous qui sont donc Git, Git LFS et Python. Les autres points (dépendances de deuxième niveau et encore) seront abordés plus en détails avec des instructions plus loin.

Cette liste indique les versions minimales recommandées ou des versions exactes (sur certains) des outils nécessaires pour travailler sur ce projet. Si vous ne respectez pas ces versions votre environnement de développement risque de ne pas fonctionner correctement. Mais surtout, vous serez en décalage avec le reste de l'équipe et vous risquez de rencontrer des problèmes lors de votre implémentation qui ne sera plus compatible avec le projet.

* [Git](https://git-scm.com/) récent
* [Git LFS](https://git-lfs.com/) récent
* [Python](https://www.python.org/) >= 3.8 stable (3.11.x recommandé)
  * Voir [requirements.txt](requirements.txt) pour les dépendances Python

### Étapes d'installation

#### Dépôt Git local

Assurez vous d'avoir une version récente de Git.

Veillez à utiliser vos identifiants GitLab Unistra dans votre dépôt local pour que les commits soient bien attribués à votre compte.

```sh
git clone git@git.unistra.fr:erken/projet-ia.git
cd projet-ia  # À partir de maintenant toutes les commandes depuis le répertoire racine du projet
git config --local user.name "NOM PRENOM"  # Utilisez votre nom sur GitLab Unistra
git config --local user.email "ernest@etu.unistra.fr"  # Utilisez votre email sur GitLab Unistra
```

Configurez votre éditeur de texte par défaut pour les messages de commit **si ce n'est pas déjà fait** :

```sh
git config --global core.editor ["vi", "vim", "nvim", "nano", "code --wait", "subl --wait"]  # Choisir votre éditeur préféré ou un de cette liste
```

#### Python

Python 3.8+ est le minimum absolu nécessaire pour ce projet. Python 3.11.x est recommandé. Python 3.11.3 est la version de référence pour ce projet.

Assurez vous d'avoir la version indiquée de Python. Si vous n'avez pas la bonne version de Python et que vous voulez gerer de multiples versions Python ou si installer la bonne version de Python s'avère difficile, vous pouvez jeter un œil à l'outil [pyenv](https://github.com/pyenv/pyenv).

L'utilisation d'un environnement virtuel est conseillé. Vous pouvez utiliser `pyenv`, `venv`, `virtuelenv` ou bien d'autres méthodes pour créer et gérer l'environnement virtuel comme vous voulez mais veillez à ne pas oublier de l'activer avant chaque fois que vous allez travailler sur le projet.

Ensuite, installez les dépendances Python (il se peut que `pip` ne soit pas correctement aliasé dans votre installation et que vous deviez le remplacer par `pip3`) :

```sh
pip install -r requirements.txt  # Installez les packages Python
```

##### Dépendances et hooks Git

Configurez les hooks Git (une fois Python est réglé) :

```sh
rm -rf .git/hooks  # Supprimez les hooks git par défaut
git lfs install
git config --local lfs.https://git.unistra.fr/erken/projet-ia.git/info/lfs.locksverify true
pre-commit install  # Installez les hooks git
pre-commit run -a  # Lancez les hooks git pour la toute première fois
```

## Astuces sur les hooks Git

Si à cause des git hooks, votre commit a été refusé après que vous avez renseigné votre message de commit, pas de panique c'est pas perdu, vous pouvez le récupérer et l'éditer pour le corriger en exécutant la commande suivante :

```sh
git commit -eF "$(git rev-parse --show-toplevel)/.git/COMMIT_EDITMSG"
```

Vous pouvez désactiver les hooks Git pour un commit en exécutant la commande suivante :

```sh
git commit --no-verify
```

Vous pouvez aussi sauter certains hooks `pre-commit` en spécifiant leur id dans `.pre-commit-config.yaml` dans vos commandes Git comme par exemple :

```sh
SKIP=black,check-yaml git commit

SKIP=nbqa-flake8,isort git push
```

Notez que les hooks Git sont là pour vous aider à écrire des commits propres et bien formatés. Essayez de n'ignorer les hooks qu'en cas de force majeure ou si vous venez déjà d'exécuter manuellement les hooks Git et tout s'est bien passé, et vous savez que rien n'a changé entre temps, pour ne pas relancer les hooks et perdre du temps quand vous savez déjà le résultat, vous pouvez les faire sauter. Mais puisqu'un certain nombre de ces hooks sont aussi lancé coté serveur, si vous les désactivez vous n'aurez pas la garantie que votre commit sera accepté par le serveur lors du CI et votre merge request peut être bloqué.
