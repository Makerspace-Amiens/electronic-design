---
layout: documentation
hide_hero: false
hero_image: "/docs/project/stepper-controller-board/hero.jpg"
hero_darken: true
image: "board.png"
component_toc: true
doc_header: true
type: project
order: 100

title: Carte contrôleur Machine That Draws
subtitle: Conception d'un contrôleur ESP32 avec stockage SD et affichage OLED
description: Projet de conception d'une carte électronique complète pour piloter des moteurs pas-à-pas, intégrant ESP32, lecteur SD, écran OLED et drivers A4988.
author: Alban Petit

# Métadonnées spécifiques au projet
difficulty: 3
team_size: "2-3 étudiants"
evaluation: true

prerequisites:
  - label: Bases en électronique et circuits numériques
    link: ""
  - label: Programmation C++ (framework Arduino)
    link: ""
  - label: KiCad (schématique et PCB)
    link: "/docs/tutorial/kicad-eeschema-bases"
  - label: Soudure de composants CMS et traversants
    link: ""

softwares:
  - label: KiCad 8.0+
    link: "https://www.kicad.org/"
  - label: VSCode + PlatformIO
    link: "/docs/tutorial/installation-vscode-platformio"

hardwares:
  - label: ESP32
    link: ""
  - label: Drivers A4988 (×2 minimum)
    link: ""
  - label: Écran OLED SSD1306 (0.96", I2C)
    link: ""
  - label: Socket SD (push-push)
    link: ""
  - label: Composants passifs (résistances, condensateurs)
    link: ""

todo: 100
---

## Présentation du projet

### Contexte

Ce projet s'inscrit dans la continuité du projet **Machine that draws** que vous avez réalisé précédemment. L'objectif est de concevoir et fabriquer une **carte électronique dédiée** pour remplacer le contrôleur de drivers.

La carte intégrera :

- **ESP32** comme microcontrôleur principal
- **2 drivers A4988** pour piloter les moteurs pas-à-pas X et Y
- **Lecteur de carte SD** pour stocker les fichiers G-code ou dessins
- **Écran OLED** pour afficher l'état, les menus et la progression
- **Connecteurs** pour moteurs, alimentation et extension

### Objectifs pédagogiques

À l'issue de ce projet, vous serez capables de :

- Concevoir un **schéma électronique complet** avec KiCad
- Réaliser le **routage d'un PCB multicouche**
- Intégrer des **bus de communication** (I2C, SPI) sur un même PCB
- Gérer les **contraintes de puissance** (découplage, largeur de pistes)
- Souder des **composants CMS et traversants**
- Déboguer une carte électronique et valider son fonctionnement
- Documenter un projet technique de A à Z

{% include message.html
title="Projet en binôme/trinôme"
message="Ce projet se réalise en équipe de 2 à 3 étudiants. Organisez-vous pour répartir les tâches : conception schématique, routage PCB, firmware, tests et documentation. La collaboration est essentielle à la réussite du projet."
status="is-info"
icon="fas fa-users" %}

---

## Cahier des charges

### Spécifications fonctionnelles

La carte doit permettre de :

1. **Piloter 2 moteurs pas-à-pas** (axes X et Y) via drivers A4988

2. **Stocker des fichiers** sur carte SD
   - Log des actions effectuées lors du fonctionnement de la solution
   - Format FAT32
   - Détection d'insertion de carte (optionnel)
   - Lancement de fichier G-code (optionnel)

3. **Afficher des informations** sur écran OLED
   - État de la machine (idle, running, error)
   - Progression (pourcentage, ligne en cours)
   - Menus de navigation (optionnel)

### Spécifications techniques

| Paramètre | Valeur | Remarques |
| ----------- | -------- | ----------- |
| **Alimentation** | 12V ou 24V DC | Alimentation externe pour moteurs |
| **Logique** | 3.3V | Fournie par le régulateur R-78E5.0-1.0 |
| **Courant moteurs** | 0.5A à 1.5A par phase | Réglable via Vref |
| **Interface I2C** | SDA=GPIO21, SCL=GPIO22 | Écran OLED |
| **Interface SPI** | VSPI (GPIO 18/19/23/5) | Carte SD |
| **Dimensions PCB** | ≤ 100×100 mm | Pour minimiser les coûts de fabrication |
| **Connecteurs** | Screw terminals | Alimentation |

---

## Bill of Materials (BOM)

### Composants principaux

| Désignation | Référence | Quantité |
| ------------- | ----------- | ---------- |
| ESP32 | ESP32 format arduino uno | 1 |
| Driver A4988 (module) | StepStick compatible | 2 |
| Écran OLED 0.96" I2C | SSD1306 128×64 | 1 |
| Socket SD push-push | - | 1 |
| Moteur NEMA 17 | - | 2 |
| Régulateur | R-78E5.0-1.0 | 1 |

### Composants passifs

| Désignation | Valeur | Package | Quantité | Remarques |
| ------------- | -------- | --------- | ---------- | ----------- |
| Condensateur céramique | 100nF | 1206 SMD | 10 | Découplage |
| Condensateur électrolytique | 100µF 35V | Radial  | 2 | Alimentation moteurs |
| Condensateur céramique | 10µF | 1206 SMD | - | Découplage VDD |
| Résistance pull-up | 10kΩ | 1206 SMD | - | I2C (SDA, SCL), SD (CS, MISO) |

### Connecteurs

| Désignation | Type | Quantité | Remarques |
|-------------|------|----------|-----------|
| Connecteur alimentation | Bornier à vis 2 pôles (5mm) | 1 | VMOT (12-24V) + GND |
| Pin headers mâle | Header (2.54mm) | 2 | 1A, 1B, 2A, 2B |
| Pin headers mâle | Header (2.54mm) | - | Connexion ESP32 |

---

## Étapes de réalisation

### Prototypage et validation

{% include step-tuto.html
greyBackground = true
title = "Étape 1.1 : Test du driver A4988 sur breadboard"
content="Objectif : Valider le fonctionnement d'un driver A4988 avec un moteur NEMA 17.

[Tutoriel A4988](/electronic-design/docs/tutorial/a4988-stepper-driver/)

**Tâches :**

- Monter le circuit A4988 + ESP32 + moteur sur breadboard
- Régler le Vref pour un courant de 1A (voir [tutoriel A4988](/electronic-design/docs/tutorial/a4988-stepper-driver/))
- Tester le code de rotation simple (full step)
- Mesurer la consommation et la température du driver

**Livrables :** Photo du montage + vidéo du moteur en fonctionnement" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 1.3 : Test de l'écran OLED"
content="Objectif : Afficher du texte et des graphiques sur l'OLED.

**Tâches :**

- Connecter l'écran OLED en I2C (voir [tutoriel SSD1306](/electronic-design/docs/tutorial/esp32-ssd1306-oled))
- Afficher : nom du fichier, état, progression
- Créer un menu simple avec 2-3 options (Start, Stop)" %}

### Conception du schéma électronique (KiCad)

{% include step-tuto.html
greyBackground = true
title = "Étape 2.1 : Schéma bloc et architecture"
content="Objectif : Définir l'architecture globale avant de dessiner le schéma.

**Tâches :**

- Dessiner un schéma bloc sur papier : ESP32 au centre, blocs I2C/SPI/GPIO autour
- Lister tous les signaux (STEP, DIR, EN, SDA, SCL, MISO, MOSI, SCK, CS)
- Définir les alimentations (3.3V, 12V/24V, GND communs)
- Identifier les découplages critiques (VDD, VMOT)" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2.2 : Schéma électronique dans KiCad"
content="Objectif : Dessiner le schéma complet dans KiCad Eeschema.

**Tâches :**

- Créer un nouveau projet KiCad
- Placer les symboles : ESP32, A4988 (×2), SSD1306, socket SD
- Connecter les alimentations (rails 3.3V et VMOT)
- Ajouter les condensateurs de découplage (100nF + 10µF)
- Ajouter les résistances de pull-up (I2C, SPI)
- Annoter tous les composants (désignateurs R1, C1, etc.)" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2.3 : Vérification ERC et revue de conception"
content="Objectif : Détecter les erreurs avant le routage.

**Tâches :**

- Lancer l'ERC (Electrical Rules Check) dans KiCad
- Corriger toutes les erreurs (connexions manquantes, conflits)
- Faire relire le schéma par un autre binôme
- Valider avec l'enseignant" %}

### Routage du PCB et fabrication

{% include step-tuto.html
greyBackground = true
title = "Étape 3.1 : Assignation des empreintes"
content="Objectif : Associer chaque composant à son empreinte physique.

**Tâches :**

- Ouvrir l'éditeur d'empreintes dans KiCad
- Assigner les footprints : ESP32, résistances/condensateurs 1206, borniers à vis
- Vérifier les dimensions des empreintes (comparer avec les datasheets)" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3.2 : Routage PCB dans KiCad Pcbnew"
content="Objectif : Router le PCB en respectant les contraintes.

**Tâches :**

- Placer les composants : ESP32 au centre, drivers A4988 proches des connecteurs moteurs, SD et OLED en périphérie
- Router les pistes de puissance (VMOT, GND) en premier (largeur ≥ 1.5mm)
- Router les signaux critiques (SPI, I2C) avec pistes courtes
- Placer les découplages au plus près des ICs
- Ajouter un plan de masse (GND) sur la couche inférieure
- Lancer le DRC (Design Rules Check) et corriger les erreurs " %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3.3 : Génération des fichiers Gerber et commande"
content="Objectif : Générer les fichiers de fabrication et commander les PCB.

**Tâches :**

- Générer les fichiers Gerber + fichier de perçage (voir [tutoriel fabrication PCB](/electronic-design/docs/tutorial/kicad-fabrication-pcb))
- Vérifier les fichiers avec un visualiseur Gerber (GerbView ou en ligne)" %}

### Assemblage, tests et validation

{% include step-tuto.html
greyBackground = true
title = "Étape 4.1 : Soudure des composants"
content="Objectif : Assembler la carte PCB.

**Tâches :**

- Souder les composants CMS en premier (résistances, condensateurs 1206, condensateurs électrolytiques)
- Souder les composants traversants (, borniers, pin headers)
- Souder les connecteurs de modules (ESP32, A4988, OLED, socket SD)
- Inspecter visuellement toutes les soudures (pas de court-circuit, pas de soudure froide)" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 4.2 : Tests de continuité et premier power-up"
content="Objectif : Vérifier l'absence de court-circuit avant la mise sous tension.

**Tâches :**

- Vérifier au multimètre : continuité GND, isolation 3.3V↔GND, isolation VMOT↔GND
- Vérifier la polarité des condensateurs électrolytiques
- Alimenter en 3.3V uniquement (via ESP32 USB) : pas de surchauffe
- Mesurer 3.3V sur les rails VDD
- Alimenter VMOT (12V) avec une alimentation à courant limité (< 500mA)" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 4.3 : Tests fonctionnels et intégration"
content="Objectif : Valider le fonctionnement complet de la carte.

**Tâches :**

- Uploader le firmware de test (blink, scan I2C, test SD)
- Vérifier l'affichage OLED (adresse I2C détectée : 0x3C)
- Vérifier la détection de la carte SD
- Tester la rotation d'un moteur avec le driver A4988
- Tester les 2 moteurs simultanément" %}

---

## Ressources techniques

Ce projet s'appuie sur les tutoriels suivants (à consulter impérativement) :

- [Installation VSCode + PlatformIO](/electronic-design/docs/tutorial/installation-vscode-platformio)
- [Driver A4988 avec ESP32](/electronic-design/docs/tutorial/a4988-stepper-driver)
- [Carte SD avec ESP32](/electronic-design/docs/tutorial/esp32-carte-sd)
- [Écran OLED SSD1306 avec ESP32](/electronic-design/docs/tutorial/esp32-ssd1306-oled)
- [KiCad : Schématique](/electronic-design/docs/tutorial/kicad-eeschema-bases)
- [KiCad : Routage PCB](/electronic-design/docs/tutorial/kicad-pcbnew-bases)
- [KiCad : Fabrication PCB](/electronic-design/docs/tutorial/kicad-fabrication-pcb)
