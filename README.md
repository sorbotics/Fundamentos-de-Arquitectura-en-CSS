# ✨ Fundamentos de Arquitectura de CSS

Este recurso no es original. se ha obtenido los recursos del curso de [aquí](https://platzi.com/cursos/arquitecturas-css/).

## Contenido

1. [Introducción](#1-introducción)
2. [Ejemplos prácticos](#2-ejemplos-prácticos)
3. [Errores comunes al implementar BEM](#3-errores-comunes-al-implementar-bem)
4. [BEM + SASS](#4-bem--sass)
5. [Recomendaciones](#5-recomendaciones)
6. [Recursos](#6-recursos)

## 1. Introducción

Existen muchas metodologías que tienen como objetivo reducir la huella de CSS, organizar la cooperación entre programadores y mantener grandes bases de código CSS. Esto es obvio en proyectos grandes como Twitter, Facebook y GitHub, pero otros proyectos a menudo crecen hasta alcanzar un estado de "archivo CSS enorme" con bastante rapidez.

**OOCSS** — Separar contenedor y contenido con “objetos” CSS.

**SMACSS** — Guía de estilo para escribir tu CSS con cinco categorías para reglas CSS.

**SUITCSS:** nombres de clases estructurados y guiones significativos.

**Atomic:** dividir estilos en partes atómicas o indivisibles.

### Porqué y para qué utilizar BEM

1. Para tener un CSS mas fácil de leer, entender, mantener y escalar. 
2. Para organizar las clases de CSS en módulos independientes. 
3. Para evitar selectores anidados. 

No importa qué metodología elija utilizar en sus proyectos, se beneficiará de las ventajas de CSS y UI más estructurados. Algunos estilos son menos estrictos y más flexibles, mientras que otros son más fáciles de entender y adaptar en equipo.

> La razón por la que elijo BEM sobre otras metodologías se reduce a esto: es menos confuso que los > otros métodos (es decir, SMACSS) pero aún nos proporciona la buena arquitectura que queremos (es > decir, OOCSS) y con una terminología reconocible. - Mark McDonnell, CSS mantenible con BEM

### ¿Qué significa BEM?

```js
"B" - BLOQUE
"E" - ELEMENTO
"M" - MODIFICACIONES
```

### ¿Cómo funciona BEM?
```js
"BLOQUE" - Contenedor principal
"ELEMENTO" - Partes internas
"MODIFICACIONES" - Variaciones
```

### ¿Cómo utilizar BEM en CSS?

1. Guiones bajos "__" separan el bloque del elemento.
2. Guiones medios "--" separan el bloque o elemento del modificador.

```js
  - [Bloque]
  - [Bloque]__[Elemento]
  - [Bloque]--[Modificador]
  - [Elemento]--[Modificador]
  - [Bloque]__[Elemento]--[Modificador]
```

## 2. Ejemplos prácticos
![Ejemplo - Ilustración](docs/images/example.png)

#### HTML
```html
  <rocket class="falcon9 falcon9--dragon">
    <stage class="flacon9__first-stage"></stage>
    <stage class="flacon9__interstage"></stage>
    <stage class="flacon9__second-stage"></stage>
  </rocket>
```

#### CSS

```css
  .falcon9 {...}
  .falcon9--dragon {...}
  .flacon9__first-stage {...}
  .flacon9__interstage {...}
  .flacon9__second-stage {...}
```

### Ejemplos de la vida real

#### HTML
```html
  <button class="button button--active">
    <i class="button__icon"></i>
    <span class="button__text"></span>
  </button>
```

#### CSS

```css
  .button {...}
  .button--active {...}
  .button__icon {...}
  .button__text {...}
```
**[⬆ Volver arriba](#contenido)**

## 3. Errores comunes al implementar BEM

### Caso 1

Tengo un componente A que ya tiene sus propias clases y deseo añadirlo a un nuevo componente B. Debo agregar una nueva conveción para el componente A que está dentro de B?

```html
# Componente A:

<button class="button button--active"></button>

# Componente B:

<div class="card">
  <img class="card__image" src="/image.png" alt="Crew Dragon" />
</div>
```

### Solución

Puedes dejar el componente **A** con las clases que ya estaban establecidas asi no sean coherentes con el nuevo componente **B**, por ejemplo:

**🙅‍ Mal:**

```html
<div class="card">
  <img class="card__image" src="/image.png" alt="Crew Dragon" />
  <button class="card__button button--active"></button>
</div>
```

**👨‍🏫 Bien:**

```html
<div class="card">
  <img class="card__image" src="/image.png" alt="Crew Dragon" />
  <button class="button button--active"></button>
</div>
```

**[⬆ Volver arriba](#contenido)**

### Caso 2

En mi estructura de html tengo padres, hijos, nietos, tataranietos, etc; Pero **BEM** sólo deja usar 3 niveles. ¿Qué hago con los elementos nietos y sus descendientes?

### Solución

Como **BEM** no representa los niveles de tu estructura de HTML. lo ideal en este caso seria tener:

**🙅‍ Mal:**

```html
<div class="card">
  <img class="card__image" src="/image.png" alt="Crew Dragon" />
  <div class="card__footer">
    <p class="card__footer__text">
      <i class="card__footer__text__icon"></i>
    </p>
  </div>
</div>
```

**👨‍🏫 Bien:**

```html
<div class="card">
  <img class="card__image" src="/image.png" alt="Crew Dragon" />
  <div class="card__footer">
    <p class="card__text">
      <i class="card__icon"></i>
    </p>
  </div>
</div>
```

**[⬆ Volver arriba](#contenido)**

### Caso 3

Quiero utilizar la propiedad `display: none` para ocultar desde js un componente de card y componente de botón. ¿Debo crear una clase para cada componente siguiendo su propia estructura de **BEM** (`.card—hidden` y `.button—hidden`).

### Solución

Puedes crear una clase independiente a la estructura de **BEM** para aplicar propiedades generales, así reducirías la cantidad de lineas de JS ya que no tendrás que utilizar una clase específica para cada componente.

**🙅‍ Mal:**

```html
<div class="card card--hidden">
  <img class="card__image" src="/image.png" alt="Crew Dragon" />
</div>
<button class="button button--hidden"></button>

<style>
  .card--hidden {
    display: none;
  }
  .button--hidden {
    display: none;
  }
</style>
```

**👨‍🏫 Bien:**

```html
<div class="card hidden">
  <img class="card__image" src="/image.png" alt="Crew Dragon" />
</div>
<button class="button hidden"></button>

<style>
  .hidden {
    display: none;
  }
</style>
```

## 4. BEM + SASS

En este ejemplo se marca la diferencia de la declaración de los estilos tanto en **CSS** como con **SASS**.
```html
<div class="card">
  <img class="card__image" src="/image.png" alt="Crew Dragon" />
  <button class="button button--active"></button>
</div>
```

### CSS

```css
<style>
  .card {
    ...
  }
  .card__image {
    ...
  }
  .button {
    ...
  }
  .button--active {
    ...
  }
</style>
```

### SASS

```scss
<style>
  .card {
    &__image {
      ...
    }
  }
  .button {
    &--active {
      ...
    }
  }
</style>
```

**[⬆ Volver arriba](#contenido)**


## 5. Recomendaciones

Los proyectos que utilizan **BEM** son:

* Fáciles de leer
* Muy intuitivos
* Evitan selectores anidados

## 6. Recursos
* [HTML](https://developer.mozilla.org/es/docs/Web/HTML)
* [CSS](https://developer.mozilla.org/es/docs/Web/CSS)
* [BEM](https://getbem.com/introduction/)
