# Lecteur Winamp (Standalone)

Une carte multimédia complète et très poussée visuellement pour Home Assistant. Elle s'inspire de l'esthétique du célèbre logiciel Winamp, tout en adoptant un look moderne de type "Glassmorphism" (verre dépoli).

## ✨ Fonctionnalités Détaillées

- **Esthétique Glassmorphism** : Reflets vitrés dynamiques, ombres portées douces, et flou d'arrière-plan interactif.
- **Écran LCD Dynamique** : Affiche le statut du lecteur, un (faux) égaliseur animé, et un chronomètre précis.
- **Défilement intelligent (Marquee)** : 
  - Le texte défile *uniquement* si sa longueur dépasse la largeur de l'écran.
  - La vitesse de base est calculée sur le nombre de caractères pour assurer une lecture confortable.
  - S'il y a deux lignes en mouvement (Artiste et Titre), la plus longue dicte le temps de la boucle (`maxDuration`). La ligne la plus courte ajuste son pourcentage d'animation pour terminer exactement en même temps, évitant ainsi le décalage visuel au fil du temps.
- **Barre de progression "Zéro Latence"** *(Merci à WarC0zes pour cette optimisation technique)* : 
  - Implémentation d'un *Ticker Javascript natif* : un chronomètre indépendant survit aux rafraîchissements de Home Assistant et met à jour le temps et la barre chaque seconde localement.
  - Lors du glissement, la barre de progression réagit instantanément au doigt, et n'envoie l'instruction à Home Assistant qu'au moment du relâchement, éliminant ainsi les "retours en arrière" et les saccades désagréables.
- **Indicateurs techniques (Dashboard)** : Affiche en temps réel le périphérique de sortie audio (`OUT:`), ainsi que les icônes `Shuffle` et `Repeat`.
- **Gestion intelligente des états** *(Merci à WarC0zes)* : 
  - **PLAY** : Animations actives, égaliseur en mouvement.
  - **PAUSE / STOP** : Affichage `[ PAUSE ]` clignotant, arrêt de l'égaliseur et des textes.
  - **OFF** : Extinction tamisée de l'écran LCD et masquage des indicateurs pour simuler un appareil hors tension.
- **Stand-alone (Zéro dépendance complexe)** : Tout le code (CSS complet, variables dynamiques, HTML, et Javascript embarqué) est contenu en un seul bloc dans la carte. La seule dépendance est l'intégration *Custom Button-Card*.

## 📦 Prérequis

- L'intégration [Custom Button-Card](https://github.com/custom-cards/button-card) (à installer via HACS).

## 🚀 Installation

1. Ouvrez le fichier [`winamp_player.yaml`](winamp_player.yaml) de ce dossier.
2. Copiez tout le contenu du fichier.
3. Allez sur votre tableau de bord Home Assistant, passez en mode édition, et ajoutez une carte **Manuelle** (Manual).
4. Collez le code.
5. Remplacez l'entité de démonstration par la vôtre. Cherchez la ligne suivante (vers la fin du fichier) :
   ```yaml
   entity: media_player.votre_lecteur_ici
   ```
   Et remplacez par votre vrai lecteur.

## 🎨 Personnalisation

Toutes les couleurs, la police d'écriture et les effets d'ombre sont centralisés dans la section `styles: > custom_fields:` au début du fichier. 
Cherchez la mention `[ZONE MODIFIABLE]` pour ajuster facilement l'apparence à votre goût (changement de couleur dominante, opacité du verre, etc.).
