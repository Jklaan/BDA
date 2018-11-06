# BDA

## Struktur des Gits

```
BDA
│   README.md  
│
└───Data
│   │   gender_submission.csv
│   │   train.csv
|   |   test.csv
│   
└───KNIME
|   └─  .metadata
|   └─  Family_survived        
|   └─  Heatmap_alternative
|   └─  Heatmap der korrelationen
|   └─  Knime Aufgaben.docx            <- Beschreibung der Aufgabendurchführung
|   └─  titanic_kabine                 <- Zusatzaufgabe
|
└───Output
    | out.png                          
```
## Annahmen
 1.) Familien können über einen gemeinsamen Nachnamen identifiziert werden
 2.) Die Familiengröße entspricht ```sibsp+parch+1 ```, also der Summe aus Elternteilen, Geschwistern und der aktuell betrachteten Person
 3.) Als Familie gelten nur Personen mit einer Familiengröße von zwei oder mehr

## Vorbereitung der Daten in Cloudera
Beim Anlegen der Datenbank und dem Laden der Daten in die Tabelle wurden zunächst die Passagiernamen in Vor- und Nachname geteilt um Familien im späteren Verlauf anhand der Nachnamen identifizieren zu können.
 
## Durchführung der Analyse in Knime

Zunächst wurden die Cloudera HIVE Datenbank mit Hilfe des Hive Connectors mit KNIME verbunden. 
Anschließend wurde die Datentabelle in Knime geladen. Dabei haben wir bei der Abfrage schon die Familienzugehörigkeit sowie die Familiengröße geprüft.

```sql
Select *, sibsp+parch+1 as family
from traincsv
where sibsp+parch+1!=1
```
Anschließend wurden die Daten nach der Summe der Überlebenden gruppiert und anschließend geprüft von welchen Familien alle Angehörigen überleben, bzw. mindestens eine Person gestorben ist. 

## Zusatzaufgabe: Hat die Wahl der Kabine einen Einfluss auf die Überlebensrate der Passagiere?

### Vorbereitung:

-	Testdaten wurden mit der Subgender Datei zusammengefasst, nennen wir das Ergebnis Test_full
-	die Spalten wurden in Benennung und Reihenfolge an die Trainingsdaten angepasst
-	anschließend wurden Test_full und die Trainingsdaten zusammengefasst

### Hypothesen:

Nach einer Ersten, kurzen Analyse der Daten wurden größere diskrepanzen in der Datenbasis entdeckt. Dazu wurde folgende Hypothese aufgestellt:

1.) Die Überlebenden wurden im Nachgang bei der Datenerhebung nach Ihrer Kabinenummer und denen ihrer Mitreisenden/Nachbarn gefragt. Und ob           letztere überlebt haben.

Für die Beantwortung der Hauptfrage wurde die zweite Hypothese aufgestellt:

2.) Die Klasse hat einen Merkliche Einfluss auf die Überlebensrate

Die detaillierte Beschreibung und Vorgehensweise der Durchführung und Beantwortung der Analysefragen können dem Dokument "Knime Aufgaben.docx" entnommen werden
