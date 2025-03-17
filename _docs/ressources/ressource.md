---
layout: documentation
hide_hero: false
hero_image: "placeholder.png"
hero_darken: true
image: "placeholder.png"
component_toc: true
doc_header: true
type: ressource
order: 1

title: Exemple de ressource
subtitle: Des informations sur cette ressource
description: Vous trouverez ici plus d'informations sur cette ressource
author: Votre Nom

manufacturer:
  - name: Manufacturer
    link: "https://example.com/manufacturer"

working_area: 200x200x200mm
materials:
  - name: PLA
    link: "https://example.com/pla"
  - name: PETG
    link: "https://example.com/petg"
file_extensions:
  - name: STL
    link: "https://example.com/pla"
  - name: 3MF
    link: "https://example.com/petg"
  - name: OBJ
    link: "https://example.com/petg"
precision: 0.15mm
speed: 4
access_level: 0

time: 2
difficulty: 1
compatibilities-os: win, mac, lin

prerequisites:
  - label: Aucun pré-requis nécessaire
    link: ""

softwares: 
  - label: Aucun logiciel requis
    link: ""

hardwares: 
  - label: Aucune machine requise
    link: ""

todo: 100
---

## Introduction

Bienvenue sur la page de démonstration des fonctionnalités. Ce template propose plusieurs éléments modulaires que vous pouvez facilement intégrer dans vos pages de documentation. Voici quelques exemples des fonctionnalités disponibles.



## Pour aller plus loin

{%
  include card_collections.html
  title="Pour aller plus loin"
  description="Explorez d'autres tutoriels pour approfondir vos connaissances"
  type="tutorial"
%}
