[https://arpfic.github.io](https://arpfic.github.io)

## Comment utiliser le site

Il s'agit d'un moteur de site de type *static* nommé [Jekyll](https://jekyllrb.com), qui sépare la forme du contenu en compilant des fichiers textes.

Le contenu s'écrit entièrement en *markdown* dans des fichiers `.md` soit avec n'importe quel éditeur de texte, soit directement dans l'interface de github en cliquant sur l'icône d'édition par exemple pour [](https://github.com/arpfic/arpfic.github.io/blob/master/README.md).

D'une manière générale, il est possible à partir de Github de créer des fichiers et des dossiers, de les renommer, de les éditer etc.

Une feuille de triche pour la syntaxe du *markdown* est téléchargeable et imprimable ici : [https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf) ou ici [https://guides.github.com/features/mastering-markdown/](https://guides.github.com/features/mastering-markdown/), ou bien enfin en français et moins clair : [https://github.com/luong-komorebi/Markdown-Tutorial/blob/master/README_fr.md](https://github.com/luong-komorebi/Markdown-Tutorial/blob/master/README_fr.md)

### Structure des dossiers

* Le dossier `img/` stocke des images, réutilisables sur d'autres sites. Pour récupérer leur lien, il suffit de cliquer sur l'image puis sur *Download* : on accède alors à une URL de type `https://raw.githubusercontent.com/arpfic/arpfic.github.io/master/img/XX.jpg`.
* Le dossier `_post/` contient des billets rangés par ordre alphabétique (les classer par date permet un rangement de type blog).
* Le dossier `drafts/` permet d'écrire des pages non visibles (ou non indexées) sur le reste du site. Un README dans le dossier explique comment les écrire.
* Le dossier `/` racine contient les pages générales du site : celles qui nous intéressent sont les fichiers *markdown* en `.md`, qui seront affectées à la barre de navigation (tel l'accueil).
* Les autres dossiers ainsi que les autres fichiers permettent la personnalisation de la forme du site : méta-pages, fichiers de style css etc. Il ne faut pas hésiter à les modifier elles aussi !

Par ailleurs, le fichier `_config.yml` contient les divers éléments configurables pour le site.

**NB :** d'une manière générale, un fichier ou un dossier commençant par `_` est par convention un fichier qui sera compilé par Jekyll.

### Structure d'une page

Pour être compilé par Jekyll, une page doit :

* être écrite en *markdown* et au mieux avoir l'extension `.md`,
* avoir une structure d'entête un peu particulière, telle que :

```
---
layout: page
title: À propos
---

L'Orguanous est le prototype [...]
```

Où, entre chaque `---` on a :

* `layout` est le type du contenu, qu'on peut à souhait ramifier mais pour le moment, un type `page` correspond à un contenu sur le site entier, avec un lien dans la barre de navigation ; le type `post` correspond à un billet de blog accessible sur la page d'accueil ; et enfin le type `priv-page` est une simple page dont on a retiré l'indexation dans la barre de navigation.
* `title` est le titre de la page telle qu'elle sera affichée dans la barre de navigation ou dans les billets.

### Workflow

Il est possible bien sûr d'utiliser l'outil `git` de gestion de versions décentralisé pour enrichir le site de manière traditionnelle. Bien qu'il soit puissant et très efficace, il demande néanmoins d'apprendre un petit peu à l'utiliser.
