# XML eXtensible Markup Language

Format universal per a documents i dades estructurades a Internet

És a dir:

**".xml"** és un format **de text** que permet crear arxius, on les dades estan estructurades i són fàcils de compartir i transformar a altres formats

Aplicacions habituals:

- Arxius d’ofimàtica (docx, xlsx …)
- Paràmetres de configuració (.plist)
- Dibuixos tècnics (.svg)
- Pàgines web (.html)
- …

Carecterístiques:

- És **portable** (és a dir fàcil d’interpretar per diferents aplicacions)
- **Depuració** (és fàcil veure si el format és correcte o incorrecte)
- **Independència** de la plataforma (no depèn ni del processador ni del SO)
- **Editable** (arxius de text plà)

Exemple d'".xml":

```xml
<?xml version="1.1" encoding="UTF-8" ?>
<!DOCTYPE note SYSTEM “note.dtd”>
<comanda>
	<producte codi="a0" seccio="b">
		<nom>Xinxeta</nom>
		<quantitat>20</quantitat>
	</producte>
	<producte codi="a1" seccio="c">
		<nom>Boli</nom>
		<quantitat>10</quantitat>
	</producte>
	<enviament origen="Sevilla" desti="Barcelona" />
</comanda>
```

Explicació:

**?xml?**: Defineix la versió de XML i el format de l'arxiu
```xml
<?xml version="1.1" encoding="UTF-8" ?>
```

**!DOCTYPE**: És opcional, serveix per validar que els elements i els atributs segueixen una definició específica
```xml
<!DOCTYPE note SYSTEM “note.dtd”>
```

**Elements/Tags/Etiquetes**: donen estructura a les dades

- Es defineixen entre < i >
- Diferèncien entre majúscules i minúscules
- Poden tenir altres elements a dins

```xml
<comanda/>, <producte/>, <nom/>, ...
```

Els elements són continguts, és a dir:

- Si no tenen dades a dins es tanquen amb **"/>"**

```xml
<valor/>
```

- Si tenen dades a dins es tanquen amb **"</"**

```xml
<nom>Xinxeta</nom>
```

- Poden tenir altres elemens dins:

```xml
<producte>
	<nom>Xinxeta</nom>
	<quantitat>20</quantitat>
</producte>
```

**Atributs**: configuren l'element sense tenir en compte els continguts

- Són opcionals, poden tenir 0 o més atributs

```xml
<producte/>
<producte codi="a0"/>
<producte codi="a1" seccio="b1"/>
```

- El format és: **etiqueta="valor"**

```xml
<producte codi="a1" seccio="b1">
	<nom>Xinxeta</nom>
	<quantitat>20</quantitat>
</producte>
```

Els atributs es poden anidar (posar uns dins d'altres), però s'han de tancar en ordre invers als que s'han definit:

- Correcte:

```xml
<comanda>
	<producte>Xinxeta</producte>
</comanda>
```

- Erroni (mal tancat):

```xml
<comanda>
	<producte>Xinxeta</comanda>
</producte>
```

**Valors**: Els elements poden tenir valors finals, en aquest exemple "Xinxeta" i "20"

```xml
<producte>
	<nom>Xinxeta</nom>
	<quantitat>20</quantitat>
</producte>
```

**Comentaris**: troços explicatius a l'arxiu ".xml" que no afecten a la informació de les dades, van entre **!--** i **--**

```xml
<!-- Els productes no són radioactius -->
<producte>
	<nom>Xinxeta</nom>
	<quantitat>20</quantitat>
</producte>
```

## Arbre d'elements ".xml"

Els documents ".xml" són un conjunt d’informació organitzada en una estructura de arbre:

```xml
<?xml version="1.1" encoding="UTF-8" ?>
<!DOCTYPE note SYSTEM “note.dtd”>
<comanda>
	<producte codi="a0" seccio="b">
		<nom>Xinxeta</nom>
		<quantitat>20</quantitat>
	</producte>
	<producte codi="a1" seccio="c">
		<nom>Boli</nom>
		<quantitat>10</quantitat>
	</producte>
	<enviament origen="Sevilla" desti="Barcelona" />
</comanda>
```

```text
* element: comanda
  │
  ├ element: producte
  │ │   atribut "codi", valor: "a0"
  │ │   atribut "seccio", valor: "b"
  │ │
  │ ├ element: "nom", valor: "Xinxeta"
  │ └ element: "quantitat", valor: "20"
  │
  ├ element: producte
  │ │   atribut "codi", valor: "a1"
  │ │   atribut "seccio", valor: "c"
  │ │
  │ ├ element: "nom", valor: "Boli"
  │ └ element: "quantitat", valor "10"
  │
  └ element: enviament
        atribut "origen", valor "Sevilla"
        atribut "desti", valor "Barcelona"
```

L'element principal s'anomena **arrel** o **root**, a l'exemple anterior és "comanda"

## Caràcters especials

".xml" reserva una sèrie de caràcters per poder donar format a l'arxiu:

```text
< > “ ‘ &
```

Per poder-los fer servir en els valors finals de text, hi ha les següents equivalències:

```text
< s’escriu amb &lth; (lower than)
> s’escriu amb &gt;  (greather than)
“ s’escriu amb &quot;
‘ s’escriu amb &apos;
& s’escriu amb &amp;
```

Exemple d'ús de caràcters especials:

```xml
<producte codi=”a0” seccio=”b”>
	<nom>Pinyol i &quot;arxinacs&quot;</nom>
<marca>Ben&amp;Joe</marca>
</producte>
```

Representa els textes:

```text
	Nom: Pinyol i “arxinacs”
	Marca: Ben&Joe
```

## Seccions CDATA

Les seccions CDATA permeten escriure codi que no serà processat:

```xml
<element>
	<material>fusta</fusta>
<![CDATA[
Normalment les seccions CDATA contenen instruccions específiques d’una aplicació, però que els intèrprets de ".xml" ignoren completament
]]>
</element>
```

## Instruccions de processament

Les instruccions de processament van entre <? i ?> l’interpret valida que segueixin el format establert. 

Exemples:

```xml
<?sort ascending ?>
<?php 2+3 ?>
<?xml-stylesheet type=”text/xsl” href=”estils.css” ?>
<?xml version=”1.1” ?>
```

# Validació d'arxius ".xml"

Hi ha dues formes de validar els arxius ".xml":

- Que estàn ben formats (tots els elements ben tancats, ...)
- Que segueixen una estructura específica **DTD**

Per poder validar si un arxiu ".xml" és correcte, es pot fer servir **"xmllint"**:

```bash
cd "01-XML/Teoria/ExempleA/"
xmllint --noout --valid player.xml
```

El resultat és "buit" perquè no hi han errors, en canvi:

```bash
cd "01-XML/Teoria/ExempleA/"
xmllint --noout --valid errorplayer.xml
```