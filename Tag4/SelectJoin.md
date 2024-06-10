# Select Join 
Auftrag Select JOIN:
```
SELECT kunden.name, orte.plz, orte.ort_name
FROM kunden
JOIN orte ON kunden.ort_id = orte.ort_id;
 
SELECT kunden.name, orte.ort_name
FROM kunden
JOIN orte ON kunden.ort_id = orte.ort_id
WHERE orte.plz = 79312;
 
SELECT kunden.name, orte.ort_name
FROM kunden
JOIN orte ON kunden.ort_id = orte.ort_id
WHERE orte.ort_name = 'Emmendingen';
 
SELECT kunden.name, orte.ort_name, orte.einwohner
FROM kunden
JOIN orte ON kunden.ort_id = orte.ort_id
WHERE orte.einwohner > 70000;
 
SELECT ort_name
FROM orte
WHERE einwohner < 1000000;
 
SELECT kunden.name, orte.ort_name
FROM kunden
JOIN orte ON kunden.ort_id = orte.ort_id
WHERE orte.einwohner BETWEEN 100000 AND 1500000;
 
SELECT kunden.name, orte.plz, orte.ort_name
FROM kunden
JOIN orte ON kunden.ort_id = orte.ort_id
WHERE kunden.name LIKE '%e%' AND (orte.ort_name LIKE '%u%' OR orte.ort_name LIKE '%r%');
```

Kartesisches Produkt: Erklären Sie in eigenen Worten, warum diese Abfrage kein sinnvolles Ergebnis gibt:
 ```
	SELECT * FROM kunden
	INNER JOIN orte;
```

Überflüssige Datenmenge: Das Ergebnis enthält eine Vielzahl von Zeilen, die in den meisten Anwendungen keine Bedeutung haben. Durch die Kombination jeder Zeile der Kunden-Tabelle mit jeder Zeile der Orte-Tabelle entsteht eine sehr grosse und irrelevante Datenmenge.
 
Fehlender logischer Zusammenhang: Die Daten weisen keine klare Beziehung auf, da die Kombinationen keine Bedeutung haben. Es fehlt an Informationen darüber, welche Kunden mit welchen Orten in Verbindung stehen.

Auftrag Select JOIN Fortgeschrittenb:
```

```