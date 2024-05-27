# Anlegen einer Datenbank
In MySQL ist ein Schema ein Synonym für Datenbank. DBS können mehrere Schemas haben. 

## Definition Character Set
- ASCII
7-Bit-Code mit 32 Steuerzeichen und 96 druckbaren Zeichen, auf Englisch ausgerichtet.

- ANSI
SO-8859-1 (Latin1) für Westeuropa, deckt fast alle ASCII-Zeichen ab und codiert zusätzliche internationale Zeichen.

- Unicode
Umfassendster Zeichensatz, der alle Sprachen der Welt unterstützt, mit bis zu 100.000 verschiedenen Zeichen.

- UTF-8
Häufigste Unicode-Kodierung mit variabler Zeichenlänge (1 bis 4 Bytes), wobei die ersten 128 Zeichen mit ASCII identisch sind.

- UTF-16, UTF-32
UTF-16 verwendet 16-Bit-Zeichen (Java), UTF-32 hat eine fixe Zeichenlänge von 32 Bit, was zu hohem Speicherbedarf für ASCII-Zeichen führt.

## Auftrag (Repetition)
CREATE SCHEMA/TABLE (name) -> erstellt tabelle 
DROP TABLE (name) -> löscht Tabelle
ALTER TABLE (name) MODIFY/CHANGE -> Änderungen vornehmen
ALTER TABLE DROP COLUMN (name) -> Attribute etc löschen
ALTER TABLE ADD COLUMN -> Spezialisieren 

## Forward Engineering mit Workbench 
