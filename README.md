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
|   └─  Family_survived         <- KNIME Workflow
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
Anschließend wurden die Daten nach der Summer der Überlebenden gruppiert und anschließend geprüft von welchen Familien alle Angehörigen überleben, bzw. mindestens eine Person gestorben ist. 
Für die Durchführung der Korellation wurde die, durch die Gruppierung, hinzugefügte Spalte "Zusammen?" in einen binäres Objekt umgewandelt.
Abschließend wurde die Korrelation durchgeführt und die Heatmap als Ergebnis in Form einer Grafik gespeichert.

## Beantwortung der Frage 



