---
layout: documentation
hide_hero: false
hero_image: "/docs/tutorial/installation-vscode-platformio/hero.png"
hero_darken: true
image: "hero.png"
component_toc: true
doc_header: true
type: tutorial
order: 10

title: Installation de VSCode et PlatformIO
subtitle: Configurez votre environnement de développement pour microcontrôleurs
description: Ce tutoriel explique comment installer Visual Studio Code et PlatformIO pour programmer des microcontrôleurs Arduino, ESP32, STM32 et bien d'autres.
author: Alban Petit

time: 1
difficulty: 1
compatibilities-os: win, mac, lin

prerequisites:
  - label: Droits administrateur sur votre ordinateur
    link: ""

softwares:
  - label: Visual Studio Code (dernière version)
    link: "https://code.visualstudio.com/"
  - label: PlatformIO IDE (extension VSCode)
    link: "https://platformio.org/"

hardwares:
  - label: Ordinateur avec au moins 4GB de RAM
    link: ""
  - label: Connexion internet pour télécharger les outils
    link: ""

todo: 100
---

## Introduction

**Visual Studio Code** (VSCode) est un éditeur de code léger et puissant développé par Microsoft. **PlatformIO** est une plateforme de développement professionnelle pour microcontrôleurs qui s'intègre à VSCode via une extension.

Ensemble, VSCode + PlatformIO offrent :
- Support de centaines de cartes de développement (Arduino, ESP32, ESP8266, STM32, Raspberry Pi Pico...)
- Gestion automatique des bibliothèques et dépendances
- Compilation, upload et débogage intégrés
- IntelliSense (autocomplétion intelligente)
- Gestion de projets multi-plateformes

Ce tutoriel vous guidera à travers l'installation complète sur Windows, macOS et Linux.

{% include message.html
title="Pourquoi PlatformIO plutôt qu'Arduino IDE ?"
message="PlatformIO offre une gestion avancée des projets, des builds plus rapides, une meilleure gestion des bibliothèques, le support de multiples plateformes dans un même projet, et des outils de débogage professionnels. C'est l'outil de référence pour les projets sérieux."
status="is-info"
icon="fas fa-info-circle" %}

---

## Installation de Visual Studio Code

### Installation sur Windows

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Téléchargement"
content="Rendez-vous sur le site officiel de VSCode à l'adresse [https://code.visualstudio.com/](https://code.visualstudio.com/). Cliquez sur le bouton de téléchargement pour Windows. Le fichier d'installation (<strong>VSCodeUserSetup-x64.exe</strong>) sera téléchargé." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Exécution de l'installateur"
content="Double-cliquez sur le fichier téléchargé pour lancer l'installation. Acceptez les conditions d'utilisation." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Options d'installation"
content="Cochez les options suivantes (recommandées) :<br>
- Ajouter l'action 'Ouvrir avec Code' au menu contextuel des fichiers<br>
- Ajouter l'action 'Ouvrir avec Code' au menu contextuel des répertoires<br>
- Ajouter à PATH (important pour PlatformIO)<br>
- Créer une icône sur le bureau<br><br>
Cliquez sur <strong>Suivant</strong> puis <strong>Installer</strong>." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 4 : Finalisation"
content="Une fois l'installation terminée, cochez <strong>Lancer Visual Studio Code</strong> et cliquez sur <strong>Terminer</strong>. VSCode se lance pour la première fois." %}

### Installation sur macOS

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Téléchargement"
content="Rendez-vous sur [https://code.visualstudio.com/](https://code.visualstudio.com/). Téléchargez la version correspondant à votre processeur :<br>
- <strong>Apple Silicon</strong> (M1, M2, M3, M4) : Télécharger .zip<br>
- <strong>Intel</strong> : Télécharger .zip" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Installation"
content="1. Double-cliquez sur le fichier .zip téléchargé pour le décompresser<br>
2. Glissez-déposez <strong>Visual Studio Code.app</strong> dans le dossier <strong>Applications</strong><br>
3. Ouvrez le dossier Applications et double-cliquez sur Visual Studio Code" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Premier lancement"
content="Si macOS affiche un message de sécurité, allez dans <strong>Préférences Système > Confidentialité et sécurité</strong>, puis autorisez l'exécution de Visual Studio Code." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 4 : Installer 'code' dans le PATH"
content="Pour utiliser VSCode depuis le terminal (utile pour PlatformIO) :<br>
1. Ouvrez VSCode<br>
2. Appuyez sur <strong>Cmd+Shift+P</strong> pour ouvrir la palette de commandes<br>
3. Tapez <strong>shell command</strong><br>
4. Sélectionnez <strong>Shell Command: Install 'code' command in PATH</strong><br>
5. Validez avec Entrée" %}

### Installation sur Linux

{% include step-tuto.html
greyBackground = true
title = "Ubuntu / Debian (méthode recommandée)"
content="Téléchargez et installez le paquet .deb depuis le site officiel :<br><br>
1. Allez sur [https://code.visualstudio.com/](https://code.visualstudio.com/)<br>
2. Téléchargez le fichier <strong>.deb</strong><br>
3. Installez avec :<br>
<code>sudo apt install ./code_*.deb</code><br><br>
Ou via le dépôt officiel :<br>
<code>wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg</code><br>
<code>sudo install -o root -g root -m 644 packages.microsoft.gpg /etc/apt/trusted.gpg.d/</code><br>
<code>sudo sh -c 'echo \"deb [arch=amd64] https://packages.microsoft.com/repos/code stable main\" > /etc/apt/sources.list.d/vscode.list'</code><br>
<code>sudo apt update</code><br>
<code>sudo apt install code</code>" %}

{% include step-tuto.html
greyBackground = true
title = "Fedora / Red Hat / CentOS"
content="Installez le paquet RPM :<br><br>
<code>sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc</code><br>
<code>sudo sh -c 'echo -e \"[code]\\nname=Visual Studio Code\\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\\nenabled=1\\ngpgcheck=1\\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc\" > /etc/yum.repos.d/vscode.repo'</code><br><br>
Puis :<br>
<code>sudo dnf check-update</code><br>
<code>sudo dnf install code</code>" %}

{% include step-tuto.html
greyBackground = true
title = "Arch Linux"
content="VSCode est disponible dans AUR :<br><br>
<code>yay -S visual-studio-code-bin</code><br><br>
Ou utilisez Snap :<br>
<code>sudo snap install code --classic</code>" %}

{% include message.html
title="Permissions USB sur Linux"
message="Sur Linux, vous devrez configurer les permissions USB pour programmer les microcontrôleurs. Cela sera expliqué plus loin dans la section dédiée."
status="is-warning"
icon="fas fa-exclamation-triangle" %}

---

## Vérification de l'installation de VSCode

{% include step-tuto.html
greyBackground = true
title = "Vérifier que VSCode fonctionne"
content="Lancez Visual Studio Code. Vous devriez voir :<br>
- La fenêtre principale avec la page d'accueil<br>
- La barre d'activité sur la gauche (Explorateur, Recherche, Extensions...)<br>
- Un éditeur vide au centre<br><br>
Si vous voyez cette interface, VSCode est correctement installé !" %}

---

## Installation de PlatformIO

Maintenant que VSCode est installé, nous allons ajouter l'extension PlatformIO qui transforme VSCode en IDE complet pour microcontrôleurs.

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Ouvrir le gestionnaire d'extensions"
content="Dans VSCode, cliquez sur l'icône <strong>Extensions</strong> dans la barre d'activité de gauche (icône de carrés empilés) ou utilisez le raccourci :<br>
- Windows/Linux : <strong>Ctrl+Shift+X</strong><br>
- macOS : <strong>Cmd+Shift+X</strong>" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Rechercher PlatformIO"
content="Dans la barre de recherche des extensions, tapez <strong>platformio</strong>. Vous devriez voir l'extension <strong>PlatformIO IDE</strong> par PlatformIO." image="platformio-install.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Installer l'extension"
content="Cliquez sur le bouton <strong>Install</strong> (Installer). L'installation prend quelques minutes car PlatformIO télécharge automatiquement :<br>
- Python (si nécessaire)<br>
- PlatformIO Core<br>
- Les outils de compilation<br><br>
<strong>Soyez patient, ne fermez pas VSCode pendant l'installation !</strong>" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 4 : Attendre la fin de l'installation"
content="Une fois l'installation terminée, vous verrez :<br>
- Une icône PlatformIO (tête d'alien) dans la barre d'activité de gauche<br>
- Une notification indiquant que PlatformIO est prêt<br>
- Possiblement une demande de redémarrage de VSCode<br><br>
Si on vous le demande, cliquez sur <strong>Reload Now</strong> (Recharger maintenant)." %}

{% include message.html
title="Première installation longue"
message="La première installation de PlatformIO peut prendre 5-10 minutes selon votre connexion internet. PlatformIO télécharge tous les outils nécessaires (compilateurs, outils de flash, etc.). C'est normal, soyez patient !"
status="is-info"
icon="fas fa-clock" %}

---

## Vérification de l'installation de PlatformIO

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Ouvrir PlatformIO Home"
content="Cliquez sur l'icône <strong>PlatformIO</strong> (tête d'alien) dans la barre d'activité de gauche. Un panneau s'ouvre avec plusieurs options. Cliquez sur <strong>PIO Home</strong> puis <strong>Open</strong>." image="platformio-navbar.png" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Interface PlatformIO Home"
content="La page d'accueil de PlatformIO s'ouvre avec plusieurs sections :<br>
- <strong>New Project</strong> : Créer un nouveau projet<br>
- <strong>Open Project</strong> : Ouvrir un projet existant<br>
- <strong>Platforms</strong> : Gérer les plateformes supportées<br>
- <strong>Libraries</strong> : Gérer les bibliothèques<br>
- <strong>Boards</strong> : Voir les cartes supportées<br><br>
Si vous voyez cette page, <strong>félicitations</strong> ! PlatformIO est correctement installé." image="platformio-home.png" %}

---

## Configuration des permissions USB (Linux uniquement)

Sur Linux, vous devez configurer les permissions pour accéder aux ports USB sans sudo.

{% include step-tuto.html
greyBackground = true
title = "Ajouter l'utilisateur au groupe dialout"
content="Ouvrez un terminal et exécutez :<br><br>
<code>sudo usermod -a -G dialout $USER</code><br>
<code>sudo usermod -a -G plugdev $USER</code><br><br>
<strong>Déconnectez-vous puis reconnectez-vous</strong> (ou redémarrez l'ordinateur) pour que les changements prennent effet." %}

{% include step-tuto.html
greyBackground = true
title = "Installer les règles udev (optionnel)"
content="Pour un meilleur support de certaines cartes (ESP32, STM32...), installez les règles udev de PlatformIO :<br><br>
<code>curl -fsSL https://raw.githubusercontent.com/platformio/platformio-core/master/scripts/99-platformio-udev.rules | sudo tee /etc/udev/rules.d/99-platformio-udev.rules</code><br><br>
Puis rechargez les règles :<br>
<code>sudo udevadm control --reload-rules</code><br>
<code>sudo udevadm trigger</code>" %}

{% include message.html
title="Redémarrage nécessaire"
message="Après avoir ajouté votre utilisateur aux groupes dialout et plugdev, vous DEVEZ vous déconnecter et reconnecter (ou redémarrer) pour que les permissions soient effectives. Sinon PlatformIO ne pourra pas accéder aux ports USB."
status="is-warning"
icon="fas fa-exclamation-triangle" %}

---

## Créer votre premier projet PlatformIO

Testons l'installation en créant un projet simple de type "Blink".

{% include step-tuto.html
greyBackground = true
title = "Étape 1 : Nouveau projet"
content="1. Cliquez sur l'icône PlatformIO dans la barre de gauche<br>
2. Cliquez sur <strong>PIO Home > Open</strong><br>
3. Cliquez sur <strong>+ New Project</strong>" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 2 : Configuration du projet"
content="Remplissez les champs suivants :<br>
- <strong>Name</strong> : <code>test_blink</code><br>
- <strong>Board</strong> : Sélectionnez votre carte (par exemple : <code>Arduino Uno</code>, <code>ESP32 Dev Module</code>, <code>NodeMCU 1.0</code>...)<br>
- <strong>Framework</strong> : Laissez <code>Arduino</code> par défaut<br>
- <strong>Location</strong> : Laissez le chemin par défaut ou choisissez un dossier<br><br>
Cliquez sur <strong>Finish</strong>. PlatformIO crée le projet et télécharge les outils nécessaires pour votre carte." %}

{% include step-tuto.html
greyBackground = true
title = "Étape 3 : Code de test"
content="PlatformIO crée automatiquement la structure du projet. Ouvrez le fichier <strong>src/main.cpp</strong>. Remplacez le contenu par ce code de test Blink :<br><br>
<pre><code>#include &lt;Arduino.h&gt;

void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
  digitalWrite(LED_BUILTIN, HIGH);
  delay(1000);
  digitalWrite(LED_BUILTIN, LOW);
  delay(1000);
}</code></pre>" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 4 : Compiler le projet"
content="Pour compiler le projet :<br>
1. Cliquez sur l'icône <strong>✓</strong> (coche) dans la barre de statut en bas (Build)<br>
2. Ou utilisez le raccourci : <strong>Ctrl+Alt+B</strong> (Windows/Linux) / <strong>Cmd+Alt+B</strong> (macOS)<br><br>
PlatformIO compile le code. Si tout va bien, vous verrez <strong>SUCCESS</strong> dans le terminal." %}

{% include message.html
title="Première compilation longue"
message="La première compilation d'un projet pour une nouvelle plateforme peut prendre plusieurs minutes car PlatformIO télécharge le compilateur, les bibliothèques et frameworks nécessaires. Les compilations suivantes seront beaucoup plus rapides !"
status="is-info"
icon="fas fa-hourglass-half" %}

{% include step-tuto.html
greyBackground = true
title = "Étape 5 : Upload sur la carte (optionnel)"
content="Si vous avez une carte connectée, vous pouvez uploader le programme :<br>
1. Branchez votre carte via USB<br>
2. Cliquez sur l'icône <strong>→</strong> (flèche) dans la barre de statut (Upload)<br>
3. Ou utilisez le raccourci : <strong>Ctrl+Alt+U</strong> (Windows/Linux) / <strong>Cmd+Alt+U</strong> (macOS)<br><br>
PlatformIO compile et upload automatiquement. La LED de votre carte devrait clignoter !" %}

{% include message.html
title="Installation réussie !"
message="Si la compilation réussit, votre installation de VSCode + PlatformIO est complète et fonctionnelle. Vous êtes prêt à développer vos projets embarqués !"
status="is-success"
icon="fas fa-check-circle" %}

---

## Configuration recommandée de VSCode

Voici quelques réglages utiles pour améliorer votre expérience de développement.

{% include step-tuto.html
greyBackground = true
title = "Extensions VSCode utiles"
content="Installez ces extensions pour améliorer votre productivité :<br>
- <strong>C/C++</strong> (Microsoft) : IntelliSense pour C/C++<br>
- <strong>Better C++ Syntax</strong> : Meilleure coloration syntaxique<br>
- <strong>Bracket Pair Colorizer 2</strong> : Colore les paires de parenthèses<br>" %}

{% include step-tuto.html
greyBackground = true
title = "Raccourcis clavier PlatformIO"
content="Mémorisez ces raccourcis essentiels :<br><br>
<strong>Windows/Linux :</strong><br>
- <strong>Ctrl+Alt+B</strong> : Build (compiler)<br>
- <strong>Ctrl+Alt+U</strong> : Upload (téléverser)<br>
- <strong>Ctrl+Alt+S</strong> : Monitor série<br>
- <strong>Ctrl+Alt+T</strong> : Run task (tâche spécifique)<br><br>
<strong>macOS :</strong><br>
- <strong>Cmd+Alt+B</strong> : Build<br>
- <strong>Cmd+Alt+U</strong> : Upload<br>
- <strong>Cmd+Alt+S</strong> : Monitor série" %}

---

## Dépannage

### Problème : PlatformIO ne se lance pas après installation

{% include step-tuto.html
greyBackground = true
title = "Solution 1 : Réinstaller PlatformIO"
content="1. Désinstallez l'extension PlatformIO dans VSCode<br>
2. Fermez complètement VSCode<br>
3. Supprimez le dossier <code>~/.platformio</code> (Linux/macOS) ou <code>C:\\Users\\VotreNom\\.platformio</code> (Windows)<br>
4. Rouvrez VSCode et réinstallez PlatformIO" %}

{% include step-tuto.html
greyBackground = true
title = "Solution 2 : Problème de Python"
content="PlatformIO nécessite Python. Vérifiez que Python est bien installé :<br>
<code>python --version</code> ou <code>python3 --version</code><br><br>
Si Python n'est pas installé, téléchargez-le depuis [python.org](https://www.python.org/) et réinstallez PlatformIO." %}

### Problème : Port USB non détecté (Linux)

{% include step-tuto.html
greyBackground = true
title = "Vérifier les permissions USB"
content="Assurez-vous d'avoir suivi les étapes de configuration USB (section précédente) :<br>
<code>sudo usermod -a -G dialout $USER</code><br>
<code>sudo usermod -a -G plugdev $USER</code><br><br>
Puis déconnectez-vous et reconnectez-vous." %}

### Problème : Erreur de compilation "tool-chain not found"

{% include step-tuto.html
greyBackground = true
title = "Réinstaller la plateforme"
content="1. Ouvrez PlatformIO Home<br>
2. Allez dans <strong>Platforms > Installed</strong><br>
3. Trouvez votre plateforme (ex: Espressif 32) et cliquez sur <strong>Uninstall</strong><br>
4. Réinstallez la plateforme depuis <strong>Platforms > Embedded</strong><br>
5. Essayez de compiler à nouveau" %}

---

## Ressources et aller plus loin

### Documentation officielle

- [Documentation PlatformIO](https://docs.platformio.org/)
- [VSCode Documentation](https://code.visualstudio.com/docs)
- [PlatformIO Boards](https://platformio.org/boards) : Liste complète des cartes supportées
- [PlatformIO Libraries](https://platformio.org/lib) : Registre de bibliothèques

### Tutoriels et guides

- [PlatformIO Getting Started](https://docs.platformio.org/en/latest/integration/ide/vscode.html)
- [PlatformIO YouTube Channel](https://www.youtube.com/@PlatformIO)
- [Forum PlatformIO](https://community.platformio.org/)

### Commandes CLI utiles

Si vous préférez utiliser PlatformIO en ligne de commande :

```bash
# Créer un nouveau projet
pio project init --board <nom_carte>

# Compiler
pio run

# Upload
pio run --target upload

# Ouvrir le moniteur série
pio device monitor

# Lister les cartes disponibles
pio boards

# Rechercher une bibliothèque
pio lib search <nom_lib>

# Installer une bibliothèque
pio lib install <nom_lib>
```

### Structure d'un projet PlatformIO

```
mon_projet/
├── .pio/               # Fichiers de build (généré automatiquement)
├── include/            # Fichiers d'en-tête (.h)
├── lib/                # Bibliothèques privées
├── src/                # Code source (.cpp, .c)
│   └── main.cpp        # Fichier principal
├── test/               # Tests unitaires
├── platformio.ini      # Configuration du projet
└── .gitignore          # Fichiers à ignorer par Git
```

Le fichier **platformio.ini** configure le projet :

```ini
[env:myboard]
platform = espressif32
board = esp32dev
framework = arduino
monitor_speed = 115200
lib_deps =
    adafruit/Adafruit Sensor@^1.1.4
    bblanchon/ArduinoJson@^6.21.0
```

{% include message.html
title="Prochaines étapes"
message="Maintenant que VSCode et PlatformIO sont installés, vous êtes prêt à développer vos projets embarqués ! Explorez les exemples inclus, testez différentes cartes, et n'hésitez pas à consulter la documentation."
status="is-success"
icon="fas fa-rocket" %}

---

## Pour aller plus loin

{%
  include card_collections.html
  title="Tutoriels de programmation embarquée"
  description="Explorez d'autres tutoriels pour maîtriser la programmation de microcontrôleurs"
  type="tutorial"
%}
