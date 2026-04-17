
```markdown
# Procédure de Réinitialisation de l'Environnement Vagrant

Ce guide détaille les étapes nécessaires pour nettoyer une instance Vagrant existante et reconstruire proprement votre machine virtuelle Debian 12 à l'aide de PowerShell.

---

## Prérequis

* **PowerShell** : Installé par défaut sur Windows.
* **Vagrant** : Version 2.2.0 ou supérieure recommandée.
* **VirtualBox** : Le fournisseur (hyperviseur) utilisé pour gérer la machine virtuelle.

---

## Étapes à suivre

Suivez ces étapes dans l'ordre pour éviter les conflits de configuration.

### 1. Ouvrir PowerShell et accéder au projet
Ouvrez une fenêtre PowerShell et déplacez-vous dans le dossier qui contient votre fichier `Vagrantfile` :

```powershell
cd "chemin\vers\votre\projet"
```

### 2. Nettoyage forcé des fichiers résiduels
Le dossier caché `.vagrant` stocke l'identifiant technique de la machine virtuelle actuelle. Si vous rencontrez des erreurs de connexion ou si vous souhaitez repartir sur une base neuve, il est crucial de le supprimer.

Exécutez la commande suivante pour forcer la suppression du dossier :

```powershell
Remove-Item -Recurse -Force .vagrant
```

### 3. Déploiement de la machine virtuelle
Lancez la création et la configuration de l'environnement avec la commande :

```powershell
vagrant up
```

**Ce que fait cette commande concrètement :**
* **Téléchargement** : Récupère l'image système (box) depuis votre lien GitHub si elle n'est pas déjà présente localement.
* **Importation** : Crée une nouvelle instance dans VirtualBox nommée `debian12`.
* **Configuration** : Définit les ressources (1024 Mo de RAM, 1 CPU) et l'adresse IP statique `192.168.44.44`.
* **Provisioning** : Exécute le script interne pour installer **Ansible**, créer l'utilisateur **debian** (mot de passe : `1234`) et configurer les privilèges **sudo**.

### 4. Vérification et Connexion
Une fois que le terminal vous redonne la main, vérifiez que la machine est bien active :

```powershell
vagrant status
```

Pour vous connecter en SSH et commencer à utiliser la machine :

```powershell
vagrant ssh
```

---

## Résumé des commandes (Quick Start)
Pour une réinitialisation rapide en une seule ligne, vous pouvez copier-coller ceci dans PowerShell :

```powershell
Remove-Item -Recurse -Force .vagrant; vagrant up
```

---

## Dépannage (Troubleshooting)

* **Erreur réseau** : Si l'IP `192.168.44.44` est déjà utilisée sur votre réseau local, modifiez-la directement dans le `Vagrantfile` avant de relancer le `vagrant up`.
* **Problème VirtualBox** : Si la machine refuse de démarrer, assurez-vous que la **Virtualisation (VT-x/AMD-V)** est activée dans le BIOS de votre ordinateur.
* **Accès Sudo** : L'utilisateur `debian` est ajouté au groupe sudo pour permettre l'utilisation d'Ansible sans restriction.
```