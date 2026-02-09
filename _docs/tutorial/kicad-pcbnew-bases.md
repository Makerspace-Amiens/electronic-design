---
layout: documentation
hide_hero: false
hero_image: "/docs/tutorial/kicad-pcbnew-bases/hero.png"
hero_darken: true
image: "hero.png"
component_toc: true
doc_header: true
type: tutorial
order: 4

title: KiCAD Pcbnew - Les Bases
subtitle: Concevez votre premier circuit imprimé
description: Ce tutoriel couvre les fonctionnalités de base de l'éditeur de PCB Pcbnew de KiCAD.
author: Alban Petit

time: 4
difficulty: 2
compatibilities-os: win, mac, lin

prerequisites:
  - label: KiCAD installé sur votre ordinateur
    link: "/electronic-design/docs/tutorial/installation-kicad"
  - label: Schéma électrique créé avec Eeschema
    link: "/electronic-design/docs/tutorial/kicad-eeschema-bases"

softwares:
  - label: KiCAD (version 8.0 ou supérieure)
    link: "https://www.kicad.org/"

hardwares:
  - label: Ordinateur avec souris
    link: ""

todo: 100
---

## Introduction

Pcbnew est l'éditeur de circuits imprimés (PCB) intégré à KiCAD. Après avoir créé votre schéma électronique dans Eeschema, Pcbnew vous permet de concevoir le circuit imprimé physique : placer les composants, router les connexions, définir les contours de la carte et générer les fichiers de fabrication.

Ce tutoriel vous guidera à travers les bases de Pcbnew : du passage du schéma au PCB jusqu'à la génération des fichiers Gerber pour la fabrication.

{% include message.html
title="Pré-requis important"
message="Ce tutoriel suppose que vous avez déjà créé un schéma électronique avec Eeschema, avec les composants annotés et les empreintes assignées. Si ce n'est pas le cas, consultez d'abord notre tutoriel sur Eeschema."
status="is-warning"
icon="fas fa-exclamation-triangle" %}

---

## Ouvrir Pcbnew et importer le schéma

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Ouvrir Pcbnew depuis le projet"
content="Depuis le gestionnaire de projets KiCAD, double-cliquez sur le fichier .kicad_pcb ou cliquez sur l'icône <strong>Éditeur de circuit imprimé</strong>. Pcbnew s'ouvre avec un PCB vierge ou votre PCB existant."
image="ouvrir-pcbnew.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Mettre à jour le PCB depuis le schéma"
content="Pour importer ou mettre à jour les composants depuis votre schéma, allez dans <strong>Outils > Mettre à jour le circuit imprimé depuis le schéma</strong> ou appuyez sur <strong>F8</strong>. Une fenêtre s'ouvre listant tous les changements." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Importer les composants"
content="Dans la fenêtre de mise à jour :<br>
- Vérifiez la liste des composants à ajouter<br>
- Cochez 'Supprimer les empreintes supplémentaires' si nécessaire<br>
- Cliquez sur <strong>Mettre à jour le PCB</strong><br>
Tous vos composants apparaissent empilés, prêts à être placés. Les connexions (chevelu/ratsnest) sont visibles."
image="composants-importation.png" %}

{% include message.html
title="Le chevelu (Ratsnest)"
message="Les lignes blanches fines qui relient les composants s'appellent le 'chevelu' ou 'ratsnest'. Elles représentent les connexions logiques de votre schéma et vous guident pour router vos pistes."
status="is-info"
icon="fas fa-project-diagram" %}

---

## Découvrir l'interface de Pcbnew

{% include step-tuto.html
greyBackground = true
title = "Les zones de l'interface"
content="L'interface de Pcbnew est organisée en plusieurs zones :<br>
<strong>1. Barre d'outils supérieure</strong> : Outils principaux (sauvegarder, annuler, zoom, couches)<br>
<strong>2. Barre d'outils verticale droite</strong> : Outils de dessin et routage<br>
<strong>3. Zone de dessin centrale</strong> : Votre PCB<br>
<strong>4. Panneau Apparence à droite</strong> : Visibilité des couches et éléments<br>
<strong>5. Barre de messages en bas</strong> : Coordonnées et informations"
image="interface-pcbnew.png" %}

{% include step-tuto.html
greyBackground = true
title = "Les couches du PCB"
content="Un PCB est constitué de plusieurs couches empilées :<br>
<strong>F.Cu (Front Copper)</strong> : Couche cuivre face avant (rouge)<br>
<strong>B.Cu (Back Copper)</strong> : Couche cuivre face arrière (vert)<br>
<strong>F.SilkS (Front Silkscreen)</strong> : Sérigraphie face avant (marquages)<br>
<strong>B.SilkS (Back Silkscreen)</strong> : Sérigraphie face arrière<br>
<strong>Edge.Cuts</strong> : Contour de découpe de la carte<br>
Pour les PCB 4 couches ou plus, il y a des couches internes (In1.Cu, In2.Cu, etc.)" %}

{% include step-tuto.html
greyBackground = true
title = "Raccourcis clavier essentiels"
content="Mémorisez ces raccourcis pour gagner en efficacité :<br>
<strong>M</strong> : Déplacer un composant<br>
<strong>R</strong> : Pivoter un composant<br>
<strong>F</strong> : Retourner un composant (face avant/arrière)<br>
<strong>X</strong> : Commencer une piste (route)<br>
<strong>V</strong> : Placer un via<br>
<strong>D</strong> : Glisser une piste (drag)<br>
<strong>U</strong> : Sélectionner la piste complète<br>
<strong>Delete</strong> : Supprimer un élément<br>
<strong>Page Up/Down</strong> : Changer de couche active<br>
<strong>Échap</strong> : Annuler l'action en cours" %}

{% include message.html
title="Astuce - Navigation"
message="Utilisez la molette pour zoomer, maintenez le bouton du milieu pour déplacer la vue. Appuyez sur F11 pour passer en mode plein écran et gagner de l'espace de travail."
status="is-success"
icon="fas fa-mouse" %}

---

## Assigner les empreintes

{% include step-tuto.html
greyBackground = true
title = "Qu'est-ce qu'une empreinte ?"
content="Une empreinte (footprint) est la représentation physique d'un composant sur le PCB : les pastilles de soudure, l'encombrement, la sérigraphie. Chaque symbole de votre schéma doit avoir une empreinte assignée pour être placé sur le PCB."
image="empreinte-exemple.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Ouvrir l'éditeur d'empreintes"
content="Depuis Eeschema, allez dans <strong>Outils > Assigner les empreintes</strong>. Une fenêtre s'ouvre avec trois colonnes :<br>
- Gauche : Bibliothèques d'empreintes<br>
- Centre : Empreintes disponibles<br>
- Droite : Votre liste de composants"
image="assigner-empreintes.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Assigner les empreintes aux composants"
content="Pour chaque composant de votre schéma :<br>
1. Sélectionnez-le dans la colonne de droite<br>
2. Cherchez l'empreinte correspondante (ex: pour une résistance CMS 0805, cherchez 'R_0805')<br>
3. Double-cliquez sur l'empreinte ou utilisez le bouton pour l'assigner<br>
4. L'empreinte apparaît à côté du composant<br><br>
<strong>Empreintes courantes :</strong><br>
- Résistances/condensateurs CMS : R_0805, C_0603<br>
- Résistances traversantes : R_Axial_DIN0207<br>
- LED CMS : LED_0805<br>
- LED traversante : LED_D3.0mm ou LED_D5.0mm" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Utiliser les filtres"
content="Utilisez les filtres en haut de la fenêtre pour trouver rapidement les empreintes :<br>
- <strong>Par mots-clés</strong> : Tapez '0805', 'SOIC', 'QFN', etc.<br>
- <strong>Par brochage</strong> : Filtrer par nombre de broches<br>
- <strong>Par bibliothèque</strong> : Sélectionnez une bibliothèque spécifique à gauche<br>
Visualisez l'empreinte avant de l'assigner avec le panneau d'aperçu."
image="filtres-empreintes.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 4 : Valider et sauvegarder"
content="Une fois toutes les empreintes assignées :<br>
1. Vérifiez qu'aucun composant n'a '<strong>&lt;non assigné&gt;</strong>'<br>
2. Cliquez sur <strong>OK</strong> ou <strong>Appliquer, Sauvegarder le schéma et continuer</strong><br>
3. Les empreintes sont maintenant liées à vos composants<br>
Retournez dans Pcbnew et mettez à jour le PCB (F8) pour voir les nouvelles empreintes." %}

{% include message.html
title="Bibliothèques d'empreintes"
message="KiCAD inclut des milliers d'empreintes standards. Pour des composants spécifiques, consultez les sites des fabricants ou utilisez SnapEDA/Ultra Librarian pour télécharger des empreintes toutes faites."
status="is-info"
icon="fas fa-download" %}

---

## Placer les composants

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Séparer les composants"
content="Après l'import, tous les composants sont empilés au même endroit. Cliquez et glissez pour les séparer grossièrement. Ne vous souciez pas encore de leur position finale, dispersez-les simplement pour y voir clair."
image="separer-composants.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Planifier l'organisation"
content="Avant de placer finement, réfléchissez à l'organisation logique :<br>
- Regroupez les composants par fonction (alimentation, microcontrôleur, connecteurs, etc.)<br>
- Identifiez les composants qui doivent être proches (ex: condensateurs de découplage près du µC)<br>
- Pensez au sens du flux de signal (entrée → traitement → sortie)<br>
- Considérez les contraintes mécaniques (trous de fixation, connecteurs en bordure)" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Placer les composants un par un"
content="Placez chaque composant en suivant ces principes :<br>
1. Sélectionnez un composant et appuyez sur <strong>M</strong> pour le déplacer<br>
2. Appuyez sur <strong>R</strong> pour le pivoter (rotation de 90°)<br>
3. Appuyez sur <strong>F</strong> pour le retourner (passer de la face avant à la face arrière)<br>
4. Observez le chevelu : les lignes doivent être courtes et peu croisées<br>
5. Alignez les composants sur la grille (clic droit > Grille pour changer le pas)<br>
Placez d'abord les composants critiques (connecteurs, µC), puis les passifs autour." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 4 : Optimiser le placement"
content="Un bon placement facilite le routage. Vérifiez :<br>
- <strong>Chevelu minimal</strong> : Les connexions se croisent le moins possible<br>
- <strong>Espacement suffisant</strong> : Laissez de l'espace pour router entre les composants<br>
- <strong>Orientation logique</strong> : Alignez les composants dans le sens du signal<br>
- <strong>Accessibilité</strong> : Les points de test et composants à souder sont accessibles<br>
N'hésitez pas à réorganiser plusieurs fois jusqu'à satisfaction."
image="placement-optimise.png" %}

{% include message.html
title="Condensateurs de découplage"
message="Les condensateurs de découplage (bypass capacitors) doivent être placés AU PLUS PRÈS des broches d'alimentation des circuits intégrés, avec des pistes courtes et directes. C'est critique pour le bon fonctionnement."
status="is-warning"
icon="fas fa-bolt" %}

---

## Définir le contour du PCB

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Sélectionner la couche Edge.Cuts"
content="Avant de tracer le contour, sélectionnez la couche <strong>Edge.Cuts</strong> dans le sélecteur de couche en haut. Cette couche définit où la carte sera découpée lors de la fabrication."
image="selectionner-edge-cuts.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Tracer un rectangle simple"
content="Pour un PCB rectangulaire simple :<br>
1. Cliquez sur l'icône <strong>Rectangle</strong> dans la barre d'outils droite<br>
2. Cliquez pour définir le premier coin<br>
3. Étirez le rectangle pour englober tous vos composants avec de la marge<br>
4. Cliquez pour terminer<br>
Laissez au moins 3-5mm de marge autour des composants."
image="contour-rectangle.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Tracer un contour personnalisé"
content="Pour une forme plus complexe, utilisez l'outil <strong>Ligne</strong> :<br>
1. Sélectionnez l'outil ligne dans la couche Edge.Cuts<br>
2. Tracez le contour segment par segment<br>
3. Pour des courbes, utilisez l'outil <strong>Arc</strong><br>
4. Le contour doit former une boucle fermée complète<br>
Vous pouvez ajouter des congés d'angle avec l'outil approprié." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 4 : Ajouter des trous de fixation"
content="Pour ajouter des trous de montage (mounting holes) :<br>
1. Allez dans <strong>Placer > Empreinte</strong> ou appuyez sur <strong>O</strong><br>
2. Cherchez 'MountingHole' dans la bibliothèque<br>
3. Choisissez le diamètre approprié (ex: MountingHole_3.2mm_M3)<br>
4. Placez les trous aux quatre coins ou selon vos besoins<br>
Respectez les distances minimales des bords (généralement 3mm minimum)."
image="trous-fixation.png" %}

{% include message.html
title="Dimensions standards"
message="Les dimensions courantes de PCB sont : 100x100mm, 100x80mm, 50x50mm. Vérifiez les tarifs de votre fabricant : certaines dimensions sont moins chères que d'autres."
status="is-info"
icon="fas fa-ruler" %}

---

## Configurer les règles de conception

{% include step-tuto.html
greyBackground = true
title = "Qu'est-ce que les règles de conception ?"
content="Les règles de conception (Design Rules) définissent les contraintes de fabrication :<br>
- Largeur minimale des pistes<br>
- Espacement minimum entre pistes<br>
- Diamètre des vias<br>
- Clearance (distance de sécurité)<br>
Ces valeurs dépendent des capacités de votre fabricant de PCB." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Ouvrir la configuration"
content="Allez dans <strong>Fichier > Configuration du circuit imprimé</strong>. Plusieurs onglets apparaissent : Couches, Règles de conception, Classes de nets, etc."
image="ouvrir-config.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Définir les contraintes"
content="Dans l'onglet <strong>Contraintes</strong>, configurez les valeurs minimales :<br><br>
<strong>Pour un PCB standard 2 couches :</strong><br>
- Clearance minimum : <code>0.2mm</code><br>
- Largeur de piste minimum : <code>0.2mm</code><br>
- Largeur de piste maximum : <code>2mm</code> (ou plus selon besoins)<br>
- Via diamètre minimum : <code>0.6mm</code><br>
- Via diamètre de perçage : <code>0.3mm</code><br><br>
Ces valeurs fonctionnent avec la plupart des fabricants standards (PCBWay, JLCPCB, etc.)." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Classes de nets (optionnel)"
content="Pour des pistes spécifiques (alimentation, signaux haute vitesse), créez des classes de nets :<br>
1. Allez dans l'onglet <strong>Classes de nets</strong><br>
2. Créez une classe (ex: 'Power' pour l'alimentation)<br>
3. Définissez une largeur de piste plus importante (ex: 0.5mm ou 1mm)<br>
4. Assignez les nets correspondants (VCC, GND, +5V, etc.)<br>
Les pistes d'alimentation seront automatiquement plus larges."
image="classes-nets.png" %}

{% include message.html
title="Consultez votre fabricant"
message="Avant de finaliser vos règles, consultez les spécifications techniques de votre fabricant de PCB. Chaque fabricant a ses propres capacités et contraintes. Respecter ces spécifications évite les erreurs de fabrication."
status="is-warning"
icon="fas fa-industry" %}

---

## Router les pistes

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Commencer une piste"
content="Pour router une connexion :<br>
1. Appuyez sur <strong>X</strong> ou cliquez sur l'icône 'Router des pistes'<br>
2. Cliquez sur une pastille de départ<br>
3. Suivez le chevelu (ligne blanche) vers la destination<br>
4. Cliquez pour créer des segments<br>
5. Terminez sur la pastille d'arrivée<br>
La piste apparaît en couleur selon la couche active."
image="router-piste.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Changer de couche avec des vias"
content="Pour passer d'une couche à l'autre pendant le routage :<br>
1. Pendant que vous tracez une piste, appuyez sur <strong>V</strong><br>
2. Un via (trou métallisé) est automatiquement placé<br>
3. La couche active bascule (F.Cu ↔ B.Cu)<br>
4. Continuez à router sur la nouvelle couche<br>
Utilisez les vias intelligemment pour éviter les croisements de pistes."
image="via-changement-couche.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Modes de routage"
content="Pcbnew propose plusieurs modes de routage (changez avec <strong>/</strong> ou <strong>\\</strong>) :<br>
<strong>Mode 1 - 45°</strong> : Les pistes suivent des angles de 45° (recommandé)<br>
<strong>Mode 2 - 90°</strong> : Angles droits (à éviter pour les signaux rapides)<br>
<strong>Mode 3 - Libre</strong> : Angles quelconques (pour cas particuliers)<br>
<strong>Push and shove</strong> : Les pistes existantes sont écartées automatiquement<br>
Pour la plupart des cas, utilisez le mode 45° avec push and shove activé." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 4 : Router les signaux"
content="Ordre de routage recommandé :<br>
1. <strong>Signaux critiques</strong> : Horloges, signaux haute vitesse, différentiels<br>
2. <strong>Alimentation principale</strong> : VCC, GND (ou utilisez des plans de masse)<br>
3. <strong>Signaux normaux</strong> : GPIO, I2C, SPI, UART, etc.<br>
4. <strong>Signaux secondaires</strong> : LEDs, boutons, connecteurs auxiliaires<br>
Gardez les pistes courtes et directes. Évitez les angles de 90° aigus." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 5 : Largeur des pistes"
content="Adaptez la largeur selon le courant :<br>
- <strong>0.2-0.3mm</strong> : Signaux faible courant (&lt;100mA)<br>
- <strong>0.5mm</strong> : Signaux moyens (100-500mA)<br>
- <strong>1-2mm</strong> : Alimentation forte (500mA-3A)<br>
- <strong>&gt;2mm</strong> : Très fort courant (&gt;3A)<br>
Changez la largeur pendant le routage : appuyez sur <strong>W</strong> puis tapez la valeur.<br>
Utilisez des calculateurs en ligne pour dimensionner précisément selon le courant."%}

{% include message.html
title="Astuce - Déplacement de pistes"
message="Pour déplacer une piste déjà routée, appuyez sur <strong>D</strong> (Drag) au lieu de <strong>M</strong> (Move). Cela déplace la piste en maintenant les connexions, ce qui est beaucoup plus pratique."
status="is-success"
icon="fas fa-arrows-alt" %}

---

## Plans de masse et zones de cuivre

{% include step-tuto.html
greyBackground = true
title = "Qu'est-ce qu'un plan de masse ?"
content="Un plan de masse (ground plane ou copper pour) est une grande surface de cuivre connectée à la masse (GND). Avantages :<br>
- Réduit les interférences électromagnétiques (EMI)<br>
- Facilite le routage (pas besoin de router tous les GND)<br>
- Améliore la dissipation thermique<br>
- Réduit l'impédance de masse<br>
C'est une bonne pratique pour presque tous les PCB." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Créer une zone de cuivre"
content="Pour créer un plan de masse sur la face arrière :<br>
1. Sélectionnez la couche <strong>F.Cu</strong> (front copper)<br>
2. Cliquez sur l'icône <strong>Ajouter une zone</strong> (ou appuyez sur <strong>Ctrl+Shift+Z</strong>)<br>
3. Une fenêtre s'ouvre : sélectionnez le net <strong>GND</strong><br>
4. Cliquez pour dessiner le contour de la zone (généralement tout le PCB)<br>
5. Double-cliquez pour terminer"
image="creer-zone-cuivre.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Configurer la zone"
content="Dans la fenêtre de configuration de zone, réglez :<br>
<strong>Net</strong> : GND (ou le net souhaité)<br>
<strong>Clearance</strong> : 0.2mm (distance de sécurité)<br>
<strong>Pad connection</strong> : Thermal reliefs (connexions thermiques)<br>
<strong>Priority</strong> : 0 (pour le plan de masse principal)<br>
<strong>Fill type</strong> : Solid (plein)<br>
Les thermal reliefs facilitent la soudure en limitant l'évacuation de chaleur."
image="configurer-zone.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Remplir la zone"
content="Pour visualiser le remplissage de cuivre :<br>
1. Appuyez sur <strong>B</strong> pour remplir toutes les zones (Fill all zones)<br>
2. Le plan de masse se remplit en évitant automatiquement les autres pistes et pastilles<br>
3. Pour vider (pour modifier), appuyez sur <strong>Ctrl+B</strong> (Unfill all zones)<br>
Le plan s'adapte automatiquement quand vous modifiez le routage."
image="remplir-zone.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 4 : Ajouter un plan de masse sur l'autre face"
content="Pour les PCB 2 couches, ajoutez aussi un plan de masse sur F.Cu :<br>
1. Sélectionnez la couche <strong>F.Cu</strong><br>
2. Répétez les étapes précédentes<br>
3. Remplissez avec <strong>B</strong><br>
Vous avez maintenant un plan de masse des deux côtés, ce qui améliore grandement les performances électriques."
image="plan-double-face.png" %}

{% include message.html
title="Connexions thermiques"
message="Les thermal reliefs (connexions thermiques) sont essentielles : elles connectent les pastilles au plan de masse via des 'ponts' fins. Sans elles, il serait très difficile de souder car tout le plan agirait comme un dissipateur thermique."
status="is-info"
icon="fas fa-fire" %}

---

## Vérification DRC (Design Rule Check)

{% include step-tuto.html
greyBackground = true
title = "Qu'est-ce que le DRC ?"
content="Le DRC (Design Rule Check) vérifie automatiquement que votre PCB respecte les règles de conception définies :<br>
- Espacements entre pistes<br>
- Largeur minimale des pistes<br>
- Chevauchements non autorisés<br>
- Connexions manquantes (chevelu non routé)<br>
- Vias trop proches des bords<br>
C'est indispensable avant d'envoyer les fichiers en fabrication." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Lancer le DRC"
content="Allez dans <strong>Inspecter > Vérificateur de règles de conception</strong> ou cliquez sur l'icône coccinelle. La fenêtre DRC s'ouvre avec plusieurs onglets."
image="lancer-drc.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Exécuter la vérification"
content="Dans la fenêtre DRC :<br>
1. Cliquez sur <strong>Exécuter DRC</strong><br>
2. L'outil analyse votre PCB (cela peut prendre quelques secondes)<br>
3. Les erreurs et avertissements s'affichent dans la liste<br>
4. Le compteur indique le nombre de problèmes détectés<br>
Double-cliquez sur une erreur pour naviguer vers l'emplacement concerné." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Corriger les erreurs"
content="Types d'erreurs courantes et solutions :<br><br>
<strong>Clearance violation</strong> : Deux pistes trop proches → Écartez-les ou changez le routage<br>
<strong>Track width</strong> : Piste trop fine → Élargissez la piste<br>
<strong>Unconnected items</strong> : Chevelu non routé → Terminez le routage ou supprimez si erreur<br>
<strong>Via too close to edge</strong> : Via trop proche du bord → Déplacez le via<br><br>
Corrigez toutes les erreurs une par une, puis relancez le DRC jusqu'à obtenir 0 erreur." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 4 : Vérifier les avertissements"
content="Les avertissements (warnings) ne bloquent pas la fabrication mais méritent attention :<br>
- <strong>Silkscreen over pad</strong> : Sérigraphie sur une pastille (sera effacée)<br>
- <strong>Courtyard overlap</strong> : Composants trop proches (problème d'assemblage potentiel)<br>
- <strong>Missing courtyard</strong> : Empreinte sans courtyard défini<br>
Évaluez chaque avertissement : certains sont acceptables, d'autres doivent être corrigés."
image="avertissements-drc.png" %}

{% include message.html
title="Objectif : 0 erreur"
message="Un PCB prêt pour la fabrication doit avoir 0 erreur DRC. Les avertissements peuvent parfois être acceptés selon le contexte, mais les erreurs doivent TOUTES être corrigées."
status="is-warning"
icon="fas fa-exclamation-triangle" %}

---

## Sérigraphie et finitions

{% include step-tuto.html
greyBackground = true
title = "Ajouter du texte sur la sérigraphie"
content="La sérigraphie (silkscreen) affiche des informations sur le PCB fini :<br>
1. Sélectionnez la couche <strong>F.SilkS</strong> (sérigraphie face avant)<br>
2. Cliquez sur l'icône <strong>Ajouter du texte</strong> (ou appuyez sur <strong>Ctrl+Shift+T</strong>)<br>
3. Tapez votre texte (nom du projet, version, votre nom, date, etc.)<br>
4. Placez et ajustez la taille (généralement 1-1.5mm de hauteur)<br>
Ajoutez des informations utiles : nom du projet, version, date, votre logo, etc."
image="ajouter-texte.png" %}

{% include step-tuto.html
greyBackground = true
title = "Améliorer les références des composants"
content="Les références (R1, C1, U1...) sont automatiquement placées mais souvent mal positionnées :<br>
1. Déplacez-les pour qu'elles soient lisibles et ne chevauchent rien<br>
2. Orientez-les dans le même sens si possible<br>
3. Pour masquer une référence : sélectionnez-la, appuyez sur <strong>E</strong> et décochez 'Visible'<br>
4. Vérifiez qu'aucune référence ne chevauche une pastille<br>
Une sérigraphie propre facilite grandement l'assemblage et le débogage."
image="references-composants.png" %}

{% include step-tuto.html
greyBackground = true
title = "Vérifier visuellement le PCB"
content="Avant de générer les fichiers de fabrication, faites une vérification visuelle complète :<br>
- Toutes les pistes sont routées (pas de chevelu blanc restant)<br>
- Les plans de masse sont remplis correctement<br>
- Les références de composants sont lisibles<br>
- La sérigraphie ne chevauche pas les pastilles<br>
- Le contour Edge.Cuts est fermé et propre<br>
- Les trous de fixation sont présents si nécessaires<br>
Prenez le temps de vérifier, c'est plus facile maintenant qu'après fabrication !" %}

{% include message.html
title="Conseil - Vue 3D"
message="Utilisez la vue 3D (Alt+3 ou menu Vue > Vue 3D) pour visualiser votre PCB en trois dimensions. C'est excellent pour détecter les problèmes et avoir un aperçu du résultat final."
status="is-success"
icon="fas fa-cube" %}

---

## Prochaines étapes et ressources

Félicitations ! Vous maîtrisez maintenant les bases de Pcbnew. Vous savez créer un PCB complet depuis le schéma jusqu'aux fichiers de fabrication.

### Pour aller plus loin

Une fois à l'aise avec les bases, explorez ces fonctionnalités avancées :

- **Routage automatique** : Utilisation d'auto-routeurs (Freerouting, etc.)
- **PCB multi-couches** : 4, 6, 8 couches ou plus
- **Paires différentielles** : Routage de signaux haute vitesse (USB, HDMI, etc.)
- **Calculs d'impédance** : Adaptation d'impédance pour RF et haute vitesse
- **Longueur de pistes** : Égalisation pour signaux synchrones (DDR, etc.)
- **PCB flex ou rigide-flex** : Circuits souples
- **Assemblage CMS** : Génération des fichiers Pick-and-Place pour assemblage automatique

{% include message.html
title="Assemblage du PCB"
message="Une fois vos PCB reçus, il faudra les assembler (souder les composants). Commandez vos composants chez Mouser, Digikey, Farnell ou RS Components. Pour le CMS, les fabricants (JLCPCB, PCBWay) proposent aussi des services d'assemblage économiques."
status="is-info"
icon="fas fa-microchip" %}

---

## Bonnes pratiques de conception PCB

### Placement et routage

- **Flux de signal logique** : Organisez entrée → traitement → sortie
- **Signaux sensibles courts** : Horloges et signaux rapides les plus courts possible
- **Découplage proche** : Condensateurs de découplage au plus près des CI
- **Retour de masse** : Assurez un chemin de retour court pour tous les signaux
- **Évitez les boucles** : Les boucles de courant créent des interférences

### Thermique et mécanique

- **Dissipation thermique** : Zones de cuivre larges pour composants chauds
- **Contraintes mécaniques** : Renforcez les zones de contrainte (connecteurs, etc.)
- **Trous de fixation** : Toujours prévoir des points de montage
- **Clearance mécanique** : Vérifiez les hauteurs de composants et boîtiers

### Fabrication et assemblage

- **Marges de bord** : 3-5mm minimum des bords pour composants et pistes
- **Orientation composants** : Même orientation si possible (facilite l'assemblage)
- **Points de test** : Ajoutez des testpoints pour débogage
- **Numérotation logique** : Références organisées (de gauche à droite, haut en bas)
- **Documentation** : Notes de version, schémas, BOM sur/avec le PCB

---

## Ressources complémentaires

Pour approfondir vos connaissances sur Pcbnew et la conception de PCB :

- [Documentation officielle Pcbnew](https://docs.kicad.org/master/fr/pcbnew/pcbnew.html)
- [Calculateur de largeur de pistes](https://www.4pcb.com/trace-width-calculator.html)
- [Forum KiCAD](https://forum.kicad.info/)
- [EEVblog - Tutoriels PCB](https://www.eevblog.com/)
- [Guide des fabricants de PCB](https://pcbshopper.com/)
- [Calculateur d'impédance](https://www.eeweb.com/tools/microstrip-impedance/)

{% include message.html
title="Continuez à pratiquer !"
message="La conception de PCB est un art qui s'améliore avec la pratique. Commencez simple, apprenez de chaque projet, et n'ayez pas peur de faire des erreurs (c'est comme ça qu'on apprend !). Bon routage !"
status="is-success"
icon="fas fa-graduation-cap" %}

---

## Pour aller plus loin

{%
  include card_collections.html
  title="Tutoriels KiCAD"
  description="Explorez d'autres tutoriels pour maîtriser KiCAD"
  type="tutorial"
%}
