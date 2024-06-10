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
-- Alle Lieferanten, die ihren Sitz in Freiburg haben:
 
SELECT l.name AS Lieferantenname, o.name AS Lieferantenort, o.postleitzahl AS Postleitzahl
FROM lieferanten l
JOIN orte o ON l.orte_orte_id = o.orte_id
WHERE o.name = 'Freiburg';
 
-- Alle Verlage, die ihren Sitz in München haben:
SELECT v.name AS Verlagsname, o.name AS Verlagsort
FROM verlage v
JOIN orte o ON v.orte_orte_id = o.orte_id
WHERE o.name = 'München';
 
-- Alle Bücher, die im Verlag Assal erschienen sind:
SELECT b.titel AS Buchtitel, b.erscheinungsjahr AS Erscheinungsjahr, v.name AS Verlagsname
FROM buecher b
JOIN verlage v ON b.verlage_verlage_id = v.verlage_id
WHERE v.name = 'Assal'
ORDER BY b.erscheinungsjahr DESC;
 
-- Alle Bücher des Lieferanten Schustermann:
SELECT b.titel AS Buchtitel, l.name AS Lieferantenname
FROM buecher b
JOIN buecher_has_lieferanten bl ON b.buecher_id = bl.buecher_buecher_id
JOIN lieferanten l ON bl.lieferanten_lieferanten_id = l.lieferanten_id
WHERE l.name = 'Schustermann';
 
-- Alle Thriller:
SELECT b.titel AS Buchtitel, s.bezeichnung AS Sparte
FROM buecher b
JOIN buecher_has_sparten bs ON b.buecher_id = bs.buecher_buecher_id
JOIN sparten s ON bs.sparten_sparten_id = s.sparten_id
WHERE s.bezeichnung = 'Thriller'
ORDER BY b.titel;
 
-- Alle Liebesromane:
SELECT b.titel AS Buchtitel, s.bezeichnung AS Sparte, v.name AS Verlagsname
FROM buecher b
JOIN buecher_has_sparten bs ON b.buecher_id = bs.buecher_buecher_id
JOIN sparten s ON bs.sparten_sparten_id = s.sparten_id
JOIN verlage v ON b.verlage_verlage_id = v.verlage_id
WHERE s.bezeichnung = 'Liebe'
ORDER BY b.titel ASC;
 
-- Alle Bücher von Sabrina Müller:
SELECT a.nachname AS Autorennachname, a.vorname AS Autorenvorname, b.titel AS Buchtitel
FROM autoren a
JOIN autoren_has_buecher ab ON a.autoren_id = ab.autoren_autoren_id
JOIN buecher b ON ab.buecher_buecher_id = b.buecher_id
WHERE a.vorname = 'Sabrina' AND a.nachname = 'Müller'
ORDER BY b.titel DESC;
 
-- Alle Thriller von Sabrina Müller:
SELECT a.vorname AS Autorenname, b.titel AS Buchtitel, s.bezeichnung AS Sparte
FROM autoren a
JOIN autoren_has_buecher ab ON a.autoren_id = ab.autoren_autoren_id
JOIN buecher b ON ab.buecher_buecher_id = b.buecher_id
JOIN buecher_has_sparten bs ON b.buecher_id = bs.buecher_buecher_id
JOIN sparten s ON bs.sparten_sparten_id = s.sparten_id
WHERE a.vorname = 'Sabrina' AND a.nachname = 'Müller' AND s.bezeichnung = 'Thriller';
 
-- Alle Bücher von Sabrina Müller, die in die Sparten Thriller oder Humor eingeordnet werden können:
SELECT a.vorname AS Autorenname, b.titel AS Buchtitel, GROUP_CONCAT(s.bezeichnung SEPARATOR ', ') AS Sparte
FROM autoren a
JOIN autoren_has_buecher ab ON a.autoren_id = ab.autoren_autoren_id
JOIN buecher b ON ab.buecher_buecher_id = b.buecher_id
JOIN buecher_has_sparten bs ON b.buecher_id = bs.buecher_buecher_id
JOIN sparten s ON bs.sparten_sparten_id = s.sparten_id
WHERE a.vorname = 'Sabrina' AND a.nachname = 'Müller' AND (s.bezeichnung = 'Thriller' OR s.bezeichnung = 'Humor')
GROUP BY b.titel
ORDER BY b.titel;
```