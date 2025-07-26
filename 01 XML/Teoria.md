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

## DTD és Document Type Definition

**DTD** explica quina és una estructura vàlida per un arxiu de dades ".xml"

Arxiu de dades: **note.xml**
```xml
<?xml version="1.1" encoding="UTF-8"?>
<!DOCTYPE note SYSTEM "note.dtd">
<note>
   <to>Tove</to>
   <from>Jani</from>
   <heading>Reminder</heading>
   <body>Don't forget me this weekend!</body>
</note>
```

Arxiu de validació: **note.dtd**
```xml
<!ELEMENT note (to,from,heading,body)>
<!ELEMENT to (#PCDATA)>
<!ELEMENT from (#PCDATA)>
<!ELEMENT heading (#PCDATA)>
<!ELEMENT body (#PCDATA)>
```

## Blocs del DTD

**Elements**: elements que apareixen a l'".xml"

**Attributs**: propietats dels elements
Entitats: caràcters especials predefinides (&lt;&gt; &amp; &quot; &apos;)

**PCDATA**: text que hi ha dins de l’element

**CDATA**: blocs de dades que s’ignoren pel validador

### Elements

Els elements es declaren amb:
```xml
<!ELEMENT element-name category>
<!ELEMENT element-name (element-content)>
```

Element buit:
```xml
<!ELEMENT br EMPTY>

<br />
```

Element amb text:
```xml
<!ELEMENT element-name (#PCDATA)>
<!ELEMENT nom (#PCDATA)>

<nom>Batman</nom>
```

Element amb qualsevol contingut (elements o text barrejats):
```xml
<!ELEMENT element-name ANY>
<!ELEMENT body ANY>

<body>Batman<br/>Robin</body>
```
Elements amb fills específics:
```xml
<!ELEMENT element-name (child1,child2,...)>

<!ELEMENT note (to,from)>
<!ELEMENT to (#PCDATA)>
<!ELEMENT from (#PCDATA)>

<note><to>Berlin</to><from>Munich</from></note>
```

### Llistes d'elements

Llistes amb 0 o més elements * :
```xml
<!ELEMENT element-name (child1*)>
<!ELEMENT usuaris (usuari*)>

<usuaris>
</usuaris>
```

Llistes amb 0 o 1 element ? :
```xml
<!ELEMENT element-name (child1?)>
<!ELEMENT usuaris (usuari?)>

<usuaris>
</usuaris>
```

Llistes 1 o més elements + :
```xml
<!ELEMENT element-name (child1+)>
<!ELEMENT usuaris (usuari+)>

<usuaris>
	<usuari>
		<nom>PacMan</nom>
</usuari>
</usuaris>
```

### Elements opcionals

Elements que són una opció o una altre (a | b):
```xml
<!ELEMENT carta (from, (message|body))>

<carta>
	<from>Pocoyo</from>
	<message>Hi</message>
</carta>

<carta>
	<from>Pocoyo</from>
	<body>Hi</body>
</carta>
```

Contingut mixte que conté elements especfics:
```xml
<!ELEMENT note (#PCDATA|to|from|header|message)*>

<note>
	Hola que tal?
	<from>Pocoyo</from>
	<message>Hi</message>
</note>
```

### Atributs dels elements

Atributs que poden tenir els elements, es declaren sota de l’element:
```xml
<!ATTLIST element-name attribute-name attribute-type attribute-value>
```
Per exemple:
```xml
<!ELEMENT square EMPTY>
<!ATTLIST square width CDATA "0">

<square width=”100”/>
```

Principals tipus d’atributs:

- **CDATA**: Cadena de text

- **(en1|en2|...)**: El valor ha de ser un dels de la llista

- **ID**: El valor és un identificador únic (si es repeteix dóna error)

Els atributs es poden definir amb una propietat:

- **#REQUIRED**: és obligatori que aparegui l’atribut amb un valor vàlid

- **#IMPLIED**: l’atribut és opcional

- **#FIXED valor**: l’atribut només accepta aquest valor

Exemple:
```xml
<!ATTLIST person number CDATA #REQUIRED>
```

### Atributs vs elements

Els atributs són configuracions del propi element, no dades contingudes en aquest. A més:

- Els atributs no poden tenir múltiples valors
- Els atributs no poden descriure estructures
- Els atributs compliquen la validació DTD
- Els atributs faciliten l’ús de identificadors i la seva validació: 
```xml
<note id="p501">
```

Els atributs s’han de fer servir amb precaució, només quan és clar que són necessaris


---
*Nota*: [Aquí](https://www.w3schools.com/xml/xml_dtd_attributes.asp) teniu la llista d'atributs completa

## Validació dels arxius

Per poder validar si un arxiu ".xml" és correcte, pot fer servir **"xmllint"**:

```bash
xmllint --noout --valid note.xml
```

La instrucció valida el format XML i l'estructura DTD.

```bash
cd "01 XML/exemple00/"
xmllint --noout --valid note.xml
```

El resultat és "buit" perquè no hi han errors, en canvi:

```bash
xmllint --noout --valid errornote.xml
```

Dona els errors de l'arxi "errornote.xml":

- Espera un element "from" i rep un "fromx"
- L'element "body" no està tancat abans de "</note>"

```text
errornote.xml:5: element fromx: validity error : No declaration for element fromx
   <fromx>Jani</fromx>
                      ^
errornote.xml:8: parser error : Opening and ending tag mismatch: body line 7 and note
</note>
       ^
errornote.xml:8: parser error : Premature end of data in tag note line 3
</note>                                       ^
```