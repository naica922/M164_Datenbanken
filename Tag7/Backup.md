# Backup

## Datensicherung von Datenbanken
![Datensicherung](image.png)

Daten müssen gesichert werden und backups enthalten, weil viele Firmen sensible Kundendaten und ihren ganzen Inhalt von Datenbanken bekommen. Zusätzlich findet der Datenaustausch statt welcher sehr wichtig ist und geschützt werden soll. Meistens kommt es zu Datenverlüsten wegen technischem Versagen oder einem Benutzerfehler. Damit der Datenverlust nicht irreversibel ist braucht man eine Datensicherung.

## Möglichkeiten zur Sicherung von Datenbanken
Mit Backups kann der Zustand einer Datenbank zum Zeitpunkt der Datensicherung wiederhergestellt werden. Diese speichert man auf einem externen Speichermedium. 

Online Backups: <br>
Werden erzeugt, ohne dass die Datenbank heruntergefahren werden muss
Datenbak nimmt vorgenommene Änderungen in separaten Bereich auf und führt sie erst im Anschluss an die Sicherung in entsprechende Datei ein.

Offline Backup: <br>
Man fährt die Datenbank für die Zeit der Sicherung herunter. 
Hat den Vorteil, dass es unkompliziert ist aber während dem Backup ist die Anwendung oder Webseite nicht verfügbar. 

Drei Arten der Sicherung: <br>
- Voll Backup
Alle Daten und Strukturen, bracuht aber speicher der sehr hoch ist
- Differentielles Backup
Voll Backup wird erstellt, Daten die gesichert werden oder sich verändert haben werden gespeichert. Es braucht weniger Speicherplatz. Die recovery funktioniert nur mit dem letzten voll backup und den differentiellen backup
- Inkrementielles Backup
Nur die Daten werden kopiert, die sich seit der letzen Sicherung geändert haben oder neu sind. Ein inkrementielles Backup bezieht sich immer auf das vorherige. Jede Datei wird nur einmal gesichert und der Speicherplatz geschont

## Backups erzeugen
- MySQL Dump:
Wird mit Shell Zugriff und integrierter Backup Funktion gemacht, nicht alle Hoster erlauben Zugriff auf diese Funktion

- phpMyAdmin:
Administrations Plattforn für SQL Benutzer, man kann die Datenbank in gewünschtem Format exportieren. Bei grossen Datenbanken gefahr vor Abbruch

- BigDump:
Ergänzung zu phpMyAdmin, kann grosse Backups wieder einspielen

- HeidiSQL:
Die Backup-Lösung für Windows-Systeme basiert nicht auf PHP und hat daher keine Probleme mit großen Backups

- Mariabackup:
Open Source Tool, welches von MariaDB bereitgestellt wird damit man physische Online Backups machen kann. Auf Linux und Windows möglich.