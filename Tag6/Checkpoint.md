# Checkpoint

## Formulieren Sie einen Satz, der den Einsatz von Subqueries erklärt und begründet.
Subqueries ermöglichen es, komplexe Abfragen zu erstellen, indem sie Ergebnisse aus einer Unterabfrage in die Hauptabfrage integrieren und so Daten aus verschiedenen Perspektiven effizienter analysieren.

## Was ist der Unterschied zwischen skalaren und nicht-skalaren Subqueries?
Skalare Subqueries geben nur eine einzelne Zeile mit einer Spalte zurück und können direkt in Bedingungen wie =, >, < verwendet werden. Nicht-skalare Subqueries liefern mehrere Zeilen und/oder Spalten und werden häufig mit Operatoren wie IN, EXISTS oder JOIN genutzt.

## Was bedeutet der Zusatz IGNORE 1 LINES in LOAD DATA INFILE?
Der Zusatz IGNORE 1 LINES in LOAD DATA INFILE bedeutet, dass die erste Zeile der Datei ignoriert wird, was oft verwendet wird, um Kopfzeilen in CSV-Dateien zu überspringen.

## Sie haben eine Windows-CSV-Datei. Der Import ist aber mit LINES TERMINATED BY '/n'; eingestellt. Welche Folgen hat das für die letzte Spalte (Attribut) der importierten Daten? Gibt es ein Problem?
Wenn der Import mit LINES TERMINATED BY '/n' eingestellt ist und die Datei tatsächlich Windows-Zeilenenden (\r\n) verwendet, wird die letzte Spalte möglicherweise nicht korrekt importiert, da die Zeilenende-Zeichen nicht richtig erkannt werden. Dies kann zu Datenverlust oder fehlerhaften Datensätzen führen.

## Welche Einstellungen müssen gemacht werden, damit ein Klient eine CSV-Datei dem Server zum Importieren übermitteln darf?
Um einem Klienten den Import einer CSV-Datei auf den Server zu ermöglichen, müssen entsprechende Benutzerrechte gewährt und eventuell der Pfad zu den Dateien konfiguriert werden. Der Benutzer muss die Berechtigung FILE besitzen, und der Server muss so konfiguriert sein, dass er den Zugriff auf die notwendigen Verzeichnisse zulässt.

## Wie importieren Sie Spalten in einer anderen Reihenfolge?
Um Spalten in einer anderen Reihenfolge zu importieren, kann die LOAD DATA INFILE-Anweisung mit einer expliziten Spaltenliste verwendet werden, die die gewünschte Reihenfolge angibt:

```
LOAD DATA INFILE 'file.csv'
INTO TABLE tablename
FIELDS TERMINATED BY ','
LINES TERMINATED BY '\r\n'
(column2, column1, column3);
```