# Bulkimport

## CSV Datei vom Server laden
MySQL bietet die Möglichkeit, CSV-Dateien effizient und schnell in Tabellen einzulesen. Mit dem Kommando LOAD DATA INFILE "/path/file.csv" kann der MariaDB-Server die Eingabedatei aus seinem eigenen Dateisystem lesen. Ohne Pfadangabe sucht der Server die Datei im Data-Verzeichnis der aktuellen Datenbasis. Pfadangaben müssen in MySQL mit / erfolgen, wie bei Linux/Unix/macOS.

## CSV Datei vom Client laden
Mit LOAD DATA LOCAL INFILE "c:/path/file.csv" kann der Client die Eingabedatei aus seinem Dateisystem lesen und den Inhalt an den MariaDB-Server senden. Dadurch können Dateien aus dem lokalen Dateisystem des Clients in die Datenbank geladen werden. Dieser Vorgang ist aus Sicherheitsgründen standardmäßig im Server und Client deaktiviert.

Settings
Um den Import zu ermöglichen, muss der Server die Einstellung SET GLOBAL local_infile=1; haben. Überprüfen lässt sich dies mit SHOW GLOBAL VARIABLES LIKE 'local_infile';. Es sollte kein spezieller Import-Pfad gesetzt sein (SHOW VARIABLES LIKE 'secure_file_priv';). Falls doch, sollte die my.ini im Abschnitt [mysqld] entsprechend angepasst werden: secure_file_priv = "". Der MySQL-Client benötigt in der my.ini die Einstellung MYSQL_OPT_LOCAL_INFILE=1. Bei der MySQL Workbench muss in den Connection-Einstellungen OPT_LOCAL_INFILE=1 hinzugefügt werden.

## Daten aus anderer Tabelle einfügen
Mit dem Befehl INSERT INTO customers (name, email, address) SELECT name, email, address FROM new_customers; können Daten aus einer Tabelle in eine andere eingefügt werden. Dies ermöglicht das Übertragen von Daten zwischen Tabellen innerhalb der Datenbank.