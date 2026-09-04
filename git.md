# Git — Guide pratique & workflow réel

# Introduction

## Qu’est-ce que Git ?

Git est un système de versionning distribué.

Il permet de :

* sauvegarder l’historique d’un projet
* revenir à des versions précédentes
* travailler en équipe
* gérer plusieurs fonctionnalités en parallèle
* éviter de perdre du code

Git fonctionne localement sur votre machine, mais peut également être connecté à des plateformes distantes comme :

* GitHub
* GitLab
* Bitbucket

---

# Git ≠ GitHub

## Git

Le logiciel de versionning.

## GitHub

Une plateforme hébergeant des dépôts Git distants.

---

# Concepts importants

## Repository

Un repository (repo) est un projet Git.

Il existe :

* des dépôts locaux
* des dépôts distants

---

## Commit

Un commit est un snapshot du projet à un instant donné.

Chaque commit possède :

* un identifiant unique (SHA)
* un auteur
* une date
* un message

---

## Branche

Une branche permet de travailler sur une fonctionnalité sans impacter la branche principale.

Exemple :

```txt
main
 └── feature/login
```

---

## HEAD

HEAD représente l’endroit actuel dans l’historique Git.

---

# Initialiser un projet

## Initialiser Git

```bash
git init
```

Crée un dépôt Git dans le dossier courant.

---

## Cloner un projet existant

```bash
git clone URL_DU_REPO
```

Télécharge un dépôt distant.

---

# Configuration Git

## Configurer son identité

```bash
git config --global user.name "Votre Nom"
git config --global user.email "mail@example.com"
```

---

# Vérifier l’état du projet

```bash
git status
```

Affiche :

* fichiers modifiés
* fichiers staged
* fichiers non suivis

---

# Les états d’un fichier

## Untracked

Fichier non suivi par Git.

---

## Staged

Fichier ajouté au prochain commit.

---

## Committed

Fichier enregistré dans l’historique Git.

---

## Modified

Fichier modifié depuis le dernier commit.

---

# Ajouter des fichiers

## Ajouter un fichier

```bash
git add fichier.js
```

## Ajouter tous les fichiers

```bash
git add .
```

---

# Créer un commit

```bash
git commit -m "add authentication system"
```

Important : les messages de commit doivent être clairs.

---

# Bons messages de commit

## Mauvais

```txt
fix
test
working
```

## Bons

```txt
fix login validation bug
add payment system
refactor navbar component
```

---

# Historique Git

## Historique simple

```bash
git log
```

## Historique compact

```bash
git log --oneline
```

## Historique visuel

```bash
git log --oneline --graph --all
```

---

# Voir les différences

## Modifications non staged

```bash
git diff
```

## Modifications staged

```bash
git diff --staged
```

---

# Restaurer des modifications

## Retirer du staging

```bash
git restore --staged fichier.js
```

## Annuler les modifications locales

```bash
git restore fichier.js
```

Les changements seront perdus.

---

# .gitignore

Permet d’ignorer certains fichiers ou dossiers.

Exemple :

```txt
node_modules/
.env
dist/
```

Très utile pour :

* dépendances
* builds
* fichiers secrets

---

# Les branches

## Voir les branches

```bash
git branch
```

---

## Créer une branche

```bash
git branch feature/login
```

---

## Créer et changer de branche

```bash
git checkout -b feature/login
```

---

## Changer de branche

```bash
git checkout main
```

---

# Workflow conseillé

1. Créer une branche
2. Développer la feature
3. Faire plusieurs commits propres
4. Merge ou Pull Request
5. Résoudre les conflits si nécessaire

---

# Merge

## Fusionner une branche

```bash
git merge feature/login
```

Fusionne les commits de la branche indiquée dans la branche actuelle.

---

# Les conflits Git

Un conflit apparaît lorsque deux branches modifient la même partie du code.

Git ajoute alors des marqueurs :

```txt
<<<<<<< HEAD
code actuel
=======
code venant du merge
>>>>>>> feature/login
```

Une fois le conflit résolu :

```bash
git add .
git commit
```

---

# Cherry-pick

```bash
git cherry-pick SHA_DU_COMMIT
```

Permet de copier un commit précis sur une autre branche sans merge toute la branche.

Très utile pour :

* récupérer un fix urgent
* récupérer un commit oublié
* corriger une erreur rapidement

---

# Tags

## Créer un tag

```bash
git tag v1.0
```

## Voir les tags

```bash
git tag
```

Les tags servent généralement à marquer des versions importantes.

---

# Dépôts distants

## Ajouter un dépôt distant

```bash
git remote add origin URL_DU_REPO
```

---

## Voir les dépôts distants

```bash
git remote -v
```

---

# Push

## Premier push

```bash
git push -u origin main
```

## Push suivant

```bash
git push
```

Envoie les commits vers le dépôt distant.

---

# Pull

```bash
git pull
```

Récupère les modifications distantes et les fusionne.

---

# Modifier le dernier commit

## Modifier le message

```bash
git commit --amend -m "nouveau message"
```

## Ajouter des fichiers oubliés

```bash
git add fichier.js
git commit --amend
```

---

# Stash

## Sauvegarder temporairement les changements

```bash
git stash
```

## Restaurer les changements

```bash
git stash pop
```

Très utile lorsqu’on doit changer rapidement de branche sans commit.

---

# Revert

```bash
git revert SHA
```

Annule un commit proprement en créant un nouveau commit inverse.

Safe pour le travail en équipe.

---

# Reset

## Soft reset

```bash
git reset --soft HEAD~1
```

Supprime le dernier commit mais garde les fichiers staged.

---

## Hard reset

```bash
git reset --hard HEAD~1
```

Supprime :

* les commits
* les modifications locales

Commande destructive.

---

# Push forcé

## Force push

```bash
git push --force
```

Écrase l’historique distant.

Dangerous en équipe.

---

## Version plus safe

```bash
git push --force-with-lease
```

Force le push uniquement si personne n’a modifié la branche entre temps.

---

# Detached HEAD

```bash
git checkout SHA_DU_COMMIT
```

Permet de revenir temporairement sur un ancien commit.

Git affiche alors :

```txt
detached HEAD
```

Cela signifie qu’on ne travaille plus directement sur une branche.

---

# Commandes les plus utilisées au quotidien

```bash
git status
git add .
git commit -m ""
git pull
git push
git checkout -b
git merge
git log --oneline --graph --all
```

---

# Conseils importants

## Faire de petits commits

Préférer :

* plusieurs petits commits propres
* plutôt qu’un énorme commit de 500 fichiers

---

## Pull régulièrement

Évite les gros conflits.

---

## Éviter de travailler sur main directement

Créer des branches de fonctionnalités.

---

## Éviter les force push inutiles

Très dangereux en équipe.

---

# Workflow moderne simplifié

```txt
main
 └── feature/login
 └── feature/payment
 └── hotfix/navbar
```

Chaque fonctionnalité possède sa propre branche.

---

# Conclusion

Git est un outil extrêmement puissant.

Le plus important n’est pas de connaître toutes les commandes, mais de :

* comprendre le workflow
* travailler proprement
* collaborer efficacement
* éviter de casser l’historique
* savoir résoudre les conflits
