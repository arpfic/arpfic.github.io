[https://arpfic.github.io](https://arpfic.github.io)

## Pages non visibles

Pour écrire des pages non indéxées et donc non visibles depuis le menu, écrire dans le dossier `drafts/` des fichiers `.md` avec l'entête particulière telle que :

```
---
layout: priv-page
title: Cahier de notes
search: exclude
---

Ici [...]
```

Le `priv-page` empêchera la page de s'afficher dans la barre de navigation, et `search: exclude` excluera le référencement par les moteurs de recherche.

### Accès

L'URL permettant l'accès à ces pages sera simplement le non du dossier, ici `drafts/` suivi du nom du fichier servant à l'écrire avec l'extension `.html`, par exemple [https://arpfic.github.io/drafts/notes.html](https://arpfic.github.io/drafts/notes.html).
