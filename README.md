# 🐮 Deadcow — Mobile Pentest & Hardware Tool

<p align="center">
  <img src="docs/assets/deadcow-icon.png" alt="Deadcow Mascot" width="160" height="160" style="border-radius: 24px;">
</p>

<p align="center">
  <b>La boîte à outils Android d'expérimentation radio, sans-fil et pentest matériel.</b><br>
  <i>Un projet dédié à la communauté du <b>Cult of the Dead Cow (cDc)</b> et au collectif <b>Deadcow</b>.</i>
</p>

<p align="center">
  <a href="https://github.com/deadcow-ghw/Deadcow-App/releases"><img src="https://img.shields.io/badge/Version-v1.30--b60-orange.svg" alt="Version"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-GPLv3-blue.svg" alt="License"></a>
  <a href="https://deadcow-ghw.github.io/Deadcow-App/"><img src="https://img.shields.io/badge/Docs-GitHub%20Pages-green.svg" alt="Docs"></a>
  <a href="#"><img src="https://img.shields.io/badge/Langues-Français%20%7C%20English%20%7C%20Русский-purple.svg" alt="Languages"></a>
</p>

---

## 🏴‍☠️ À propos du Projet

**Deadcow** est une suite logicielle Android puissante, autonome et modulaire conçue pour les passionnés d'audit de sécurité, de radiofréquences et de bidouillage matériel. Inspirée de l'esprit du **Flipper Zero** et développée pour fonctionner sans nécessiter de droits root, elle transforme un smartphone standard en véritable couteau suisse d'interception et d'émission de protocoles.

Ce fork est dédié :
* **À l'esprit et à l'héritage de la cDc (Cult of the Dead Cow)** : pionniers du hacktivisme, de la recherche en vulnérabilités et de la libération technologique.
* **Au groupe Deadcow** : pour leurs expérimentations, leurs outils et leurs besoins d'audit de proximité sur le terrain.

---

## 🚀 Arsenal & Fonctionnalités

### 📡 Infrarouge (IR)
* **Base de données de télécommandes universelles** : Contrôle immédiat de téléviseurs, systèmes de climatisation, amplificateurs audio et projecteurs (intégrée depuis les dépôts Flipper-IRDB et firmware Flipper Zero).
* **IR-Storm** : Rafale automatisée de signaux de mise hors tension pour tests massifs d'environnements.
* **Brouilleur IR (IR Jammer)** : Saturation optique empêchant la réception de commandes par les équipements récepteurs.

### 📶 Bluetooth & Bluetooth Low Energy (BLE)
* **Scanner NRF Avancé** : Détection exhaustive des balises BLE, analyse de payloads publicitaires, identification constructeur (OUI) et surveillance spectrale.
* **Spam & Émulation d'appairage** : Tests de robustesse via l'émission de trames FastPair (Android), SwiftPair (Windows) et Continuity / Setup (iOS/macOS).
* **Clavier & Souris sans fil (HID)** : Émulation d'un périphérique d'entrée humain Bluetooth pour piloter un ordinateur ou exécuter des scripts BadUSB/HID à distance.
* **Deadcow Chat** : Messagerie locale directe hors-réseau (mesh P2P) fonctionnant à 100% via le protocole BLE entre utilisateurs de Deadcow.

### 💳 NFC & RFID
* **Lecture & Émulation de cartes/tags** : Lecture bas niveau, clonage et rejeu d'identifiants NFC compatibles.
* **Analyse de protocoles** : Détection des puces MIFARE, NTAG, FeliCa et ISO-DEP.

### 🌐 Réseau Local & Wi-Fi
* **Scanner LAN Ultra-rapide** : Cartographie des hôtes actifs, détection des services ouverts, identification des adresses MAC et fabricants sur le sous-réseau.
* **Serveur Audio Local & Générateur QR Code** : Partage de flux audio locaux, synthèse vocale (TTS) et génération instantanée de QR codes réseau ou payloads.

### 🐍 Plugins Python & Mascotte Deadcow
* **Moteur de Plugins Chaquopy (Python)** : Ajoutez facilement vos propres scripts et écrans via des modules Python `.dolphyplugin`.
* **Système de Mascotte Deadcow** : Animations 128x64 pixels, gain d'expérience (XP) au fil de vos scans et audits, niveaux débloquables et portraits passeport.

---

## 🛠️ Compilation & Utilisation (Linux & Android)

### 🐧 1. Compiler l'APK sur Linux

Pour compiler l'APK Deadcow directement sur votre machine Linux :

#### Prérequis
* **JDK 17** :
  ```bash
  # Arch / Manjaro / Omarchy :
  sudo pacman -S jdk17-openjdk
  # Debian / Ubuntu :
  sudo apt install openjdk-17-jdk
  ```
* **Python 3.11 ou 3.12** (requis par le moteur Chaquopy pour compiler les plugins Python) :
  ```bash
  python3 --version
  ```
* **Android SDK** (ou Android Studio) avec `platforms;android-36` et `build-tools;36.0.0`.
  Définissez votre variable d'environnement :
  ```bash
  export ANDROID_HOME="$HOME/Android/Sdk"
  ```

#### Commandes de compilation
1. Rendez le wrapper Gradle exécutable :
   ```bash
   chmod +x gradlew
   ```
2. Lancez la compilation :
   * **Pour un APK Debug (développement rapide)** :
     ```bash
     ./gradlew assembleDebug
     ```
     L'APK généré sera situé dans :  
     `app/build/outputs/apk/debug/app-debug.apk`
   * **Pour un APK Release optimisé** :
     ```bash
     ./gradlew assembleRelease
     ```
     L'APK généré sera situé dans :  
     `app/build/outputs/apk/release/app-release.apk`

---

### 🖥️ 2. Exécuter l'application sur Linux

Vous pouvez utiliser l'application Deadcow directement sur votre environnement Linux sans avoir besoin d'un téléphone :

#### Option A : Avec Waydroid (Le plus performant sous Wayland)
1. Installez et initialisez **Waydroid** sur votre distribution Linux.
2. Installez l'APK Deadcow d'une seule commande :
   ```bash
   waydroid app install app/build/outputs/apk/release/app-release.apk
   ```
3. Lancez l'application depuis votre lanceur d'applications de bureau ou via :
   ```bash
   waydroid app launch com.droid.dolphy
   ```

#### Option B : Avec Scrcpy (Smartphone Android branché en USB)
Si vous compilez sur Linux et souhaitez tester instantanément sur votre téléphone physique :
1. Activez le **Débogage USB** dans les options développeur de votre téléphone.
2. Branchez le smartphone en USB à votre PC Linux.
3. Installez l'APK généré :
   ```bash
   adb install -r app/build/outputs/apk/release/app-release.apk
   ```
4. Affichez et contrôlez l'écran de votre téléphone en direct sur votre bureau Linux :
   ```bash
   scrcpy
   ```

---

### ☁️ 3. Compilation Cloud automatique (GitHub Actions)

Si vous ne souhaitez pas installer les outils Android SDK sur votre machine :
1. Rendez-vous dans l'onglet **Actions** de votre dépôt GitHub.
2. Sélectionnez le workflow **Build Deadcow APK**.
3. Cliquez sur **Run workflow**, choisissez la branche `main` et le type (`release` ou `debug`).
4. GitHub compile le projet dans le cloud en quelques minutes et met à disposition l'APK en artefact et dans la section **Releases**.

---

## 🔄 Mises à jour automatiques & GitHub Pages

* **Mises à jour in-app autonomes** :  
  L'application Deadcow intègre son propre module d'auto-mise à jour (`AutoUpdater`). À chaque lancement, elle consulte le dépôt GitHub et le fichier `version.json` publié sur GitHub Pages. Lorsqu'une nouvelle version est disponible, elle propose le téléchargement et l'installation directe en 1 clic.
* **Documentation & Site GitHub Pages** :  
  Le site web et la documentation interactive des plugins sont disponibles à l'adresse :  
  👉 **[https://deadcow-ghw.github.io/Deadcow-App/](https://deadcow-ghw.github.io/Deadcow-App/)**  
  Toute modification poussée dans le dossier `docs/` est automatiquement synchronisée avec la branche `gh-pages`.

---

## 📥 Téléchargement direct

Téléchargez la dernière version stable prête à installer :  
👉 **[Dernière Release Deadcow](../../releases/latest)**

---

## 📜 Licence & Mentions Légales

* Distribué sous licence **GNU General Public License v3.0 (GPLv3)**.
* Développé à des fins éducatives, de recherche et d'audit défensif d'équipements autorisés.
* Remerciements et crédits aux développeurs du projet Flipper Zero et du projet source Dolphy.
