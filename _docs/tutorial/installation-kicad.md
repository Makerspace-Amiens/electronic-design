---
layout: documentation
hide_hero: false
hero_image: "/docs/tutorial/installation-kicad/hero.png"
hero_darken: true
image: "hero.png"
component_toc: true
doc_header: true
type: tutorial
order: 2

title: Installation de KiCAD
subtitle: Installez KiCAD sur votre système d'exploitation
description: Ce tutoriel explique comment installer KiCAD sur Windows, macOS et Linux.
author: Alban Petit

time: 1
difficulty: 1
compatibilities-os: win, mac, lin

prerequisites:
  - label: Droits administrateur sur votre ordinateur
    link: ""

softwares:
  - label: KiCAD (version 8.0 ou supérieure recommandée)
    link: "https://www.kicad.org/"

hardwares:
  - label: Ordinateur avec au moins 4GB de RAM
    link: ""

todo: 100
---

## Introduction

KiCAD est un logiciel libre et open-source de conception de circuits électroniques et de circuits imprimés (PCB). Il permet de créer des schémas électroniques, de dessiner des PCB et de générer les fichiers nécessaires à la fabrication de vos cartes électroniques.

Ce tutoriel vous guidera à travers l'installation de KiCAD sur les trois systèmes d'exploitation principaux : Windows, macOS et Linux.

{% include message.html
title="Version recommandée"
message="Nous recommandons d'installer la dernière version stable de KiCAD (version 8.0 ou supérieure) pour bénéficier des dernières fonctionnalités et corrections de bugs."
status="is-info"
icon="fas fa-info-circle" %}

---

## Installation sur Windows

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Téléchargement"
content="Rendez-vous sur le site officiel de KiCAD à l'adresse [https://www.kicad.org/download/windows/](https://www.kicad.org/download/windows/). Téléchargez la dernière version stable pour Windows (fichier .exe)." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Exécution de l'installateur"
content="Double-cliquez sur le fichier téléchargé pour lancer l'installation. Si Windows vous demande l'autorisation d'exécuter le fichier, cliquez sur 'Oui'." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Configuration de l'installation"
content="Suivez les instructions de l'assistant d'installation. Il est recommandé de conserver les paramètres par défaut :<br>
- Installation complète (incluant les bibliothèques de composants)<br>
- Chemin d'installation par défaut : C:\\Program Files\\KiCAD<br>
- Création des raccourcis sur le bureau" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 4 : Finalisation"
content="Cliquez sur 'Installer' et patientez pendant l'installation. Une fois terminée, cliquez sur 'Terminer'. Vous pouvez maintenant lancer KiCAD depuis le menu Démarrer ou le raccourci sur le bureau." %}

{% include message.html
title="Conseil"
message="Lors du premier lancement, KiCAD peut mettre quelques instants à initialiser les bibliothèques de composants. C'est normal."
status="is-success"
icon="fas fa-check-circle" %}

---

## Installation sur macOS

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Téléchargement"
content="Rendez-vous sur le site officiel de KiCAD à l'adresse [https://www.kicad.org/download/macos/](https://www.kicad.org/download/macos/). Téléchargez la version correspondant à votre processeur :<br>
- KiCAD pour Apple Silicon (M1, M2, M3, M4) - fichier .dmg<br>
- KiCAD pour Intel - fichier .dmg" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Ouverture du fichier DMG"
content="Double-cliquez sur le fichier .dmg téléchargé pour le monter. Une fenêtre s'ouvrira avec l'icône de KiCAD et le dossier Applications." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Installation"
content="Glissez-déposez l'icône KiCAD dans le dossier Applications. Attendez que la copie se termine." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 4 : Premier lancement"
content="Ouvrez le dossier Applications et double-cliquez sur KiCAD. Si macOS vous affiche un message de sécurité, allez dans Préférences Système > Confidentialité et sécurité, puis autorisez l'exécution de KiCAD." %}

{% include message.html
title="Important - Sécurité macOS"
message="Lors du premier lancement, macOS peut bloquer KiCAD car il n'est pas téléchargé depuis l'App Store. C'est normal, suivez simplement les instructions ci-dessus pour autoriser l'application."
status="is-warning"
icon="fas fa-exclamation-triangle" %}

---

## Installation sur Linux

KiCAD peut être installé sur la plupart des distributions Linux. Voici les méthodes pour les distributions les plus populaires.

### Ubuntu / Debian

{% include step-tuto.html
greyBackground = true
title = "Méthode 1 : Installation via PPA (recommandée)"
content="Ouvrez un terminal et exécutez les commandes suivantes pour ajouter le PPA officiel de KiCAD et installer la dernière version :<br><br>
<code>sudo add-apt-repository ppa:kicad/kicad-8.0-releases</code><br>
<code>sudo apt update</code><br>
<code>sudo apt install kicad</code>" %}

{% include step-tuto.html
greyBackground = true
title = "Méthode 2 : Installation via Snap"
content="Si vous préférez utiliser Snap, exécutez simplement :<br><br>
<code>sudo snap install kicad</code>" %}

### Fedora

{% include step-tuto.html
greyBackground = true
title = "Installation sur Fedora"
content="Ouvrez un terminal et exécutez :<br><br>
<code>sudo dnf install kicad</code>" %}

### Arch Linux

{% include step-tuto.html
greyBackground = true
title = "Installation sur Arch Linux"
content="Ouvrez un terminal et exécutez :<br><br>
<code>sudo pacman -S kicad</code>" %}

### Flatpak (toutes distributions)

{% include step-tuto.html
greyBackground = true
title = "Installation via Flatpak"
content="Si votre distribution supporte Flatpak, vous pouvez installer KiCAD avec :<br><br>
<code>flatpak install flathub org.kicad.KiCad</code><br><br>
Et le lancer avec :<br>
<code>flatpak run org.kicad.KiCad</code>" %}

{% include message.html
title="Bibliothèques de composants"
message="Sur Linux, les bibliothèques de composants sont généralement installées automatiquement avec le package principal. Si ce n'est pas le cas, installez également le package kicad-libraries ou kicad-symbols."
status="is-info"
icon="fas fa-info-circle" %}

---

## Vérification de l'installation

{% include step-tuto.html
greyBackground = true
title = "Vérifier que KiCAD fonctionne"
content="Une fois l'installation terminée, lancez KiCAD. Vous devriez voir la fenêtre principale du gestionnaire de projets avec plusieurs icônes :<br>
- Eeschema (éditeur de schémas)<br>
- Pcbnew (éditeur de PCB)<br>
- GerbView (visualiseur Gerber)<br>
- Et d'autres outils<br><br>
Si vous voyez cette interface, félicitations ! KiCAD est correctement installé." %}

---

## Configuration initiale (optionnelle)

{% include step-tuto.html
greyBackground = true
title = "Configurer les préférences"
content="Avant de commencer votre premier projet, vous pouvez personnaliser KiCAD :<br>
1. Allez dans Préférences > Préférences<br>
2. Configurez vos unités préférées (mm ou inches)<br>
3. Ajustez la grille de travail selon vos besoins<br>
4. Configurez les chemins vers les bibliothèques si nécessaire" %}

{% include step-tuto.html
greyBackground = true
title = "Installer des bibliothèques additionnelles"
content="KiCAD est livré avec de nombreux composants, mais vous pouvez en ajouter d'autres :<br>
- Depuis le gestionnaire de bibliothèques (Préférences > Gérer les bibliothèques de symboles/empreintes)<br>
- En téléchargeant des bibliothèques tierces depuis GitHub<br>
- En créant vos propres bibliothèques personnalisées" %}

---

## Ressources utiles

Une fois KiCAD installé, voici quelques ressources pour bien démarrer :

- [Documentation officielle de KiCAD](https://docs.kicad.org/)
- [Forums KiCAD](https://forum.kicad.info/)
- [Tutoriels vidéo sur YouTube](https://www.youtube.com/results?search_query=kicad+tutorial)
- [Bibliothèques de composants communautaires](https://kicad.github.io/)

{% include message.html
title="Prochaines étapes"
message="Maintenant que KiCAD est installé, vous êtes prêt à créer votre premier projet ! Consultez nos autres tutoriels pour apprendre à concevoir votre première carte électronique."
status="is-success"
icon="fas fa-rocket" %}

---

## Pour aller plus loin

{%
  include card_collections.html
  title="Tutoriels KiCAD"
  description="Explorez d'autres tutoriels pour maîtriser KiCAD"
  type="tutorial"
%}
