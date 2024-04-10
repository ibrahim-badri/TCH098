# TCH098 Projet multidisciplinaire
Réaliser un projet en équipe multidisciplinaire (au moins deux disciplines représentées par équipe selon le programme spécialisé d’appartenance) mettant en application les connaissances et compétences apprises au fur et à mesure de l’avancement du deuxième volet d’un cheminement universitaire en technologie.

## Table des matières

## Tech Stack
Les principales technologies utilisées dans le cadre de ce cours sont principalement le langage C.

## Cours 1A - Montage de la plaquette de prototypage
### Plaquette de prototypage de la manette (_joystick_)

### Alimentation

Une batterie de $9V$ ou $7.4V$ si elle est en Lithium sont utilisés pour alimenter le circuit.

Des régulateurs de charge sont placés dans le circuit pour contrôler les tensions entrantes et sortantes. *



### Microcontrôleur _ATmega324A_
#### Caractéristiques
Demi-cercle indique le haut de la puce. Il dispose de 40 broches ou pin situées de part et d’autres du microcontrôleur. Le microcontrôleur est symétrique.
Le microcontrôleur est muni d’un oscillateur interne qui fonctionne à une fréquence de 8 MHz. Par conséquent, il effectue 8 millions d’opérations par seconde.
#### Connexion minimum
Les broches de *l’alimentation* et du *reset* sont essentielles.

Le circuit est muni d’une résistance de tirage, ou *[pull-up* *resistance*](https://fr.wikipedia.org/wiki/R%C3%A9sistance_de_rappel) en anglais.

### Programmation

Un programmeur USB AVR Pololu est utilisé pour charger et programmer le micro-contrôleur par le moyen du connecteur ISP.

### Sorties DEL

### Sortie d'écran LCD

### Entrée _joystick_

## Laboratoire 1A - Montage de la plaquette de prototypage
### Synthèse du laboratoire

## Cours 1B - Introduction à la programmation de microcontrôleur

### Sections du microcontrôleur


### Types de variables 

### Format et opérateurs binaires

### Registres de configuration et contrôle

### Bibliothèques de fonctions et définitions utiles

## Laboratoire 1B - Introduction à la programmation de microcontrôleur

### Procédure de connexion

### Exemples de codes

## Cours 2A - Lecture de potentiomètre par conversion analogique à numérique (CAN) et contrôle de moteur par modulation de largeur d’impulsion (MLI)

### Fonctions avancées du microcontrôleur

### Fonction de conversion du microcontrôleur

### Configuration de la conversion analogique à numérique

### Solution d'ajustement d'intensité

### Modulation de largeur d’impulsion

### Configuration de la modulation de largeur d’impulsion

## Laboratoire 2A - Lecture de potentiomètre (CAN) , contrôle d’intensité lumineuse (MLI), contrôle de la vitesse d’un moteur et contrôle de servomoteur (MLI)

## Cours 2B - Protocoles de communication série asynchrone RS232

### Broches de communication

### Transmission série asynchrone

### Norme RS232

### _Universal Asynchronous Receiver Transceiver_ (USART)

### Modules de programmation

### Interruptions

### En résumé…

## Laboratoire 2B - Protocole de communication série asynchrone RS232

## Cours 3A et 3B - Conception d’un circuit et brasage à l’étain

### Pont en H DRV8801

### Communication sans-fil ESP8266

### Dessin de circuit imprimé

### Brasage électronique

### Entretien de la pointe

### Transfert thermique

### Placement des composants

### Ordre de soudure

### Résultat de la soudure

## Licence
Ce projet est sous licence conformément à la [licence MIT](LICENSE).
