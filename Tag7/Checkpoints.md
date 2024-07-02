# Checkpoints

## Nennen Sie den grundsätzlichen Ablauf, wie man Daten in eine normalisierte DB bringt.
Um Daten in eine normalisierte Datenbank zu bringen, identifizieren Sie zuerst die redundanten Daten und erstellen dann separate Tabellen, um diese Redundanzen zu eliminieren. Stellen Sie sicher, dass jede Tabelle nur Daten enthält, die sich direkt auf den Primärschlüssel beziehen.

## Was ist der Unterschied zwischen logischem und physischem Backup?
Ein logisches Backup sichert die Struktur und Daten der Datenbank in einem lesbaren SQL-Format, während ein physisches Backup die tatsächlichen Datenbankdateien kopiert. Logische Backups sind einfacher zu portieren, während physische Backups schneller wiederherzustellen sind.

## Beschreibe den Restore-Prozess der drei Backup-Typen: FULL / INKREMENTELL / DIFFERENZIELL.
- FULL: Erstellen Sie die Datenbank neu und spielen Sie das vollständige Backup ein.

- INKREMENTELL: Stellen Sie zuerst das letzte vollständige Backup und dann nacheinander alle inkrementellen Backups bis zum gewünschten Zeitpunkt 
wieder her.

- DIFFERENZIELL: Stellen Sie das letzte vollständige Backup wieder her und dann das letzte differentielle Backup.

## Nenne drei Möglichkeiten, wie man ein Backup einer Datenbasis machen kann. Wie sind die konkreten Befehle oder das konkrete Vorgehen?

```
MySQLDump: mysqldump -u root -p database_name > backup.sql

phpMyAdmin: Navigieren Sie zu Exportieren, wählen Sie die Datenbank aus und laden Sie das Backup herunter.

Docker: docker exec -it mysql /usr/bin/mysqldump -u root -p database_name --result-file=/var/lib/mysql/backup.sql
```

## Was sind die (5) Schritte, um eine DB in die 3.NF zu normalisieren?
Identifizieren und Entfernen von Wiederholenden Gruppen (1NF):

1. Stellen Sie sicher, dass jede Tabelle eine einheitliche Struktur hat, indem Sie alle Felder atomar machen, also keine wiederholenden Gruppen oder Arrays in einem einzigen Feld haben.
Erstellen Sie separate Tabellen für jede Gruppe verwandter Daten (1NF):

2. Teilen Sie Ihre Daten in Tabellen auf, sodass jede Tabelle eine zusammenhängende Gruppe von Daten darstellt. Jeder Eintrag sollte eindeutig identifizierbar sein, oft durch einen Primärschlüssel.
Entfernen Sie partielle Abhängigkeiten (2NF):

3. Stellen Sie sicher, dass alle Nicht-Schlüssel-Attribute vollständig funktional abhängig vom gesamten Primärschlüssel sind. Dies bedeutet, dass es keine Felder gibt, die nur von einem Teil des zusammengesetzten Schlüssels abhängig sind.
Erstellen Sie separate Tabellen für thematisch zusammenhängende Daten (2NF):

4. Zerlegen Sie Tabellen weiter, sodass jede Tabelle sich auf ein einziges Thema konzentriert und die Abhängigkeiten von Nicht-Schlüssel-Attributen von einem zusammengesetzten Primärschlüssel beseitigt werden.
Entfernen Sie transitive Abhängigkeiten (3NF):

5. tellen Sie sicher, dass alle Nicht-Schlüssel-Attribute nur vom Primärschlüssel abhängen und nicht voneinander. Verschieben Sie alle Attribute, die indirekt vom Primärschlüssel abhängen, in separate Tabellen.

## Was macht der Befehl SELECT INTO OUTFILE?
Der Befehl SELECT INTO OUTFILE exportiert das Ergebnis einer SQL-Abfrage in eine Datei auf dem Server, was nützlich ist, um Daten schnell in ein externes Dateiformat zu speichern. Beispiel: SELECT * FROM table_name INTO OUTFILE 'file_path'.
