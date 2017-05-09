---

![Sass](assets/images/logo-sass.png)

### Where the magic happens

---

## Qu'est-ce que Sass ?

Sass (Syntactically Awesome StyleSheets) est  
un **pré-processeur**, qui génère du CSS.

Deux syntaxes possibles :
  - SASS : une syntaxe indentée
  - SCSS : une syntaxe CSS3 (avec des accolades)

---

## Sass vs CSS

- Variables et opérations
- Règles imbriquées
- Sélecteur avancé
- Mixins et placeholders
- Fonctions prédéfinies
- Structures de contrôle
- Partials

--- 

## Pré-requis

Installer Ruby

```bash
ruby -v
```

Installer Sass

```bash
gem install sass
```

---

## Utilisation

En ligne de commande

```bash
sass --update scss/input.scss:output.css
sass --watch scss/input.scss:output.css
sass --watch scss/
```

Via une application tiers  
*(Scout, Compass.app, LiveReload, Koala…)*

Via un workflow Gulp

---

## Variables

Nombres, chaînes, couleurs, booléens, null, listes, maps 

Portée globale et/ou locale (Sass 3.4+)

+++

### Exemple de variables

```scss
$fs: 16px;
$fs: 20px !default;

body {
  font-size: $fs;
}
```

+++

### Exemple compilé

```css
body {
  font-size: 16px;
}
```

---

## Opérations

- Relation : **== != < > <= >=**
- Arithmétique : **+ - * /**
- Concaténation : **+**
- Booléen : **and or not**
- Parenthèses : **( )**
- Interpolation : **#{$variable}**

---

## Règles imbriquées

Les blocs de règles peuvent être imbriqués. 

On évite la répétition de sélecteurs,  
et on gagne en lisibilité.

+++

### Exemple de règles imbriqués

```scss
a {
  text-decoration: none;
}

footer {
  a:hover {
    text-decoration: underline;
  }
}
```

+++

### Exemple compilé

```css
a {
text-decoration: none;
}

footer a:hover {
  text-decoration: underline;
}
```

---

## Sélecteur avancé

Il est possible d'utiliser le caractère **&**  
dans vos sélecteurs. 

Il s'agit du sélecteur de parent.

+++

### Exemple de sélecteur de parent

```scss
a {
  text-decoration: none;

  &:hover {
    color: tomato; 
  }

  footer & {
    text-decoration: underline; 
  }
}
```

+++

### Exemple compilé

```css
a {
  text-decoration: none; 
}

a:hover {
  color: tomato; 
}

footer a {
  text-decoration: underline; 
}
```

---

## Mixins

Les mixins peuvent être assimilés à des **fonctions**.

Le code généré par les mixins est dupliqué à chaque appel.

+++

### Exemple de mixin

```scss
@mixin border($color) {
  border: 1px solid $color; 
}

header {
  @include border(black);
  border-color: red; 
}

footer {
  @include border(black); 
}
```

+++

### Exemple compilé

```css
header {
  border: 1px solid black;
  border-color: red; 
}

footer {
  border: 1px solid black; 
}
```

---

## Placeholders

Les placeholders peuvent être assimilés à des **procédures**.

Le code généré par les placeholders est factorisé à la compilation.

+++

### Exemple de placeholder

```scss
%border {
  border: 1px solid black; 
}

header {
  @extend %border;
  border-color: red; 
}

footer {
  @extend %border; 
}
```

+++

### Exemple compilé

```css
header, footer {
  border: 1px solid black; 
}

header {
  border-color: red; 
}
```

---

## Fonctions prédéfinies

lighten, darken, saturate, desaturate, greyscale,  
opacify, transparentize, str-lengh, str-insert,  
str-index, str-slice, round, ceil, floor, abs,  
min, max, random, length, nth, join, append,  
index, map-get, map-keys, type-of, unique-id…

---

## Structures de contrôle

```scss
@if … { }
@else {}
```

```scss
@for … from … to … {}
```

```scss
@for … from … through … {}
```

```scss
@each … in … {}
```

```scss
@while … {}
```

---

## Partials

Fichiers Sass avec un nom préfixé d'un underscore.

Nom compilables en standalone.

Inclus via le mot-clé **@import** :

```scss
@import "partial";
```

Permettent de structurer les sources Sass.

---

## Sass avancé : OOSCSS

Reprise des principes de l'OOCSS.

Utilisation massive des placeholders.

Évite la surchage de code à la compilation.

+++

### Exemple d'OOCSS

```css
.font-larger {
  font-size: 130%; 
}
.centered {
  margin: 0 auto; 
}
.intro {
  padding: 25px; 
}
```

```html
<div class="intro font-larger centered">
  Lorem ipsum
</div>
```


+++

### Exemple d'OOSCSS

```css
%font-larger {
  font-size: 130%; 
}
%centered {
  margin: 0 auto; 
}
.intro {
  @extend %font-larger;
  @extend %centered;
  padding: 25px; 
}
```

```html
<div class="intro">
  Lorem ipsum
</div>
```

---

## Sass avancé : @at-root

Évite de générer des sélecteurs à rallonge.

Maintient l'organisation du fichier Sass.

Devrait être utilisé devant chaque id.

+++

### Exemple de sélecteur @at-root

```scss
.foo {
  .bar {
    background: blue;

    @at-root #baz {
      color: red; 
    }

    #qux {
      color: green; 
    }
  }
}
```

+++

### Exemple compilé

```css
.foo .bar {
  background: blue; 
}

#baz {
  color: red; 
}

.foo .bar #qux {
  color: green; 
}
```

---

## Sass avance : media queries

Les media queries doivent se trouver à la racine du CSS.

Donc incompatible avec l'imbrication Sass.

On peut utiliser un mixin pour contourner la limitation.

+++

### Exemple de mixin pour les media queries

```scss
@mixin media-min($_w) {
  @media screen and (min-width: $_w) {
    & { @content; }
  }
}

#content {
  background: blue;

  @include media-min(1024px) {
    background: red;
  }
}
```

+++

### Exemple compilé

```css
#content {
  background: blue;
}

@media screen and (min-width: 1024px) {
  #content {
    background: red;
  }
}
```

---

## Sass avancé : optimisation de mixins

But : limiter la duplication du code d'un mixin.

On place le code statique dans un placeholder.  
*(le code indépendant des paramètres)*

Seul le code dynamique sera dupliqué.

+++

### Exemple d'optimisation de mixin

```scss
%foo {
  background: black;
}

@mixin foo($_color) {
  @extend %foo;
  color: $_color;
}

header {
  @include foo(blue); 
}
footer {
  @include foo(blue); 
}
```

+++

### Exemple compilé

```css
header, footer {
  background: black;
}

header {
  color: blue;
}

footer {
  color: blue;
}
```

---

## Ressources utiles

Documentation : <a href="http://sass-lang.com" target="_blank">sass-lang.com</a>

Compilateur en ligne : <a href="http://sassmeister.com" target="_blank">sassmeister.com</a>

Librairies : <a href="http://compass-style.org" target="_blank">compass-style.org</a>, <a href="http://bourbon.io" target="_blank">bourbon.io</a>

---

cimer.

<a href="https://twitter.com/zessx" target="_blank">@zessx</a>