# Exercici002: 

Construir una mini-web corporativa amb 3 pàgines, aplicant max-width + auto-center, Flex i Grid. 

La temàtica pot ser: "un gimnàs", "una botiga de roba", ...

Estructura de projecte
```text
exercici-002/
├── index.html
├── productes.html
└── contacte.html
└── global.css
```

## Estils

L'arxiu "global.css" té els estils comuns a totes les pàgines

Cada HTML té el seu `<style>`amb l'estil particular d'aquella pàgina.

## index.html

Landing, pàgina principal amb "max-width" i "auto-center".

Ha de ser la pàgina principal que presenta l'empressa.

**Requisits de maquetació**

- Contenidor centrat: max-width (p. ex. 1100px) + margin: auto.
- Hero al capdamunt (títol, subtítol i un botó “Comprar ara” amb display: inline-block).
- Secció “Col·leccions” amb 3 blocs informatius (cartes simples).
    * Títols i paràgrafs com elements de bloc.
    * Etiquetes curtes (p. ex. “Nou”, “Eco”, “Outlet”) com elements de línia (span) dins el text.
- Banda de beneficis en horitzontal amb Flex (p. ex.: Enviament 48h · Canvis gratuïts · Pagament segur).
- Peu amb info bàsica.

**Criteris de validació**

- El layout es manté centrat i llegible a diferents amplades.
- Es distingeix clarament bloc vs línia (p. ex. spans dins paràgrafs).
- El botó es veu amb padding propi (gràcies a inline-block).
- La banda de beneficis usa Flex (distribució horitzontal i gap).

## productes.html

Catàleg i flex, amb tergetes (cards) tipus wrap

Ha de ser una pàgina on es mostren els productes o serveis de l'empressa.

**Requisits de maquetació**

- Barra de filtres al capdamunt: elements en línia (p. ex. span o a) que es col·loquen un al costat de l’altre (sense canviar a bloc).
- Grid de targetes amb Flex: contenidor display: flex; flex-wrap: wrap; gap: …;
    * Cada targeta: imatge fictícia (caixa de color amb alçada), nom del producte i preu.
    * Amplada flexible: flex: 1 1 260px (o similar) perquè s’adaptin a l’ample i saltin de línia si cal.
- Peu amb info bàsica.

**Criteris de validació**

- Les targetes reflueixen (wrap) quan redueixes l’amplada de la finestra.
- La barra de filtres és clarament elements en línia (no salten de línia si hi ha espai).

## contacte.html

Bloc informatiu amb Grid de dues columnes, amb auto-center.

Busca a internet informació sobre com mostrar un mapa de google en una pàgina web i posa-hi un mapa amb la direcció de l'institut.

**Requisits de maquetació**

- Contenidor centrat: max-width + margin: auto.
- Secció principal amb CSS Grid:
display: grid; grid-template-columns: 1fr 1fr; gap: …; (en pantalles estretes, pots passar a 1 columna amb repeat(auto-fit, minmax(...)) si voleu responsivitat bàsica).
    * Columna A: formulari de contacte senzill (nom, email, missatge; sense JS).
    * Columna B: informació de botiga (adreça, horari, telèfon) i un “mapa” fictici (caixa grisa amb alçada).
- Peu amb info bàsica.

**Criteris de validació**

- El Grid mostra dues columnes en ample adequat i 1 columna quan l’espai és limitat (si useu auto-fit/minmax).
- El formulari i el bloc d’informació queden alineats i espaiats amb gap.
