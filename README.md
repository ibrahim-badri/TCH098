## TCH098 Projet multi disciplinaire

<!-- TODO: add project description -->
<!-- TODO: add table of content -->

## Cours 1A - Montage de la plaquette de prototypage

### Plaquette de prototypage de la manette (_joystick_)

<!-- TODO: add joystick circuit -->

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

La **partie rouge** correspond aux entrées et sorties.

La **partie verte** correspond à microprocesseur/CPU.

La **partie bleue** correspond à la mémoire.

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

`DDRx` : direction du port avec $0$ en entrée et $1$ en sortie.

`PORTx` : forcer un $1$ ou un $0$ sur une broche.

`PINx` : valeurs d’entrée et connaître l’état des entrées.

### Bibliothèques de fonctions et définitions utiles

## Laboratoire 1B - Introduction à la programmation de microcontrôleur

### Procédure de connexion

### Exemples de codes

```C
/*
+===============================================+
|   LIBRAIRES ET COMMANDES AUX PRÉPROCESSEURS   |
+===============================================+
Au début de chaque programme, il est important d'importer et d'inclure
les libraires nécessaires à l'utilisation des différentes méthodes
ou fonctions. Se référer à la documentation pour connaître
les fonctionnalités de chacune.
*/

#include <avr/io.h>
#include <util/delay.h>
#include "lcd.h"
#include "utils.h"
#include <stdio.h>

/*
+====================+
|   PROGRAMME MAIN   |
+====================+
Le code doit être rédigé dans cette section pour pouvoir être compilé.
*/

int main(void)
{

/*
+==============================+
|   DÉFINITION DES VARIABLES   |
+==============================+
 Le bouton de Joystick possèdes 2 états : appuyé et non-appuyé.
 Lorsqu'il est appuyé, on connecte la broche dy microcontrôleur
à la masse, générant un 0. Ici, on le définit comme étant 1.

On déclare aussi une chaîne de caractère qui composera le message
affiché par le LCD.

*/
	uint8_t b = 1;	
	char str[40];	
		

/*
+===========================+
|   CONFIGURATION DES DEL   |
+===========================+
Les témoins lumineux de la DEL sont connectées aux broches PB0 à PB4.
Néanmoins, puisque les DEL n'envoient aucune information aux microcontrôleurs,
les broches PB0 à PB4 doivent être définies comme des sorties. Pour se faire,
on utilise la fonction DDRx = set_bits pour mettre les bits correspondants à 
1.
*/

	DDRB=set_bits(DDRB,0b00011111);

/*
+===============================+
|   CONFIGURATION DU JOYSTICK   |
+===============================+
Le joystick est connecté au microcontrôleur à travers la broche PA2. 
Contraitement aux DEL, celui-ci envoi de l'information pertinente au 
microcontrôleur et par conséquent, doit être défini comme une entrée par le biais
de la fonction DDRx = clear_bit. Ici, il s'agit d'un bit individuel, il est donc
primordial d'enlever le 's'. La fonction PORTx = set_bit, quant à elle, force 
un état sur une broche, ou en d'autres termes, permet d'activer la pull-up 
resistance de la broche pour forcer un état (0 ou 1).
*/
	
	DDRA = clear_bit(DDRA,PA2);
	PORTA = set_bit(PORTA,PA2);

/*
+===============================+
|   INITIALISATION DE L'ÉCRAN   |
+===============================+
L'affichage LCD est un composant pertinent permetttant d'afficher et de relayer des informatiques critiques
telles que la position du joystick, la puissance d'un moteur, des états ou bien même, des poèmes romantiques
si vous êtes un SIMP. Tout d'abord il est important d'initaliser le LCD et d'en effacer le contenu.
*/

	lcd_init();
	lcd_clear_display();

/*
+============================+
|   BOUCLE INFINI WHILE(1)   |
+============================+
Cette boucle permet une éxécution continu du programme dans le microcontrôleur et ce, jusqu'à celui-ci soit mis
hors tension.
*/

    while (1) 
    {

/*
+==========================+
|   LECTURE D'UNE BROCHE   |
+==========================+
Comme il a été mentionné précédemment, le joystick deux états non simultanées.
Ces états peuvent être traduites par une valeur numérique de 0 ou 1. Or, dépendemment
de si le bouton est appuyé ou non, il est possible de récupérer cette valeur à travers la broche
à laquelle il est connecté. Dans ce cas, puisque le joystick est connecté à la broche PA2,
on récupère l'état du bouton par le biais de la fonction read_bit(PINx,XXX). 
*/

		b = read_bit(PINA,PA2);

/*
+================================+
|   MISE HORS TENSION DES DELS   |
+================================+
Pour éteindre les DEL, il suffit de forcer l'état 0 sur les broches 
connectés aux microcontrôleurs. La fonction clear_bits permet de forcer des 0
là ou les valeurs sont à 1.
*/
		
		PORTB = clear_bits(PORTB,0b00011111);

/*
+==============================+
|   STRUCTURE CONDITIONNELLE   |
+==============================+
Cette boucle permet d'effectuer une séquence d'action en conséquence de l'état du bouton.
Si le bouton est enfoncé (0), la DEL connectée à la broche BP4 s'allumera.
Si le bouton est désenfoncé (1), la DEL connectée à la broche BP0 s'allumera.
*/

		if (b == 0){
			PORTB = set_bit(PORTB,PB4);
		}
		else 
			PORTB = set_bit(PORTB,PB0);
		
/*
+========================+
|   CHAÎNE DE CARATÈRE   |
+========================+
L'affichage de caractères ou de chaînes de caractères se fait à travers l'affichage LCD.
Pour afficher un message, il faut d'abord définir la chaîne de caractère, son 
contenu et le type de valeur devant être affiché avec la méthode sprintf(str,contenu et type de valeur, valeur).
Par la suite, cette chaîne de caractère est envoyé vers l'écran LCD avec la fonction lcd_write_string(str),
*/
		sprintf(str,"b vaut %d",b);
		
		lcd_set_cursor_position(0,0);
		lcd_write_string(str);

/*
+=======================+
|   DÉLAI DE SÉCURITÉ   |
+=======================+
Un délai de sécurité est parfois nécessaire si l'information transmise nécessite
d'être rafraîchie selon un certain intervale. Pour ajouter un délai,
on utilise la fonction _delay_ms(temps).
*/
		_delay_ms(10);
		
    }
}
```

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

Le microcontrôleur dispose de plusieurs broches de communication pouvant agir à titre de récepteur (RX) ou transmetteur (TX). Ses broches font partie du port D.

### Transmission série asynchrone

### Norme RS232

### _Universal Asynchronous Receiver Transceiver_ (USART)

### Modules de programmation

Les bibliothèques uart.c, uart.h, fifo.c et fifo.h sont des librairies essentielles.

### Interruptions

### En résumé…

<!-- TODO: add table with resume of libraries -->

## Laboratoire 2B - Protocole de communication série asynchrone RS232

## Cours 3A et 3B - Conception d’un circuit et brasage à l’étain

### Pont en H DRV8801

Le pont en H est un composant essentiel du circuit. Il permet entre autres d’inverser le sens de rotation du moteur dépendamment du circuit interne qui est activé.

### Communication sans-fil ESP8266

Le module de communication sans fil permet aux deux plaquettes de communiquer sans qu’elles soient connectées entre elles.

### Dessin de circuit imprimé

Le but d’un logiciel EDA est de faire une conception en deux temps : schématique qui permet de spécifier les connexions en faisant abstraction de la forme physique et circuit imprimé ou *printed circuit board* (PCB) qui permet de dessiner les connexions sur la plaque en tenant compte des dimensions. 

Le logiciel suivant est utilisé pour la conception des circuits imprimés :

<!-- Placeholder for Altium Designer Software -->

Lors de la conception d’un circuit, une trace est un chemin de conduction sur le circuit imprimé.

Un via est un trou métallisé qui permet d'établir une liaison électrique entre deux couches.

### Brasage électronique

Le but est d’unir deux pièces de métal à l’aide d’une résine (flux) empêchant l’oxydation.

### Entretien de la pointe

### Transfert thermique

<!-- Add schema here -->

### Placement des composants

<!-- Add schema here -->

### Ordre de soudure

Plus petit au plus grand 

### Résultat de la soudure

## Licence

Ce projet est sous licence conformément à la [licence MIT](LICENSE).
