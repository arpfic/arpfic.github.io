---
layout: post
title: Cahier des charges pour un travail sans fin
---

À présent équipé d'une électromécanique conçue initialement pour jouer tranquilou avec un orgue de barbarie, l'objet trouve à l'intérieur de son propre fonctionnement des obstacles : par exemple, l'électronique des décodeurs MIDI souffre en effet de la sursollicitation de notes répétées et de groupes de notes importants, recherchées dans les musiques jouées avec l'Organous. En plus de cela, le dispositif actuel ne protège pas les vieilles électrovannes, qui chauffent et par conséquent s'usent vite.

L'Organous est probablement un *prototype en évolution permanente*, se spécialisant à la fois par différentiation en parties et par concrétisation en ensemble, en synergie.

![](https://raw.githubusercontent.com/arpfic/arpfic.github.io/master/img/49.jpg)

## Deux fenêtres de recherches sont ouvertes à présent :

### Les électrovannes

Non seulement très vieilles et d'origine, les électrovannes en tant que transducteur ont été conçues comme *système ouvert-fermé*, permettant d'actionner ou non une flûte en réaction au stimulus du musicien. Un des aspects d'évolution envisagés serait de *moduler la quantité d'air* qui entre dans chaque flûte, afin par conséquent de moduler l'amplitude du son produit. 

Pour cela, nous imaginons fabriquer des électrovannes dont la forme serait adaptée à la modulation désirée, et autant que possible par un fonctionnement proportionnel.

Voici les premières tentatives d'évolution de ces petites objets :

![](https://raw.githubusercontent.com/arpfic/arpfic.github.io/master/img/electrovrac.jpg)

### L'électronique

Du point de vue de la transmission et de l'amplification, l'électronique embarquée dans l'instrument joue également un rôle important qui dans les orgues existant aujourd'hui est plus ou moins déjà sophistiquée.

En dehors des problèmes évoqués ci-dessus qu'une nouvelle génération de cartes permettrait de résoudre nous pourrions -- en imaginant par nous-même une architecture adaptée à l'Organous -- tout simplement augmenter l'espace des jeux et des expérimentations aux frontières des limites mécaniques d'un orgue.

Un ensemble de contraintes pour un cahier des charges a déjà été donné.

#### En voici les aspects techniques essentiels :

* Ergonomie reprise sur les cartes d'[Orgautomatech](https://www.orgautomatech.com) : programmation du canal MIDI, de l'assignation des notes MIDI des sorties.
* 8 cartes de 16 sorties, chaînables (pour chaque module de cromorne, il faut pouvoir en chaîner 2).
* Compatible avec électrovannes actuelles de l'Organous de 15V.
* Système de réduction de tension envoyées aux électrovannes : pour s'ouvrir, celle-ci a besoin de 15V seulement pendant quelques ms le temps que le plongeur ait atteint sa position finale ; ensuite il est possible de baisser (peut-être même jusqu'à 3-6V), pour moins les faire chauffer; on les préserve ainsi au maximum, afin qu'elles arrêtent de perdre des spires, et éviter d'avoir à toutes les changer un jour.
* Une forme de fusible pour chaque électrovanne: si une électrovanne crame, il ne faut pas qu'elle crame aussi la carte, ou ne serait-ce lui laisser le temps de refroidir avant d'être réamorcée.
* Une électronique surdimensionnée, afin de pouvoir jouer sans limitation toutes les électrovannes de l'Organous, pendant de longues durées (plusieurs heures).
* Protection de la carte contre les surtensions.
* Protocole OSC (*Open Sound Control*), afin de ne plus être limité par la quantité de données.
* Un signal PWM des sorties, sur une fréquence inaudible, avec au moins 128 pas, en prévision d'un usage proportionnel.
* Inversion de tension, pour un usage PUSH/PULL sur des électrovannes proportionnelles.

#### Premières tentatives

Plusieurs pistes ont été envisagées, et le travail en cours sera bien plus détaillé dans ce site dont il est l'un des objet.

![](https://raw.githubusercontent.com/arpfic/arpfic.github.io/master/img/sprint_layout.jpg)
