---
layout: documentation
hide_hero: false
hero_image: "/docs/tutorial/kicad-eeschema-bases/hero.png"
hero_darken: true
image: "hero.png"
component_toc: true
doc_header: true
type: tutorial
order: 3

title: KiCAD Eeschema - Les Bases
subtitle: Apprenez à créer vos premiers schémas électroniques
description: Ce tutoriel couvre les fonctionnalités de base de l'éditeur de schémas Eeschema de KiCAD.
author: Alban Petit

time: 3
difficulty: 2
compatibilities-os: win, mac, lin

prerequisites:
  - label: KiCAD installé sur votre ordinateur
    link: "/electronic-design/docs/tutorial/installation-kicad"

softwares:
  - label: KiCAD (version 8.0 ou supérieure)
    link: "https://www.kicad.org/"

hardwares:
  - label: Ordinateur avec souris
    link: ""

todo: 100
---

## Introduction

Eeschema est l'éditeur de schémas électroniques intégré à KiCAD. Il vous permet de créer des schémas de circuits, d'ajouter des composants, de les connecter entre eux, et de vérifier la cohérence de votre conception avant de passer à la création du PCB.

Ce tutoriel vous guidera à travers les bases d'Eeschema : création d'un projet, placement de composants, connexions, annotation et vérification électrique.

{% include message.html
title="Pré-requis"
message="Assurez-vous d'avoir KiCAD installé et d'être familier avec son interface principale. Si ce n'est pas le cas, consultez notre tutoriel d'installation."
status="is-info"
icon="fas fa-info-circle" %}

---

## Créer un nouveau projet

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Lancer KiCAD"
content="Ouvrez KiCAD. Vous arrivez sur le gestionnaire de projets (Project Manager), l'interface principale de KiCAD."
image="kicad-main.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Créer un nouveau projet"
content="Cliquez sur <strong>Fichier > Nouveau Projet</strong> ou utilisez le raccourci <strong>Ctrl+N</strong> (Cmd+N sur macOS). Choisissez un emplacement pour votre projet et donnez-lui un nom significatif, par exemple 'mon-premier-schema'." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Ouvrir l'éditeur de schémas"
content="Une fois le projet créé, double-cliquez sur le fichier .kicad_sch dans le gestionnaire de projets, ou cliquez sur l'icône <strong>Éditeur de schémas</strong> dans la barre d'outils. Eeschema s'ouvre avec une feuille vierge."
image="ouvrir-eeschema.png" %}

{% include message.html
title="Organisation des fichiers"
message="KiCAD crée automatiquement plusieurs fichiers pour votre projet : .kicad_pro (projet), .kicad_sch (schéma), et plus tard .kicad_pcb (circuit imprimé). Conservez tous ces fichiers dans le même dossier."
status="is-info"
icon="fas fa-folder" %}

---

## Découvrir l'interface d'Eeschema

{% include step-tuto.html
greyBackground = true
title = "Les zones de l'interface"
content="L'interface d'Eeschema est divisée en plusieurs zones :<br>
<strong>1. Barre d'outils supérieure</strong> : Outils principaux (sauvegarder, annuler, zoom, etc.)<br>
<strong>2. Barre d'outils verticale droite</strong> : Outils de dessin et placement<br>
<strong>3. Zone de dessin centrale</strong> : Votre schéma<br>
<strong>4. Arborescence à gauche</strong> : Navigation entre les feuilles<br>
<strong>5. Barre de messages en bas</strong> : Informations et coordonnées"
image="interface-eeschema.png" %}

{% include step-tuto.html
greyBackground = true
title = "Raccourcis clavier essentiels"
content="Mémorisez ces raccourcis pour gagner en efficacité :<br>
<strong>A</strong> : Ajouter un composant (Add symbol)<br>
<strong>W</strong> : Tracer un fil (Wire)<br>
<strong>L</strong> : Ajouter un label<br>
<strong>M</strong> : Déplacer un élément<br>
<strong>R</strong> : Pivoter un élément<br>
<strong>E</strong> : Éditer les propriétés<br>
<strong>Delete</strong> : Supprimer un élément<br>
<strong>Échap</strong> : Annuler l'action en cours" %}

{% include message.html
title="Astuce - Zoom"
message="Utilisez la molette de la souris pour zoomer/dézoomer. Maintenez le bouton du milieu (molette) enfoncé pour déplacer la vue. Double-clic sur la molette pour ajuster le zoom à la page."
status="is-success"
icon="fas fa-mouse" %}

---

## Placer des composants

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Ouvrir le sélecteur de composants"
content="Appuyez sur la touche <strong>A</strong> ou cliquez sur l'icône 'Ajouter un symbole' dans la barre d'outils droite. Une fenêtre de sélection de composants s'ouvre."
image="ajouter-composant.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Rechercher un composant"
content="Dans le champ de recherche, tapez le nom du composant souhaité. Par exemple :<br>
- <code>R</code> pour une résistance<br>
- <code>C</code> pour un condensateur<br>
- <code>LED</code> pour une LED<br>
- <code>GND</code> pour la masse<br>
Utilisez les filtres pour affiner votre recherche si nécessaire."
image="recherche-composant.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Placer le composant"
content="Double-cliquez sur le composant choisi ou appuyez sur <strong>Entrée</strong>. Le composant s'attache à votre curseur. Déplacez-le à l'emplacement souhaité et cliquez pour le placer. Vous pouvez :<br>
- Appuyer sur <strong>R</strong> pour le pivoter avant de cliquer<br>
- Appuyer sur <strong>X</strong> ou <strong>Y</strong> pour le retourner horizontalement/verticalement<br>
- Appuyer sur <strong>Échap</strong> pour annuler"
image="placer-composant.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 4 : Placer plusieurs composants"
content="Créons un circuit simple LED avec résistance :<br>
1. Placez une <strong>LED</strong> (cherchez 'LED')<br>
2. Placez une <strong>résistance</strong> (cherchez 'R')<br>
3. Placez un symbole <strong>+5V</strong> (cherchez '+5V' dans Device)<br>
4. Placez deux symboles <strong>GND</strong> (masse)<br>
Disposez-les de manière logique sur votre schéma."
image="placer-composant.png" %}

{% include message.html
title="Bibliothèques de composants"
message="Les composants sont organisés en bibliothèques thématiques : Device (composants génériques), Connector (connecteurs), MCU (microcontrôleurs), etc. N'hésitez pas à explorer les différentes bibliothèques."
status="is-info"
icon="fas fa-book" %}

---

## Connecter les composants

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Activer l'outil fil"
content="Appuyez sur la touche <strong>W</strong> (Wire) ou cliquez sur l'icône 'Tracer un fil' dans la barre d'outils droite. Le curseur se transforme en croix."
image="outil-fil.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Tracer des connexions"
content="Cliquez sur l'extrémité d'une broche d'un composant pour commencer le fil. Le fil suit votre curseur. Cliquez à nouveau pour créer un point d'ancrage ou terminer sur une autre broche. Le fil devient vert quand il est correctement connecté à une broche.<br><br>
<strong>Astuces :</strong><br>
- Double-clic pour terminer le fil sans connexion<br>
- Les fils se connectent automatiquement aux broches quand vous êtes dessus<br>
- Appuyez sur <strong>Échap</strong> pour annuler"
image="tracer-fils.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Créer des jonctions"
content="Lorsque deux fils se croisent et doivent être connectés, placez une <strong>jonction</strong> (point de connexion). KiCAD le fait généralement automatiquement, mais vous pouvez en ajouter manuellement : cliquez sur l'icône jonction ou utilisez le menu clic droit > Ajouter une jonction."
image="jonctions.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 4 : Connecter votre circuit LED"
content="Connectez les composants de votre circuit :<br>
1. Connectez <strong>+5V</strong> à une broche de la résistance<br>
2. Connectez l'autre broche de la résistance à l'anode de la LED (broche +)<br>
3. Connectez la cathode de la LED (broche -) à <strong>GND</strong><br>
Votre premier circuit est maintenant câblé !" %}

{% include message.html
title="Attention - Symboles d'alimentation"
message="Les symboles d'alimentation (+5V, GND, +3.3V, etc.) sont des connexions implicites : tous les symboles portant le même nom sont connectés entre eux automatiquement, même sans fil visible."
status="is-warning"
icon="fas fa-bolt" %}

---

## Ajouter des labels et des valeurs

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Éditer les valeurs des composants"
content="Survolez un composant et appuyez sur <strong>E</strong> (Edit) ou double-cliquez dessus. Une fenêtre de propriétés s'ouvre. Modifiez :<br>
- <strong>Value</strong> : la valeur du composant (ex: 220R pour une résistance de 220Ω)<br>
- <strong>Reference</strong> : sera généré automatiquement lors de l'annotation<br>
- <strong>Footprint</strong> : l'empreinte physique (nous verrons ça plus tard)<br>
Validez avec OK."
image="editer-valeur.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Ajouter des valeurs à vos composants"
content="Éditez vos composants pour leur donner des valeurs réalistes :<br>
- Résistance : <code>220R</code> ou <code>220</code><br>
- LED : <code>Red</code> ou <code>LED_Red</code><br>
Ces informations apparaissent sur le schéma et seront utiles pour la suite."
image="valeurs-composants.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Ajouter des labels de nets"
content="Les labels permettent de nommer des connexions sans tracer de fils. Appuyez sur <strong>L</strong> (Label) ou cliquez sur l'icône correspondante. Tapez un nom (ex: 'LED_ANODE') et placez le label sur un fil. Tous les fils portant le même label sont connectés entre eux.<br><br>
C'est particulièrement utile pour les schémas complexes ou multi-feuilles."
image="labels.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 4 : Ajouter des notes et du texte"
content="Pour documenter votre schéma, vous pouvez ajouter du texte libre. Cliquez sur l'icône 'T' (Texte) dans la barre d'outils droite, ou allez dans <strong>Placer > Texte</strong>. Ajoutez des commentaires, des notes de version, ou toute information pertinente." %}

{% include message.html
title="Bonnes pratiques - Documentation"
message="Documentez toujours vos schémas : ajoutez un titre, votre nom, la date, et des notes expliquant le fonctionnement du circuit. Votre vous-même dans 6 mois vous remerciera !"
status="is-success"
icon="fas fa-file-alt" %}

---

## Annoter les composants

{% include step-tuto.html
greyBackground = true
title = "Qu'est-ce que l'annotation ?"
content="L'annotation attribue automatiquement des références uniques à tous vos composants. Par exemple :<br>
- Les résistances deviennent R1, R2, R3...<br>
- Les condensateurs deviennent C1, C2, C3...<br>
- Les circuits intégrés deviennent U1, U2, U3...<br>
C'est une étape essentielle avant de créer le PCB." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Ouvrir l'outil d'annotation"
content="Allez dans <strong>Outils > Annoter les symboles</strong> ou cliquez sur l'icône correspondante dans la barre d'outils. Une fenêtre d'annotation s'ouvre avec plusieurs options."
image="annoter.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Configurer et annoter"
content="Dans la fenêtre d'annotation :<br>
- <strong>Étendue</strong> : Sélectionnez 'Utiliser le schéma entier' pour annoter tout<br>
- <strong>Ordre</strong> : Choisissez de préférence 'Horizontal puis vertical' ou 'Vertical puis horizontal'<br>
- <strong>Options</strong> : Laissez les options par défaut pour commencer<br>
Cliquez sur <strong>Annoter</strong>, puis <strong>OK</strong> pour confirmer."
image="annoter.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Vérifier l'annotation"
content="Après annotation, vérifiez que tous vos composants ont bien reçu une référence unique (R1, LED1, etc.). Les références apparaissent au-dessus ou à côté des symboles. Si vous modifiez votre schéma, relancez l'annotation pour mettre à jour." %}

{% include message.html
title="Ré-annotation"
message="Si vous ajoutez de nouveaux composants après avoir annoté, relancez l'outil d'annotation. Vous pouvez choisir de ne numéroter que les nouveaux composants ou de tout ré-annoter depuis le début."
status="is-info"
icon="fas fa-redo" %}

---

## Vérification électrique (ERC)

{% include step-tuto.html
greyBackground = true
title = "Qu'est-ce que l'ERC ?"
content="L'ERC (Electrical Rule Check) est un outil qui vérifie automatiquement votre schéma pour détecter les erreurs courantes :<br>
- Broches non connectées<br>
- Conflits entre sorties<br>
- Labels non utilisés<br>
- Symboles d'alimentation manquants<br>
C'est une étape cruciale avant de passer au PCB." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Lancer l'ERC"
content="Allez dans <strong>Inspecter > Vérificateur de règles électriques</strong> ou cliquez sur l'icône coccinelle/vérification dans la barre d'outils. La fenêtre ERC s'ouvre."
image="lancer-erc.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Exécuter la vérification"
content="Cliquez sur le bouton <strong>Exécuter ERC</strong>. L'outil analyse votre schéma et affiche les erreurs et avertissements trouvés. Chaque problème est listé avec :<br>
- Le type (erreur ou avertissement)<br>
- Une description du problème<br>
- L'emplacement sur le schéma"
image="executer-erc.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Corriger les erreurs"
content="Double-cliquez sur une erreur dans la liste pour naviguer vers l'élément concerné sur le schéma. Corrigez les problèmes :<br>
- Connectez les broches non connectées<br>
- Ajoutez des drapeaux 'Non connecté' (No Connect) sur les broches intentionnellement non utilisées<br>
- Vérifiez les connexions d'alimentation<br>
Relancez l'ERC jusqu'à obtenir 0 erreur."
image="corriger-erreurs.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 4 : Drapeaux No Connect"
content="Pour les broches intentionnellement non connectées, placez un drapeau 'No Connect' pour indiquer à l'ERC que c'est voulu. Cliquez sur l'icône 'X' dans la barre d'outils droite ou appuyez sur <strong>Q</strong>, puis cliquez sur la broche."
image="no-connect.png" %}

{% include message.html
title="Avertissements vs Erreurs"
message="Les erreurs (rouge) doivent impérativement être corrigées. Les avertissements (jaune) sont à évaluer : certains sont légitimes, d'autres peuvent être ignorés selon votre conception. Un schéma propre devrait avoir 0 erreur et le minimum d'avertissements."
status="is-warning"
icon="fas fa-exclamation-triangle" %}

---

## Compléter les informations du schéma

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Cartouche d'informations"
content="Dans le coin inférieur droit de votre schéma se trouve le cartouche (title block). Cliquez dessus pour le modifier. Remplissez :<br>
- <strong>Title</strong> : Le titre de votre projet<br>
- <strong>Company</strong> : Votre nom ou organisation<br>
- <strong>Date</strong> : Date de création/modification<br>
- <strong>Revision</strong> : Version du schéma (v1.0, v1.1, etc.)<br>
- <strong>Comment</strong> : Notes additionnelles"
image="cartouche.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Sauvegarder votre travail"
content="Sauvegardez régulièrement votre schéma avec <strong>Ctrl+S</strong> (Cmd+S sur macOS) ou <strong>Fichier > Enregistrer</strong>. KiCAD crée automatiquement des fichiers de sauvegarde (backup) pour éviter les pertes de données." %}

{% include message.html
title="Conseil - Versioning"
message="Pour les projets importants, utilisez un système de contrôle de version (Git) pour suivre l'évolution de vos schémas et pouvoir revenir en arrière si nécessaire."
status="is-success"
icon="fas fa-code-branch" %}

---

## Exporter votre schéma

{% include step-tuto.html
greyBackground = true
title = "Exporter en PDF"
content="Pour partager ou archiver votre schéma, exportez-le en PDF :<br>
1. Allez dans <strong>Fichier > Tracer</strong><br>
2. Sélectionnez le format <strong>PDF</strong><br>
3. Choisissez les options (couleur ou noir & blanc, une page ou tout le schéma)<br>
4. Cliquez sur <strong>Tracer le schéma</strong><br>
Le PDF est créé dans le dossier de votre projet."
image="export-pdf.png" %}

---

## Prochaines étapes

Félicitations ! Vous maîtrisez maintenant les bases d'Eeschema. Vous savez créer un schéma, placer et connecter des composants, les annoter et vérifier votre conception.

### Que faire ensuite ?

Une fois votre schéma terminé et vérifié, les prochaines étapes sont :

1. **Associer les empreintes** : Attribuer à chaque composant son empreinte physique (footprint) pour le PCB
2. **Créer le PCB** : Passer à Pcbnew pour router votre circuit imprimé
3. **Générer les fichiers de fabrication** : Créer les fichiers Gerber pour faire fabriquer votre carte

{% include message.html
title="Continuez votre apprentissage"
message="Consultez nos tutoriels avancés pour apprendre à créer des schémas hiérarchiques multi-feuilles, créer vos propres symboles, et maîtriser les fonctionnalités avancées d'Eeschema."
status="is-success"
icon="fas fa-graduation-cap" %}

---

## Astuces et bonnes pratiques

### Organisation du schéma

- **Soyez logique** : Organisez votre schéma de gauche à droite (entrée vers sortie)
- **Espacez les composants** : Laissez de l'espace pour une meilleure lisibilité
- **Alignez les composants** : Utilisez la grille pour aligner les éléments
- **Regroupez par fonction** : Mettez ensemble les composants liés fonctionnellement

### Nommage

- **Labels explicites** : Utilisez des noms clairs (ex: 'LED_POWER' plutôt que 'NET1')
- **Valeurs complètes** : Indiquez l'unité (220R, 100nF, 10uH)
- **Notes importantes** : Ajoutez des commentaires pour les choix critiques

### Vérification

- **ERC régulier** : Lancez l'ERC après chaque modification importante
- **Vérification visuelle** : Relisez votre schéma comme si vous le découvriez
- **Validation par un pair** : Faites relire votre schéma par quelqu'un d'autre si possible

### Sauvegarde

- **Sauvegardez souvent** : Ctrl+S doit devenir un réflexe
- **Versioning** : Utilisez Git ou faites des copies manuelles avec dates
- **Backup externe** : Sauvegardez régulièrement sur un disque externe ou cloud

---

## Raccourcis clavier complets

Voici la liste complète des raccourcis les plus utiles dans Eeschema :

### Placement et édition
- **A** : Ajouter un symbole
- **P** : Ajouter une broche de connexion (Power)
- **W** : Tracer un fil
- **B** : Tracer un bus
- **L** : Placer un label
- **H** : Placer un label hiérarchique
- **G** : Placer un label global
- **Q** : Placer un drapeau No Connect
- **T** : Placer du texte

### Manipulation
- **M** : Déplacer un élément
- **G** : Glisser (drag) un élément en gardant les fils attachés
- **C** : Copier un élément
- **R** : Pivoter un élément
- **X** : Retourner horizontalement
- **Y** : Retourner verticalement
- **E** : Éditer les propriétés
- **Delete** : Supprimer un élément
- **Ctrl+D** : Dupliquer un élément

### Navigation et affichage
- **Molette** : Zoom avant/arrière
- **Ctrl+Molette** : Défilement vertical
- **Shift+Molette** : Défilement horizontal
- **Bouton milieu maintenu** : Déplacer la vue (pan)
- **F1** : Zoomer pour tout afficher
- **Home** : Recentrer le curseur

### Général
- **Ctrl+S** : Sauvegarder
- **Ctrl+Z** : Annuler
- **Ctrl+Y** : Rétablir
- **Échap** : Annuler l'action en cours
- **Ctrl+F** : Rechercher
- **F11** : Passer en plein écran

---

## Ressources complémentaires

Pour approfondir vos connaissances sur Eeschema et KiCAD :

- [Documentation officielle Eeschema](https://docs.kicad.org/master/fr/eeschema/eeschema.html)
- [Forum KiCAD (en anglais)](https://forum.kicad.info/)
- [Tutoriels vidéo KiCAD](https://www.youtube.com/results?search_query=kicad+eeschema+tutorial)
- [KiCad Library](https://kicad.github.io/)

{% include message.html
title="Prêt pour le PCB ?"
message="Une fois votre schéma terminé, annoté et vérifié, vous êtes prêt à passer à Pcbnew pour créer votre circuit imprimé. Consultez notre prochain tutoriel sur Pcbnew pour la suite !"
status="is-success"
icon="fas fa-arrow-right" %}

---

## Pour aller plus loin

{%
  include card_collections.html
  title="Tutoriels KiCAD"
  description="Explorez d'autres tutoriels pour maîtriser KiCAD"
  type="tutorial"
%}
