---
layout: documentation
hide_hero: false
hero_image: "/docs/tutorial/kicad-fabrication-pcb/hero.png"
hero_darken: true
image: "hero.png"
component_toc: true
doc_header: true
type: tutorial
order: 5

title: Fabrication de PCB
subtitle: De KiCad à la carte physique
description: Apprenez à générer les fichiers Gerber, comprendre les paramètres de fabrication et commander vos circuits imprimés.
author: Alban Petit

time: 2
difficulty: 2
compatibilities-os: win, mac, lin

prerequisites:
  - label: PCB terminé et vérifié dans Pcbnew
    link: "/electronic-design/docs/tutorial/kicad-pcbnew-bases"

softwares:
  - label: KiCAD (version 8.0 ou supérieure)
    link: "https://www.kicad.org/"

hardwares:
  - label: Ordinateur avec connexion internet
    link: ""

todo: 100
---

## Introduction

Une fois votre PCB conçu et vérifié dans Pcbnew, la prochaine étape est de le faire fabriquer. Ce tutoriel vous guide à travers :
- L'export des fichiers Gerber (format standard de fabrication)
- La compréhension des paramètres de fabrication
- L'utilisation du service Aisler pour commander vos PCB

{% include message.html
title="Prérequis important"
message="Avant d'exporter vos fichiers de fabrication, assurez-vous que votre PCB est complètement terminé : routage achevé, DRC passé sans erreur, plans de masse remplis, et sérigraphie finalisée."
status="is-warning"
icon="fas fa-exclamation-triangle" %}

---

## Comprendre les fichiers Gerber

{% include step-tuto.html
greyBackground = true
title = "Qu'est-ce qu'un fichier Gerber ?"
content="Les fichiers Gerber (format RS-274X ou Gerber X2) sont le standard industriel pour la fabrication de PCB. Ils décrivent chaque couche de votre circuit imprimé :<br>
- Couches de cuivre (F.Cu, B.Cu, couches internes)<br>
- Masque de soudure (soldermask)<br>
- Sérigraphie (silkscreen)<br>
- Contours de découpe (Edge.Cuts)<br>
- Fichiers de perçage (drill files)<br>
Le fabricant utilise ces fichiers pour créer les photomasques et piloter les machines de production." %}

{% include step-tuto.html
greyBackground = true
title = "Fichiers de perçage (Drill files)"
content="En complément des Gerber, les fichiers de perçage décrivent tous les trous :<br>
- Trous métallisés (vias, pastilles traversantes)<br>
- Trous non métallisés (trous de fixation)<br>
Format : généralement Excellon (.drl) ou Gerber<br>
Ces fichiers indiquent la position, le diamètre et le type de chaque trou." %}

{% include message.html
title="Un ensemble complet"
message="Un jeu de fichiers Gerber complet contient typiquement 8-12 fichiers pour un PCB 2 couches : cuivre dessus/dessous, masque de soudure dessus/dessous, sérigraphie dessus/dessous, contour, perçage, et parfois fichier de paste pour l'assemblage CMS."
status="is-info"
icon="fas fa-file-archive" %}

---

## Visualiser et vérifier les fichiers Gerber

{% include step-tuto.html
greyBackground = true
title = "Utiliser le visualiseur Gerber de KiCAD"
content="KiCAD inclut un visualiseur Gerber intégré. Depuis le gestionnaire de projet, cliquez sur <strong>Visualiseur Gerber</strong> ou allez dans Fichier > Ouvrir le visualiseur Gerber depuis Pcbnew."
image="ouvrir-visualiseur.png" %}

{% include step-tuto.html
greyBackground = true
title = "Charger les fichiers Gerber"
content="Dans le visualiseur :<br>
1. Allez dans <strong>Fichier > Ouvrir les fichiers Gerber</strong><br>
2. Sélectionnez TOUS vos fichiers .gbr du dossier gerber<br>
3. Ouvrez aussi les fichiers de perçage .drl<br>
4. Tous les fichiers s'affichent dans le panneau de gauche<br>
Activez/désactivez les couches pour inspecter chaque élément." %}

{% include step-tuto.html
greyBackground = true
title = "Points de vérification"
content="Vérifiez visuellement dans le visualiseur Gerber :<br>
✓ Le contour Edge.Cuts est complet et fermé<br>
✓ Toutes les pistes et zones de cuivre sont présentes<br>
✓ Le masque de soudure couvre bien le cuivre (sauf les pastilles)<br>
✓ La sérigraphie est lisible et ne chevauche pas les pastilles<br>
✓ Les trous de perçage sont bien positionnés sur les pastilles<br>
✓ Aucune zone vide ou manquante<br>
Comparez avec votre PCB dans Pcbnew pour confirmer."
image="verification-gerber.png" %}

{% include message.html
title="Erreurs courantes à vérifier"
message="Problèmes fréquents dans les Gerber : contour non fermé (la carte ne sera pas découpée correctement), sérigraphie sur pastilles (sera supprimée), trous mal alignés, zones de cuivre non remplies. Corrigez dans Pcbnew et réexportez si nécessaire."
status="is-warning"
icon="fas fa-exclamation-triangle" %}

---

## Comprendre les paramètres de fabrication

{% include step-tuto.html
greyBackground = true
title = "Nombre de couches"
content="<strong>2 couches</strong> : Le plus courant et économique. Cuivre dessus + dessous.<br>
<strong>4 couches</strong> : Ajoute 2 couches internes, utile pour les cartes complexes avec beaucoup de signaux ou pour des plans d'alimentation dédiés.<br>
<strong>6+ couches</strong> : Pour circuits très complexes, haute vitesse, ou impédance contrôlée.<br><br>
Pour débuter : 2 couches suffisent pour 90% des projets." %}

{% include step-tuto.html
greyBackground = true
title = "Épaisseur du PCB"
content="<strong>Standard : 1.6mm</strong> (le plus courant et économique)<br>
<strong>Autres : 0.8mm, 1.0mm, 2.0mm</strong><br><br>
<strong>Choix selon usage :</strong><br>
- <strong>1.6mm</strong> : Usage général, bon compromis rigidité/coût<br>
- <strong>1.0mm</strong> : Cartes plus compactes, électronique portable<br>
- <strong>2.0mm</strong> : Applications mécaniques, fortes contraintes<br><br>
Vérifiez les connecteurs : certains sont prévus pour une épaisseur spécifique." %}

{% include step-tuto.html
greyBackground = true
title = "Épaisseur du cuivre"
content="Exprimée en oz (once par pied carré) ou µm :<br>
<strong>1 oz (35µm)</strong> : Standard, suffisant pour la plupart des applications<br>
<strong>2 oz (70µm)</strong> : Pour courants plus élevés (&gt;3A par piste)<br>
<strong>0.5 oz (18µm)</strong> : Moins courant, pour circuits très fins<br><br>
Plus de cuivre = meilleure conduction mais coût supérieur.<br>
Pour débuter : <strong>1 oz</strong> est le choix standard." %}

{% include step-tuto.html
greyBackground = true
title = "Couleur du masque de soudure (Soldermask)"
content="Le masque de soudure protège le cuivre et donne sa couleur au PCB :<br>
<strong>Vert</strong> : Standard, le moins cher<br>
<strong>Bleu</strong> : Populaire, légèrement plus cher<br>
<strong>Rouge, Noir, Blanc, Jaune</strong> : Autres couleurs disponibles<br>
<strong>Transparent/None</strong> : Pas de masque (rare, applications spéciales)<br><br>
La couleur n'affecte pas les performances, c'est purement esthétique.<br>
<strong>Vert = meilleur prix</strong>, autres couleurs = supplément." %}

{% include step-tuto.html
greyBackground = true
title = "Couleur de la sérigraphie (Silkscreen)"
content="La sérigraphie imprime les marquages, références et textes :<br>
<strong>Blanc</strong> : Standard sur masque vert/bleu/rouge/noir<br>
<strong>Noir</strong> : Sur masque blanc/jaune clair<br>
<strong>Jaune, Rouge</strong> : Disponible chez certains fabricants<br><br>
Le contraste est important : blanc sur fond sombre, noir sur fond clair.<br>
La sérigraphie est optionnelle mais fortement recommandée pour l'assemblage." %}

{% include step-tuto.html
greyBackground = true
title = "Finition de surface"
content="La finition protège le cuivre des pastilles et facilite la soudure :<br><br>
<strong>HASL (Hot Air Solder Leveling)</strong> :<br>
- Étamage à l'air chaud, le moins cher<br>
- Surface légèrement irrégulière<br>
- Bon pour soudure manuelle, limite pour CMS fins<br><br>
<strong>HASL Lead-Free (Sans plomb)</strong> :<br>
- Comme HASL mais RoHS compliant<br>
- Recommandé pour produits commerciaux<br><br>
<strong>ENIG (Electroless Nickel Immersion Gold)</strong> :<br>
- Surface plane et dorée<br>
- Excellent pour CMS fins, contacts, RF<br>
- Plus cher mais meilleure qualité<br>
- Longue durée de conservation<br><br>
Pour débuter : <strong>HASL Lead-Free</strong> (bon compromis)" %}


{% include message.html
title="Configuration standard recommandée"
message="<strong>Pour débuter, configuration économique :</strong><br>
• 2 couches<br>
• 1.6mm épaisseur<br>
• 1 oz cuivre<br>
• Vert + sérigraphie blanche<br>
• HASL Lead-Free<br>
• Vias tented<br>
Cette configuration est la moins chère et parfaitement adaptée à 90% des projets."
status="is-success"
icon="fas fa-star" %}

---

## Commander avec Aisler

{% include step-tuto.html
greyBackground = true
title = "Qu'est-ce qu'Aisler ?"
content="<strong>Aisler</strong> est un fabricant de PCB européen (Allemagne) offrant :<br>
- Prix compétitifs pour petites séries (3-20 PCB)<br>
- Qualité européenne certifiée<br>
- Livraison rapide en Europe (5-10 jours)<br>
- Intégration directe avec GitHub<br>
- Plugin KiCAD pour commande simplifiée<br>
- Support en anglais/allemand<br><br>
Site web : <a href='https://aisler.net/' target='_blank'>aisler.net</a>" %}

{% include step-tuto.html
greyBackground = true
title = "Créer un compte Aisler"
content="1. Allez sur <a href='https://aisler.net/' target='_blank'>aisler.net</a><br>
2. Cliquez sur <strong>Sign up</strong> en haut à droite<br>
3. Inscrivez-vous avec votre email ou compte GitHub<br>
4. Validez votre email<br>
5. Complétez votre profil (adresse de livraison)<br><br>
L'inscription est gratuite, vous ne payez que lors de la commande." %}

{% include step-tuto.html
greyBackground = true
title = "Méthode 1 : Upload manuel des Gerber"
content="La méthode classique pour commander :<br>
1. Connectez-vous à votre compte Aisler<br>
2. Cliquez sur <strong>Upload Project</strong> ou <strong>New Project</strong><br>
3. Compressez vos fichiers Gerber en .zip : sélectionnez tous les .gbr et .drl, clic droit > Compresser<br>
4. Glissez-déposez le fichier .zip sur la zone d'upload Aisler<br>
5. Aisler analyse automatiquement les fichiers<br>
6. Vérifiez l'aperçu généré automatiquement"
image="upload-gerber-aisler.png" %}

{% include step-tuto.html
greyBackground = true
title = "Configurer les paramètres de fabrication"
content="Après l'upload, configurez votre commande :<br><br>
<strong>Quantité</strong> : Nombre de PCB (minimum souvent 3)<br>
<strong>Layers</strong> : 2 layers (détecté automatiquement)<br>
<strong>Thickness</strong> : 1.6mm (standard)<br>
<strong>Color</strong> : Choisissez la couleur du masque de soudure<br>
<strong>Surface finish</strong> : HASL lead-free ou ENIG<br>
<strong>Copper weight</strong> : 1 oz (35µm)<br><br>
Aisler détecte automatiquement la plupart des paramètres depuis vos Gerber."
image="configurer-aisler.png" %}

{% include step-tuto.html
greyBackground = true
title = "Vérifier et valider"
content="Avant de commander :<br>
1. <strong>Vérifiez l'aperçu</strong> : Aisler affiche une vue 3D de votre PCB<br>
2. <strong>Vérifiez les dimensions</strong> : Contrôlez que la taille est correcte<br>
3. <strong>Consultez les warnings</strong> : Aisler signale les problèmes potentiels (pistes trop fines, espacements limites, etc.)<br>
4. <strong>Vérifiez le prix</strong> : Le prix s'affiche en fonction de la quantité et des options<br>
5. Cliquez sur <strong>Add to cart</strong> puis procédez au paiement" %}

{% include message.html
title="Délais de fabrication"
message="Aisler propose généralement 2 options :<br>
<strong>Standard</strong> : 10-15 jours (moins cher)<br>
<strong>Express</strong> : 5-7 jours (supplément)<br>
Les délais incluent fabrication + expédition en Europe. Ajoutez 3-5 jours pour assemblage si vous commandez l'assemblage CMS."
status="is-info"
icon="fas fa-shipping-fast" %}

---

## Plugin KiCAD pour Aisler

{% include step-tuto.html
greyBackground = true
title = "Installer le plugin Aisler"
content="Aisler propose un plugin KiCAD pour commander directement depuis Pcbnew :<br><br>
<strong>Installation via le gestionnaire de plugins :</strong><br>
1. Dans KiCAD, ouvrez Pcbnew<br>
2. Allez dans <strong>Outils > Plugins externes > Ouvrir le gestionnaire de plugins</strong><br>
3. Cherchez <strong>Aisler</strong> dans la liste<br>
4. Cliquez sur <strong>Installer</strong><br>
5. Redémarrez KiCAD<br><br>
Le plugin apparaît ensuite dans le menu Outils > External Plugins > Aisler."
image="installer-plugin-aisler.png" %}

{% include step-tuto.html
greyBackground = true
title = "Utiliser le plugin Aisler"
content="Une fois installé, pour commander directement :<br>
1. Ouvrez votre PCB dans Pcbnew<br>
2. Allez dans <strong>Outils > Plugins externes > Aisler Push</strong><br>
3. Le plugin génère automatiquement les Gerber<br>
4. Connectez-vous à votre compte Aisler (si ce n'est pas déjà fait)<br>
5. Les fichiers sont uploadés automatiquement<br>
6. Votre navigateur s'ouvre sur la page de configuration Aisler<br>
7. Configurez les paramètres et commandez<br><br>
<strong>Gain de temps énorme !</strong> Plus besoin d'exporter manuellement les Gerber."
image="utiliser-plugin-aisler.png" %}

{% include message.html
title="Avantage du plugin"
message="Le plugin Aisler automatise tout le processus : export Gerber + upload + vérification en un clic. Il garantit aussi que les bons paramètres d'export sont utilisés pour la compatibilité avec Aisler."
status="is-success"
icon="fas fa-rocket" %}

---


## Autres fabricants de PCB populaires

{% include step-tuto.html
greyBackground = true
title = "JLCPCB (Chine)"
content="<strong>JLCPCB</strong> : <a href='https://jlcpcb.com/' target='_blank'>jlcpcb.com</a><br><br>
<strong>Avantages :</strong><br>
- Prix très compétitifs (5 PCB pour $2)<br>
- Service d'assemblage CMS intégré<br>
- Composants en stock pour assemblage<br>
- Qualité correcte<br><br>
<strong>Inconvénients :</strong><br>
- Délais de livraison longs (15-30 jours)<br>
- Frais de douane possibles<br>
- Support en anglais<br><br>
Bon choix pour prototypes pas chers si le délai n'est pas critique." %}

{% include step-tuto.html
greyBackground = true
title = "PCBWay (Chine)"
content="<strong>PCBWay</strong> : <a href='https://www.pcbway.com/' target='_blank'>pcbway.com</a><br><br>
<strong>Avantages :</strong><br>
- Prix compétitifs<br>
- Assemblage CMS disponible<br>
- Large gamme de finitions et options<br>
- Qualité bonne<br><br>
<strong>Inconvénients :</strong><br>
- Similaire à JLCPCB : délais longs, douanes<br><br>
Alternative intéressante à JLCPCB avec options similaires." %}

{% include step-tuto.html
greyBackground = true
title = "Eurocircuits (Europe)"
content="<strong>Eurocircuits</strong> : <a href='https://www.eurocircuits.com/' target='_blank'>eurocircuits.com</a><br><br>
<strong>Avantages :</strong><br>
- Fabrication européenne (Belgique)<br>
- Qualité professionnelle excellente<br>
- Livraison rapide en Europe<br>
- Visualiseur en ligne puissant<br>
- Certifications industrielles<br><br>
<strong>Inconvénients :</strong><br>
- Prix plus élevés<br>
- Minimum de commande parfois plus élevé<br><br>
Pour projets professionnels nécessitant qualité certifiée." %}

{% include step-tuto.html
greyBackground = true
title = "OSH Park (USA)"
content="<strong>OSH Park</strong> : <a href='https://oshpark.com/' target='_blank'>oshpark.com</a><br><br>
<strong>Avantages :</strong><br>
- PCB violet distinctif (ENIG)<br>
- Excellente qualité<br>
- Support open-source<br>
- Upload direct depuis GitHub<br><br>
<strong>Inconvénients :</strong><br>
- Prix au pouce carré (peut être cher pour grandes cartes)<br>
- Livraison en Europe coûteuse et lente<br><br>
Populaire dans la communauté maker américaine." %}

---

## Fichiers de fabrication additionnels

{% include step-tuto.html
greyBackground = true
title = "BOM (Bill of Materials)"
content="La BOM liste tous les composants de votre PCB :<br>
- Référence (R1, C1, U1...)<br>
- Valeur (220R, 100nF, ATmega328...)<br>
- Empreinte (0805, SOIC-8...)<br>
- Quantité<br>
- Référence fabricant / distributeur<br><br>
<strong>Générer la BOM depuis KiCAD :</strong><br>
Dans Eeschema : <strong>Outils > Générer la nomenclature</strong><br>
Exportez en CSV ou utilisez un script personnalisé." %}

{% include step-tuto.html
greyBackground = true
title = "Fichier de pâte à braser (Stencil)"
content="Pour souder les composants CMS, un pochoir (stencil) applique la pâte à braser :<br><br>
Les fichiers F.Paste et B.Paste dans vos Gerber définissent les ouvertures du pochoir.<br><br>
Vous pouvez commander un pochoir métallique ou plastique avec votre PCB chez la plupart des fabricants.<br><br>
<strong>Épaisseurs courantes :</strong><br>
- 0.1mm (100µm) : Composants fins (0402, QFN fin pitch)<br>
- 0.12-0.15mm : Standard pour 0603, 0805, SOIC<br>
- 0.2mm : Composants plus gros" %}

{% include message.html
title="Package complet de fabrication"
message="Pour une commande professionnelle, préparez un package complet :<br>
• Fichiers Gerber (.gbr) + Drill (.drl)<br>
• BOM (liste des composants)<br>
• Schéma PDF<br>
• Notes de fabrication (si exigences spéciales)<br>
• Pick-and-Place (si assemblage)<br>
Compressez le tout en .zip avec un nom clair : <code>ProjectName_v1.0_2026-02-09.zip</code>"
status="is-success"
icon="fas fa-archive" %}

---

## Ressources et aller plus loin

### Capabilities des fabricants

Consultez les capabilities (capacités de fabrication) de votre fabricant :

- **Aisler** : [Capabilities](https://aisler.net/help/capabilities)
- **JLCPCB** : [Capabilities](https://jlcpcb.com/capabilities/Capabilities)
- **PCBWay** : [Capabilities](https://www.pcbway.com/capabilities.html)

### Guides et standards

- [IPC Standards](https://www.ipc.org/) : Standards industriels PCB
- [KiCAD Documentation - Gerber](https://docs.kicad.org/master/fr/pcbnew/pcbnew.html#generate-fabrication-files)

{% include message.html
title="Continuez à apprendre"
message="La fabrication de PCB devient plus facile avec l'expérience. Commencez simple, observez les résultats, et ajustez pour les versions suivantes. N'ayez pas peur de faire des erreurs - c'est comme ça qu'on apprend !"
status="is-success"
icon="fas fa-graduation-cap" %}

---

## Pour aller plus loin

### Assemblage CMS (SMT Assembly)

Une fois vos PCB reçus, vous pouvez :
- **Souder manuellement** : Fer à souder + flux pour CMS (composants 0805 et plus)
- **Hot air rework station** : Pistolet à air chaud pour CMS fins
- **Réflow au four** : Pâte à braser + pochoir + four de refusion (précis, pour composants fins)
- **Service d'assemblage** : JLCPCB, PCBWay proposent assemblage automatique à prix abordable

### PCB avancés

Explorez des fonctionnalités avancées :
- **PCB multi-couches** : 4, 6, 8 couches pour circuits complexes
- **PCB flex/rigide-flex** : Circuits souples pour électronique portable
- **Contrôle d'impédance** : Pour signaux haute fréquence (RF, USB 3.0, HDMI)
- **HDI (High Density Interconnect)** : Micro-vias, blind/buried vias
- **Embedded components** : Composants noyés dans le PCB

### Certifications et normes

Pour produits commerciaux, considérez :
- **RoHS** : Sans substances dangereuses (plomb, etc.)
- **UL** : Certification sécurité (ignifugation, etc.)
- **IPC Class 2/3** : Qualité fabrication (Class 3 = aéronautique, médical)
- **CE marking** : Conformité européenne

{%
  include card_collections.html
  title="Tutoriels KiCAD"
  description="Explorez d'autres tutoriels pour maîtriser KiCAD"
  type="tutorial"
%}
