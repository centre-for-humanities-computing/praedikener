# Prædikener
 
Dette repositorie genspejler hvordan indsamlede data renses og struktureres for at blive gemt i en relationel database. Denne opførelse udelukker selve prædikernes tekster for at undgå at dele personfølsomme data. 

## Oprindelig Metadata
Indsamlingens oprindelige metadata var i form af en tabel med de følgende kolonner. 

```
Kolonnenavn             | Beskrivelse
------------------------------------------------------------
dokumentId              | id på dokumentet med prædikens text
præstId                 | id på den afholdenede praæst
dato                    | datoen prædiken blev holdt på 
helligdag               | relevant helligdag
sognIndbyggere          | sognens indbyggere 
sognMedlemmer           | sognens antal medlemmer i folkekirken
stift                   | stiftens navn
årgang                  | præstens årgang
køn                     | præstens køn
uddannelsessted         | præstens uddannelsessted
kommentarer             | noter vedrorende data indsamling
```

## Rensning
Indsamlede data blev renset for persondata for at opnå tilstrækkelig anonymisering af deltagerne. For dette formål blev kolonnen _kommentarer_ slettet. Yderligere nævnes stifter som afholdesessted fremfor navn på sognet for at øge anonymisering af meta data. Data modellerne anonymiserer præsternes køn ved at bruge aliaserne 1 og 2 for mandlig of kvindelig køn, uden at oplyse hvilken alias indikerer hvilket køn.   

## Data Model
Indsamlede data blev normaliseret for at undgå duplering og ambivalens. For at genspejle data punkternes relationer blev tabellens kolonner fordelt på tre deciderede data modeller: __Prædiken__ og __Præst__. Modellerne beskriver hver deres egen data klasse. Klasserne og egenskaber beskrives i det følgende.

### Prædiken
Klassen __Prædiken__ indeholder data punkter om begivelsen for selve prædikens levering. _Præst_ holder en reference til den __Præst__ som holdt prædiken. _Stift_ nævner hvilken stift prædiken blev afholdt i. _SognIndbyggere_ gemmer antal indbyggere i sognet. _SognMedlemmer_ tæller hvor mange medlemmer af folkekirken der er i sognet. _Text_ indeholder prædikens indhold i klartekst.  

```
Prædiken: {
    præst:              <id Præst>,
    stift:              String,
    sognIndbyggere:     Integer,
    sognMedlemmer:      Integer
    text:               String
}
```

### Præst
Klassen __Præst__ specificerer generelle data om personen. _Køn_ klassificerer mandlige og kvindelige præster uden at nævne kønnet (1 eller 2). _Uddannelsessted_ nævner byen praæsten fik sin uddannelse i. _Årgang_ indholder præstens fødselsår. 
```
Præst: {
    køn:                Integer,
    uddannelsesSted:    String,
    årgang:             Integer,
}
```

## Data Graf
Grafen for modellerne og deres relation vises nedenfor. Integers er vist i rød, strings i grøn og Data klasserne kan skelnes i farve.

![graf](./graf.png)
