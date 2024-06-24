# Checkpoint 

## Nennen Sie die fünf Aspekte der Datenintegrität in einer Datenbank.

Entity-Integrität: Sicherstellung, dass jede Tabelle einen Primärschlüssel hat, der einzigartig und nicht NULL ist.

Referentielle Integrität: Gewährleistung, dass Beziehungen zwischen Tabellen korrekt sind und Fremdschlüssel auf gültige Datensätze verweisen.

Domänen-Integrität: Sicherstellung, dass alle Spaltenwerte innerhalb vordefinierter Bereiche (Domänen) liegen und den Datentypen entsprechen.

Benutzerdefinierte Integrität: Durchsetzen von Regeln, die spezifisch für die Anwendung oder das Geschäftsszenario sind.

Zeitliche Integrität: Sicherstellung, dass Daten zeitlich korrekt und aktuell sind.

## Was ist der Unterschied zwischen Datenintegrität und Datenkonsistenz?

- Datenintegrität bezieht sich auf die Richtigkeit und Zuverlässigkeit der Daten innerhalb einer Datenbank und wird durch Regeln wie Primärschlüssel, Fremdschlüssel, Domänen und benutzerdefinierte Regeln gewährleistet.

- Datenkonsistenz bedeutet, dass alle Kopien eines bestimmten Datenwertes denselben Wert aufweisen, was insbesondere bei verteilten Datenbanken wichtig ist. Es stellt sicher, dass keine widersprüchlichen Daten innerhalb der Datenbank oder zwischen verteilten Datenbanken vorhanden sind.


## Was ist die Gefahr bei der FK-Constraint-Option ON DELETE Cascade?

Die Gefahr der Verwendung von ON DELETE Cascade besteht darin, dass das Löschen eines Datensatzes in einer Tabelle dazu führen kann, dass alle verknüpften Datensätze in anderen Tabellen ebenfalls gelöscht werden. Dies kann unbeabsichtigt zu einem massiven Datenverlust führen, wenn nicht sorgfältig darauf geachtet wird, welche Datensätze gelöscht werden.


## Was ist der Unterschied zwischen COUNT(*) und COUNT(attr)?

- COUNT(*) zählt die Anzahl der Zeilen in einer Tabelle, unabhängig davon, ob die Zeilen NULL-Werte in irgendeiner Spalte enthalten.

- COUNT(attr) zählt die Anzahl der Zeilen, bei denen der angegebene Attributwert (Spaltenwert) nicht NULL ist.

## Formuliere einen SELECT-Befehl mit der WHERE BETWEEN Klausel.
```
SELECT *
FROM orders
WHERE order_date BETWEEN '2023-01-01' AND '2023-12-31';
```

## Worauf müssen Sie bei der HAVING Klausel achten? 
Aggregatfunktionen: HAVING wird verwendet, um Bedingungen auf aggregierte Daten anzuwenden, die durch Funktionen wie SUM, AVG, COUNT, MAX, MIN usw. erzeugt werden.

GROUP BY: Die HAVING-Klausel wird immer in Verbindung mit GROUP BY verwendet, um die aggregierten Ergebnisse nach der Gruppierung zu filtern.

Reihenfolge: HAVING kommt immer nach GROUP BY und vor ORDER BY in einer SQL-Abfrage.