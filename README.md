# Configuration Home Assistant pour la Gestion d'Énergie Domestique

Ce dépôt contient mes fichiers de configuration pour divers projets Home Assistant, axés sur la gestion intelligente de l'énergie à domicile. Les configurations sont organisées en deux dossiers principaux : `ESP` et `automatisation`.

## Dossier ESP

Dans le dossier `ESP`, vous trouverez les configurations nécessaires à deux projets distincts :

1. **Projet Linky en triphasé avec production solaire** : Configuration pour récupérer des informations depuis un compteur Linky via un ESP, spécifiquement adaptée pour un système en triphasé et avec production d'énergie. Ce projet permet une surveillance précise de la consommation et de la production d'énergie.

3. **Projet de détection de présence** : Utilisant un ESP32-S2 Mini et un capteur de présence LD410C, cette configuration s'inspire d'une vidéo des frères Poulain. Elle est améliorée par l'ajout d'un capteur de luminosité pour activer l'éclairage uniquement lorsque c'est nécessaire, optimisant ainsi la consommation d'énergie.

## Dossier Automatisation

Le dossier `automatisation` contient des configurations visant à rendre les appareils domestiques plus intelligents et écoénergétiques :

1. **Automatisation du chauffe-eau** : Cette configuration permet de contrôler un chauffe-eau avec une prise connectée Tuya, activant le chauffage de l'eau en fonction de la production d'énergie solaire. Cela assure que l'eau chaude est produite de manière écoénergétique, en utilisant le maximum d'énergie solaire disponible.

2. **Automatisations intelligentes avec prises connectées** : Diverses automatisations utilisant des prises connectées pour consommer de l'énergie de manière plus intelligente en fonction de la production solaire. Ces configurations permettent d'optimiser l'utilisation des appareils électriques en les activant lorsque la production d'énergie solaire est suffisante.

