## TCH098 Projet multidisciplinaire

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

Le circuit est muni d’une résistance de tirage, ou [*pull-up resistance*](https://fr.wikipedia.org/wiki/R%C3%A9sistance_de_rappel) en anglais.

### Programmation

Un programmeur USB AVR Pololu est utilisé pour charger et programmer le micro-contrôleur par le moyen du connecteur ISP.

### Sorties DEL

Le point doit être branché à la masse pour la barre de résistance. Il faut aussi respecter l’orientation des DEL.

### Sortie d'écran LCD

Le potentiomètre permet d’ajuster le contraste de l’écran de sortie LCD. Le rétro-éclairage de 3.3V correspond aux broches $15$ et $16$.

Les données sont reliées aux broches $PC0$ à $PC7$. 

Le contrôle est relié aux broches $PA5$ à $PA7$.

### Entrée _joystick_

L’entrée Joystick sera sujet à la programmation au prochain cours. Néanmoins, celui-ci permettait de vérifier le branchement des lumières DEL lors de la phase finale de vérification. Dans notre cas, les deux plaquettes de prototypage étaient fonctionnelles et la note de $100%$ nous a été attribuée.

## Laboratoire 1A - Montage de la plaquette de prototypage

### Synthèse du laboratoire

## Cours 1B - Introduction à la programmation de microcontrôleur

### Sections du microcontrôleur

### Types de variables 

### Format et opérateurs binaires

```C
uint8_t A = 0b01110010;
uint8_t B = 0b10110111;
uint8_t X = A | B; // X = 0b11110111
uint8_t X = A & B; // X = 0b00110010
uint8_t X = A ^ B; // X = 0b11000101
uint8_t ~A = 0b10001101;
uint8_t A = A << 3; // A = 0b10010000
uint8_t A = A >> 4; // A = 0b00000011
```

### Registres de configuration et contrôle

### Bibliothèques de fonctions et définitions utiles

## Laboratoire 1B - Introduction à la programmation de microcontrôleur

### Procédure de connexion

### Exemples de codes

## Cours 2A - Lecture de potentiomètre par conversion analogique à numérique (CAN) et contrôle de moteur par modulation de largeur d’impulsion (MLI)

### Fonctions avancées du microcontrôleur

### Fonction de conversion du microcontrôleur

Dans le cas du ATmega324A, le port A détient 8 broches responsables de la conversion. Dans le cadre du projet, les ports PA0 et PA1 se chargent de convertir les valeurs analogiques du courant entre $0$ à $3.3 V$ en valeurs numériques dans les directions $x$ et $y$. La tension est régulée par un potentiomètre.

### Configuration de la conversion analogique à numérique

On configure les broches PA0 et PA1 en entrée au moyen de `DDRA = clear_bits (DDRA, 0b00000011)`;

On sélectionne la référence de tension au moyen des fonctions `ADMUX = clear_bit (ADMUX, REFS1);` et `ADMUX = set_bit(ADMUX, REFS0);` . Ceci découle des spécifications du projet. 

Choisir le format du résultat de conversion spécifié ay moyen de fonction `ADMUX = set_bit (ADMUX, ADLAR);`

Choisir le facteur de division de l’horloge de 128 en activant les bits `ADPS0`, `ADPS1` et `ADPS2` du registre `ADCSRA` au moyen de la fonction `ADCSRA = set_bits(ADCSRA, 0b00000111);` ou activer chaque bit individuellement.

Activer la conversion analogique à numérique en activant le bit `ADEN` du registre `ADCSRA` au moyen de la fonction `ADCSRA = set_bit (ADCSRA, ADEN);`

Choisir l’entrée à convertir, prendre sa valeur binaire et et activer les bits correspondant. Pour la broche PA6, sa valeur binaire est égale à $00110$. Dans le registre `ADMUX`, il faut donc activer les bits `MUX0` à `MUX4` correspondant à la valeur binaire.

Attendre la fin de la conversion en effectuant un `while(read_bit(ADCSRA,ADSC) == 1)` .

Faire une lecture du résultat de la conversion et donc `return ADCH`;

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

Le pont en H est un composant essentiel du circuit. Il permet entre autres d’inverser le sens de rotation du moteur dépendamment du circuit interne qui est activé.

### Communication sans-fil ESP8266

Le module de communication sans fil permet aux deux plaquettes de communiquer sans qu’elles soient connectées entre elles.

### Dessin de circuit imprimé

### Brasage électronique

Le but est d’unir deux pièces de métal à l’aide d’une résine (flux) empêchant l’oxydation.

### Entretien de la pointe

### Transfert thermique

### Placement des composants

Voir schéma

### Ordre de soudure

Plus petit au plus grand 

### Résultat de la soudure

## Licence

Ce projet est sous licence conformément à la [licence MIT](LICENSE).
