# CSS bàsic

## Què és CSS?

**CSS (Cascading Style Sheets)** és el llenguatge que serveix per definir l’aspecte (colors, mides, marges, fonts...) dels elements HTML d’una pàgina web.

Dit d’una altra manera:

```text
Si HTML és l’esquelet de la pàgina (estructura i contingut),
CSS és el disseny i decoració (colors, aparença).
```

[Documentació CSS](https://developer.mozilla.org/en-US/docs/Web/CSS#reference)

## Maneres de definir CSS

Hi ha tres maneres principals d’afegir CSS a una pàgina web:

### CSS en línia (inline CSS)

S’escriu directament dins de l’atribut style de l’element HTML.

```html
<p style="color: red; font-size: 20px;">Aquest text és vermell i gran.</p>
```

**Important**: S'ha d'evitar aquesta manera de definir CSS, perquè normalment el valor de l'atribut **"style"** es modificar a partir de la programació amb *JavaScript*.

### CSS dins del document (internal CSS)

S’escriu dins de l’element `<style>` que va a la secció `<head>` de la pàgina HTML.

Dins d'aquest element es defineixen les propietats CSS, en aquest exemple diem que volem mostrar els elements de paràgraf `<p>` de color blau i el doble de gran de l'habitual.

```html
<head>
  <style>
    p {
      color: blue;
      font-size: 2em;
    }
  </style>
</head>
<body>
  <p>Aquest text és blau.</p>
</body>
```

**Important**: D'aquesta manera els estils definits només afecten la pàgina on es defineixen. Quan hi ha molt codi CSS costa d'organitzar.

### CSS en un fitxer (external CSS)

S’escriu en un arxiu .css separat i s’importa amb un element `<link>` dins del `<head>`.

**Exemple-004**: Obrir amb "Show preview" la pàgina "02-Web/exemple-004/index.html"

**Important**: Moltes pàgines web, defineixen els estils combinant les tècniques anteriors:

- **Inline**: per CSS modificat a través de JavaScript
- **Internal**: per ajustos específics del document
- **External**: per compartir estils entre diverses pàgines web

## Maneres d’assignar CSS als elements HTML

Un cop definits els estils, els podem aplicar de diferents maneres:

### Per etiqueta

Afecta a tots els elements d'aquell tipus, en aquest cas tots els `<p>` tindràn color lila:
```css
p {
  color: purple;
}
```

### Per identificador "id"

’aplica a un element amb un id únic.

**Important**, cada element ha de tenir un **id** diferent, per tant un estil definit amb **id** només es pot aplicar a un element.

Al CSS es defineix amb **#** davant de l'etiqueta:
```css
#titol {
  font-size: 24px;
  text-decoration: underline;
}
```
```html
<h1 id="titol">Títol principal</h1>
```

### Per atribut "class"

Afecta tots els elements, que posin l'etiqueta definida al CSS a l'atribut **class"**
```css
.text-important {
  color: red;
  font-weight: bold;
}
```
```html
<p class="text-important">Aquest text és vermell i en negreta.</p>
```

Les diferències amb l'**id** són que:
- Es pot assignar aquell estil a múltiples elements 
- Es poden assignar múltiples etiquetes a l'element class

```css
.vermell {
  color: red;
}
.gran {
  font-size: 24px;
}
.negreta {
  font-weight: bold;
}
.subratllat {
  text-decoration: underline;
}
```
```html
 <h1 class="vermell gran">Títol vermell i gran</h1>

<p class="negreta">Aquest paràgraf és només en negreta.</p>

<p class="vermell subratllat">Aquest paràgraf és vermell i subratllat.</p>

<p class="gran negreta subratllat">
  Aquest paràgraf és gran, en negreta i subratllat.
</p>
```

**Exemple-005**: Obrir amb "Show preview" la pàgina "02-Web/exemple-005/index.html"

## Pseudoclasses CSS

Les **Pseudoclasses** són “estats especials” que serveixen per aplicar estils quan passa una condició, s’escriuen amb : davant del nom.

**Interacció amb l'usuari**

- **:hover** → quan el ratolí passa per sobre d’un element.
- **:active** → quan l’element està sent clicat.
- **:focus** → quan l’element (per exemple, un input) té el focus del teclat.

**Posició dins del contenidor**

- **:first-child** → el primer fill d’un element.
- **:last-child** → l’últim fill d’un element.
- **:nth-child(n)** → el fill número n (o amb patrons com odd, even).
- **:first-of-type**, 
- **:last-of-type** → el primer/últim element d’un tipus concret.

**Per estat de formularis**

- **:checked** → un checkbox o radiobutton seleccionat.
- **:disabled** → un element de formulari deshabilitat.
- **:enabled** → un element de formulari habilitat.
- **:required** → un camp obligatori.
- **:valid / :invalid** → segons si el valor del formulari és vàlid o no.

**Exemple-006**: Obrir amb "Show preview" la pàgina "02-Web/exemple-006/index.html"