# 🛰️ Téléchargeur Intelligent d'Orbites Précises SP3

Ce projet fournit un outil en ligne de commande (CLI) pour télécharger de manière intelligente les produits d'orbites précises GNSS (GPS/GLONASS et multi-constellations) depuis les serveurs CDDIS (Crustal Dynamics Data Information System) de la NASA.

L'outil sélectionne automatiquement le meilleur produit disponible (Final, Rapide ou Ultra-rapide) en fonction de la date demandée, assurant ainsi un compromis optimal entre précision et disponibilité.

---

## 📖 Contexte Technique

[cite_start]Ce téléchargeur s'appuie sur les produits d'orbites précises fournis par l'IGS (International GNSS Service) et distribués par la NASA[cite: 4, 10]. Ces produits sont essentiels pour les applications de géodésie, de photogrammétrie et de positionnement de haute précision.

Les informations ci-dessous sont extraites du document technique `Produits d'Orbites Précises NASA Earthdata` inclus dans ce dépôt.

### Types de Produits et Caractéristiques

| Type de Produit | Nom IGS | Latence (Délai de disponibilité) | Précision de l'orbite | Description |
| :--- | :--- | :--- | :--- | :--- |
| **Final** | `IGS` | [cite_start]12-19 jours [cite: 13] | [cite_start]**~2-3 cm** [cite: 3] | [cite_start]La solution la plus précise, utilisée comme référence pour le post-traitement[cite: 14]. |
| **Rapide** | `IGR` | [cite_start]~17-24 heures [cite: 11] | [cite_start]**~2.5 cm** [cite: 12] | [cite_start]Solution rapide de haute qualité, idéale pour les traitements quasi-quotidiens[cite: 11]. |
| **Ultra-rapide**| `IGU` | [cite_start]3-9 heures (temps réel pour la prédiction) [cite: 7, 82] | [cite_start]**~3-5 cm** [cite: 9] | [cite_start]Solution quasi-réelle, mise à jour 4 fois par jour, pour les applications sensibles au temps[cite: 8]. |

### Avantages des Solutions Combinées (GPS+GLONASS)

L'utilisation de produits combinant plusieurs constellations GNSS offre des avantages significatifs :
* [cite_start]**Précision améliorée** : Gain de performance de 20% à 40% par rapport à une solution GPS seule[cite: 16, 59].
* [cite_start]**Meilleure disponibilité** : En moyenne 14 à 19 satellites visibles simultanément, contre 8-9 pour un système unique[cite: 17, 63].
* [cite_start]**Robustesse accrue** : Particulièrement efficace dans les environnements difficiles comme les canyons urbains ou les hautes latitudes[cite: 18, 67].

---

## ✨ Fonctionnalités

* **Sélection automatique du produit** : choisit intelligemment entre `Final`, `Rapid` et `Ultra-rapid` en fonction de la disponibilité temporelle.
* **Logique de secours (Fallback)** : Si un produit n'est pas trouvé, le script tente automatiquement de télécharger le produit de priorité inférieure.
* [cite_start]**Gestion des conventions de nommage** : Prend en charge les formats de fichiers hérités (avant nov. 2022) et les nouveaux formats IGS20[cite: 29, 31].
* [cite_start]**Authentification moderne** : Utilise un token JWT pour s'authentifier auprès des serveurs HTTPS de NASA Earthdata[cite: 40, 41].
* **Décompression automatique** : Décompresse les fichiers `.sp3.gz` et `.sp3.Z` après le téléchargement.
* **Analyse post-téléchargement** : Vérifie le fichier SP3 téléchargé pour lister les constellations et le nombre de satellites.
* **Configuration facile** : Gère les paramètres (token, répertoire de sortie) via un fichier `sp3_config.json`.
* **Exécutable disponible** : Fourni sous forme d'exécutable pour Windows, ne nécessitant pas d'installation de Python.

---

## 🚀 Installation et Utilisation

Vous avez deux options pour utiliser cet outil.

### Option 1 : Utiliser l'exécutable (Recommandé pour les non-développeurs)

1.  Téléchargez la dernière version de l'exécutable depuis la section "Releases" de ce dépôt GitHub.
2.  Lancez l'exécutable. Un fichier `sp3_config.json` sera créé dans le même dossier.
3.  **Obtenez votre token JWT** :
    * Connectez-vous à [NASA Earthdata Login](https://urs.earthdata.nasa.gov/).
    * Accédez à votre profil et générez un token.
4.  Ouvrez le fichier `sp3_config.json` et collez votre token dans le champ `"jwt_token"`.
5.  Relancez l'exécutable et suivez les instructions du menu.

### Option 2 : Exécuter le script Python

1.  **Prérequis** :
    * **Python 3.x**
    * La bibliothèque `requests`. Installez-la avec pip :
        ```bash
        pip install requests
        ```
2.  **Clonez le dépôt** :
    ```bash
    git clone [https://github.com/VOTRE_NOM_UTILISATEUR/sp3-precise-orbit-downloader.git](https://github.com/VOTRE_NOM_UTILISATEUR/sp3-precise-orbit-downloader.git)
    cd sp3-precise-orbit-downloader
    ```
3.  **Configuration** :
    * Lancez le script une première fois : `python sp3exe.py`.
    * Un fichier `sp3_config.json` sera créé.
    * Suivez les instructions de l'étape 3 de l'Option 1 pour obtenir et configurer votre token JWT.
4.  **Lancez l'application** :
    ```bash
    python sp3exe.py
    ```

---

## 🗂️ Fichiers du Dépôt

* `sp3exe.py` : Le script principal du téléchargeur.
* `README.md` : Ce fichier d'information.
* `Produits d'Orbites Précises NASA Earthdata _ Guide Technique Complet.pdf` : Le document technique de référence sur lequel ce projet est basé.

---

## 📝 Licence

Ce projet est distribué sous la licence MIT.