# Aggregatsfunktionen
Werden verwendet, um Daten in einer Spalte zusammenzufassen oder zu berechnen. 

Funktionen werden in Verbindung mit Group by verwendet werden um Gruppen zu gruppieren und auf diesen zu berechnen oder zusammenfassen

COUNT
Anzahl der Zeilen einer Tabelle oder Gruppe zurück
Beispiel:
```
SELECT COUNT(*) FROM customers;
SELECT COUNT(salary) FROM customers;
```

SUM
Berechnet Summe der Werte in Spalte oder Tabelle
```
SELECT SUM(salary) FROM employees;
```


AVG
Berechnet Durchschnittwert von Spalte oder Tabelle
```
SELECT AVG(salary) FROM employees;
```

MIN
Kleinster Wert ausgeben 
```
SELECT MIN(salary) FROM employees;
```

MAX
grössten Wert ausgeben
```
SELECT MAX(salary) FROM employees;

```