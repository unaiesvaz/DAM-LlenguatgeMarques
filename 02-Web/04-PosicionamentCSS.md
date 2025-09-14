1. Introducció al posicionament
Per què serveix el posicionament CSS (organitzar i distribuir els elements a la pàgina).
Diferència entre flux normal i quan fem servir tècniques de posicionament.
2. Elements de bloc i elements de línia
Elements de bloc: ocupen tot l’ample disponible, comencen en línia nova. Ex: <div>, <p>, <h1>.
Elements de línia: només ocupen l’espai del contingut, es posen un al costat de l’altre. Ex: <span>, <a>, <strong>.
Exemple visual senzill.
Nota: amb CSS (display) podem canviar un element de bloc a línia i viceversa.
3. Propietat display
Valors bàsics:
block
inline
inline-block
none
Exemple de cada cas.
4. Posicionament bàsic
Propietat position:
static (per defecte).
relative.
absolute.
fixed.
sticky.
Explicar top, left, right, bottom.
Exemple amb caixes acolorides.
5. Posicionament amb Flexbox
Què és flexbox i per què s’utilitza.
Contenidor → display: flex;.
Direcció principal (flex-direction: row / column).
Alineació (justify-content: start, center, space-between...).
Alineació transversal (align-items: start, center, stretch...).
Exemple senzill amb 3 caixes.
6. Posicionament amb Grid
Què és grid i diferència amb flexbox (bidimensional vs unidimensional).
Contenidor → display: grid;.
Definir columnes i files (grid-template-columns, grid-template-rows).
Separació (gap).
Posicionar elements amb grid-column i grid-row.
Exemple senzill amb 4 caixes en una graella 2x2.
7. Comparació ràpida Flex vs Grid
Flex → millor per distribuir elements en una sola direcció (fila o columna).
Grid → millor per estructures complexes en dues direccions (files i columnes).
8. Resum i bones pràctiques
Usar flex per menús, barres de navegació, distribucions simples.
Usar grid per maqueta general de la pàgina.
Recordar que block i inline són la base, i display permet transformar-los.