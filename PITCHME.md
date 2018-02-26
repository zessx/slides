---

![Drupal](assets/images/logo-css3.png)

### REM - Finding My Religion

---

## Les différentes unités en CSS

« CSS Values and Units Module Level 3 » *2013*

- Valeurs absolues : `px`, `pt`, `cm`, `mm`, `in`, `pc`
- Valeurs relatives : `%`, `em`, `rem`, `vh`, `vw`, `vmin`, `vmax`, `ex`, `ch`

+++

### L'unité `em`

*1eM correspondait à la taille du « M » majuscule.*

Taille relative à l'élément parent.

```css
html       { font-size: 20px; }
.module    { font-size: 16px; }
.module h3 { font-size: 1.5em; /* = 24px */ }
```

+++

### L'unité `rem`

*Root em*, taille relative à l'élément racine (`<html>`).

```css
html       { font-size: 20px; }
.module    { font-size: 16px; }
.module h3 { font-size: 1.5rem; /* = 30px */ }
```

+++

### Les unités `vh`, `vw`, `vmin` et `vmax`

- `vh` = hauteur de la fenêtre (IE9+)
- `vw` = largeur de la fenêtre (IE9+)
- `vmin` = `min(vh, vw)` (Edge 16+)
- `vmax` = `max(vh, vw)` (IE9+)

+++

### L'unité `ex`

*X-height*, taille relative à la hauteur du « m » minuscule.   
Compatible avec tous les navigateurs.    
Intéressant pour les pictogrammes.

+++

### L'unité `ch`

*Character*, taille relative à la largeur du « 0 ».   
Mal supporté sur Internet Explorer (9~11).    
Intéressant pour les fontes monospace.

---

## Intégration modulaire

*Ne pas confondre avec les CSS Modules, un outils de namespacing principalement utilisé avec ReactJS.*

- Faciliter la réutilisation de blocs
- Avoir un design dynamique
- Préserver l'équilibre en responsive

---

## Le problème du tout-pixel

Reprenons l'exemple précédent, un peu développé :

```scss
html { 
  font-size: 20px; 
}
.module { 
  font-size: 16px; 
  padding: 25px;
  h3 {
    font-size: 24px;
    margin-bottom: 25px;
  } 
}
```

+++

### Absolu = Indépendance

La modification d'un seul élément entraîne une perte d'équilibre sur l'ensemble.   
Il faut donc tout modifier à chaque fois :

```scss
@media screen and(max-width: 320px) {
  .module { 
    font-size: 10px; 
    padding: 15px;
    h3 {
      font-size: 15px;
      margin-bottom: 15px;
    } 
  }
}
```

---

## Du relatif avec `em`

`em` doit ête utilisé pour tout élément dont la taille est étroitement liée à son parent :

- les paddings
- les margins (selon les cas)

+++

### Relatif = Dépendance 

Si la font-size change, les éléments restent équilibrés :

```scss
.module { 
  font-size: 16px; 
  padding: 1.5em; /* = 24px */
}
@media screen and(max-width: 320px) {
  .module { 
    font-size: 10px; 
    /* padding = 15px */
  }
}
```

---

## Penser "modulaire" avec `rem` 

`rem` doit être utiliser pour tout module (= bloc visuel) pouvant être réutilisé, ainsi :

- le module ne dépend pas de son parent direct
- on change la taille d'un module en une ligne

+++

### Modularité = Réutilisabilité

Chaque module est indépendant, et réutilisable :

```scss
.module { 
  font-size: 1rem; /* = 16px */ 
  padding: 1.5em; 
  h3 {
    font-size: 1.8em;
    margin-bottom: 1em; 
  } 
  aside & {
    font-size: 0.8rem;  /* = 12.8px */ 
  }
}
@media screen and(max-width: 320px) {
  html {
    font-size: 14px;
  }
}
```

---

## Utiliser `%` pour l'élément racine

Afin que la feuille de style prenne les paramètre utilisateurs en compte :

```scss
html { 
  font-size: 100%; /* 16px par défaut */ 
}
.module { 
  font-size: 1rem; 
  /* ... */
}
@media screen and(max-width: 320px) {
  html {
    font-size: 87.5%; /* 14px par défaut */
  }
}
```

---

## Récapitulatif 

- Racine de la page : `%`
- Racine d'un module : `rem`
- Intérieur d'un module : `em`

Les `px` doivent être limités aux cas particuliers, aux images et éventuellement à la structure de la page.

---

## Ressources utiles

Specification W3C : <a href="https://www.w3.org/TR/2013/CR-css3-values-20130730/" target="_blank">w3.org</a>

---

cimer.

<a href="https://twitter.com/zessx" target="_blank">@zessx</a>