
# DTD és Document Type Definition

## Validació d'arxius ".xml"

Hi ha dues formes de validar els arxius ".xml":

- Que estàn ben formats (tots els elements ben tancats, ...)
- Que segueixen una estructura específica **DTD**

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

Per poder validar si un arxiu ".xml" és correcte, es pot fer servir **"xmllint"**:

```bash
cd "01-XML/Teoria/ExempleB/"
xmllint --noout --valid note.xml
```

El resultat és "buit" perquè no hi han errors, en canvi:

```bash
cd "01-XML/Teoria/ExempleB/"
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