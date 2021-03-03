# Danish Sermons
 
This repository present a corpus of 11,955 sermons from the Evangelical Lutheran Church in Denmark (ELCD), which is structured for a relational database. The repository only includes metadata, since the corpus texts contain sensitive personal information.

## Metadata
The corpus metadata is included in the file metadata.csv as a table with the following columns. The labels are composed in Danish.

```
Kolonnenavn             | Beskrivelse
------------------------------------------------------------
dokumentId              | id of the document holding the sermon's text
præstId                 | id of the pastor who wrote the sermon
dato                    | date of the church service
helligdag               | church holiday 
sogn str.               | inhabitants in the parish for which the sermon is composed (ELCD members/total) 
stift                   | name of diocese
årgang                  | the pastor's birth year
køn                     | the pastor's sex
uddannelsessted         | the pastor's place of education

```  

## Data Model
The data has been normalised to avoid ambivalence. In order to resemble the relationship between data points, the columns in the table have been divided between two distinct data models: __Prædiken__ og __Præst__. The models each describe a data class. The classes and their features are explicated in the following:

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
