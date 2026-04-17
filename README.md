# Procédure de Réinitialisation de l'Environnement Vagrant

Ce guide explique comment nettoyer une instance Vagrant existante et la redémarrer proprement via PowerShell.

## Prérequis

* PowerShell (intégré à Windows)
* Vagrant installé
* VirtualBox (ou un autre fournisseur de virtualisation compatible)

## Étapes à suivre

Suivez ces étapes dans l'ordre pour éviter les conflits de configuration.

### 1. Ouvrir PowerShell
Lancez une instance de PowerShell. Vous pouvez le faire en recherchant "PowerShell" dans le menu Démarrer de Windows.

### 2. Supprimer les fichiers résiduels
Avant de relancer la machine, il est nécessaire de supprimer le dossier technique `.vagrant`. Ce dossier contient l'état actuel de la machine virtuelle locale.

Exécutez la commande suivante dans le répertoire de votre projet :
```powershell
Remove-Item -Recurse -Force .vagrant