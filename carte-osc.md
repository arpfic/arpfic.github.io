---
layout: page
title: Prototype de carte OSC
---

## Présentation

### Design

Après plusieurs tentatives de design, celui qui semblait à la fois concrétiser dans la même logique les éléments et l'ensemble des besoins d'un tel instrument ; et à la fois répondre à un  processus d'adaptation le plus ouvert possible à ses excentricités ; celui-ci peut se schématiser simplement tel que :

![](https://raw.githubusercontent.com/arpfic/Organous_OSC/master/Hardware/carte_osc_schema_fonc.png)

* Nous souhaitons pouvoir communiquer en **OSC** (*Open Sound Control*) simplement parce que sa rapidité dépend du matériel de transport et non d'une horloge fixée par le protocole tel que le MIDI (31250baud). L'orgue sera donc connecté en **ETHERNET** à un routeur central et à toutes les interfaces supportant le protocole ou bien permettant une traduction de et vers le **MIDI**.
* Le processeur central choisi est un **Nucleo-F767ZI**, assez puissant pour couvrir toutes les fonctions logicielles qui nous passerons par la tête. Il faut bien sûr le brancher en **ETHERNET** au routeur central.
* Le processeur **F767ZI** est relié à une carte fille qui contient, outre les composants nécessaires à l'alimentation, deux ensembles d'éléments.
  * Un *contrôleur de LED*, un **PCA9956B** commandé par le processeur central en *I2C Fast Mode*, capable de générer 24 signaux PWM à une fréquence ultra-son de 31.25Khz. Il s'agit en quelque sorte d'un détournement de son usage, habituellement réservé à l'affichage (Google ayant fabriqué du matériel bling-bling avec celui-ci), vers nos besoins.
  * Enfin, des drivers montés en *ponts-H* -- les **DRV8844**, sont placés en sortie du contrôleur de LED, par l'intermédiaire des LED elles-mêmes assurant la conversion *pull-down*. Ces drivers apportent beaucoup d'avantages : une grande souplesse de configurations **PULL**, **PUSH** et **PUSH-PULL**, des sorties dispensables, la possibilité d'utiliser une tension symétrique et des mesures et protections internes qu'il est possible de monitorer en retour avec le **F767ZI**.

Du point de vue de la carte, ces éléments se retrouvent tels que :

![](https://raw.githubusercontent.com/arpfic/Organous_OSC/master/Hardware/carte_osc_fonctions_avancees.png)

### Branchements

##### À partir de la carte fille

Les branchements avec le reste de l'orgue sont assez simples :

![](https://raw.githubusercontent.com/arpfic/Organous_OSC/master/Hardware/carte_osc_fonctions.png)

L'alimentation générale doit être considérée avec importance, *d'autant plus que la souplesse de son design ouvert ne nous permet pas de restreindre son usage par des précautions*. Ainsi, de gauche à droite sur le schéma,

* on peut brancher sur le bornier associé une **tension négative**
* son point-milieu **la masse**, servant surtout à l'alimentation du traitement de données, et
* une **tension positive**.

Par exemple nous pouvons alimenter la carte avec du **-15V/GND/+15V** pour driver des bobines sur une amplitude de **30V** qui selon la manière dont on les branche se réalise soit *absolument* sur 30V, soit *relativement* au point milieu la masse, avec inversion de tension.

Par un autre exemple, nous pouvons alimenter la carte en branchant tel que **GND/GND/15V** afin de driver simplement des bobines en **PULL**, la masse ici fusionnant avec le point négatif.

**NB** : bien sûr, il est impossible de fusionner la masse avec la tension positive.

Les limites absolues du driver sont de :

* soit au minimum de **GND/GND/+8V**, et au maximum
* soit de **-24V/GND/+24V**,
* soit de **GND/GND/+36V**,
* avec un courant de **1.75A RMS** par sortie.

##### Pour la carte-mère

La carte-mère pour sa part, la **Nucleo-767ZI** se branche d'un côté ou de l'autre selon les sorties que l'on souhaite voir utilisées par l'intermédiaire des grands ports **CN1 1** et **CN1 2** de part et d'autre :

![](https://raw.githubusercontent.com/arpfic/Organous_OSC/master/Hardware/Nucleo_144.jpg)

Afin d'être alimentée par l'alimentation de la carte-fille au travers du convertisseur 5V, il est nécessaire si cela n'a pas été déjà fait de placer le jumper **JP3** sur la configuration **E5V**, tout à gauche.

En dehors de la programmation, le seul branchement ici nécessaire à l'usage est un câble ethernet vers un routeur.

Voici en résumé le branchement dans sa version la plus simple :

![](https://raw.githubusercontent.com/arpfic/Organous_OSC/master/Hardware/Organous_OSC_v0.2_exemple.jpg)

### Programmation

La carte se programme par **copier-coller** de son firmware dans sa mémoire comme on copie un fichier sur une clé USB par l'intermédiaire du port USB **CN1** **du haut sur les photos**, situé sur la petite extension de la carte nommée *st-link*.

Le firmware lui-même est téléchargeable [ici](https://raw.githubusercontent.com/arpfic/Organous_OSC/master/Firmware/Organous_OSC_stable.bin).

Attention cependant : la communication entre les cartes-filles et les cartes-mères imposent une *adresse I2C*. Le firmware stable du dessus prend comme adresses I2C les petites soudures sur les cartes de sorte que :

* sur le **SOCKET A 1-24**, l'adresse est **Vdd-GND-Vdd** (*0x2A* dans le programme)
* sur le **SOCKET B 25-48**, l'adresse est **GND-Vdd-GND** (*0xD2* dans le programme).

### Interface avec Puredata

Il faut d'abord s'être assuré d'avoir connecté un ordinateur au même réseau que la carte OSC, c'est-à-dire *au même routeur* ou bien sur un switch qui mène à ce routeur.

... Et d'avoir alimenté l'ensemble avec au minimum une alimentation supérieure à 8V en configuration **GND/GND/8V**.

Le patch puredata encore en phase de test est téléchargeable [ici](https://raw.githubusercontent.com/arpfic/Organous_OSC/master/Puredata/pd_osc_F767ZI_stable.pd).

Si le réseau et la carte fonctionnent correctement :

* la carte doit afficher **deux** LED vertes et non une.
* l'écran de puredata devrait afficher le message que la carte lui envoie en **2** :

![](https://raw.githubusercontent.com/arpfic/arpfic.github.io/master/img/puredata.png)

Si au contraire le message n'est pas apparu et que le réseau a été mis en place après le lancement de puredata ou si la carte a été lancée avant lui, il suffit :

* dans le premier cas, d'appuyer sur le bouton **1** de puredata,
* dans le second cas, d'appuyer sur le bouton **bleu** de la carte OSC pour relancer le message, ou sur son bouton **noir** (*RESET*).

Une fois ceci terminé, il est nécessaire (une fois pour toutes) d'adapter l'adresse IP du module dans la boîte de message **3** sur puredata et de cliquer sur le *bang* en bas à droite qui lance `/tools/connect`.

L'ensemble des *fonctions OSC* est disponible sur [https://github.com/arpfic/Organous_OSC/blob/master/USAGE.md](https://github.com/arpfic/Organous_OSC/blob/master/USAGE.md)
