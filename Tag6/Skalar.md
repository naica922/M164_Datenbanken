# Skalare Unterabfrage / Nicht Skalare Unterabfrage

## Skalar:
Eine skalare Unterabfrage gibt nur eine Spalte mit nur einer Zeile zurück. Operatoren wie =, >, >=, < und <= können nur mit skalaren Unterabfragen verwendet werden, sodass die Unterabfrage skalar sein muss. Zum Beispiel, wenn ein Kunde prüfen möchte, ob es günstigere Tickets gibt als ein Paris-Bariloche-Ticket, kann er die folgende Abfrage nutzen:

´´´
SELECT city_destination, ticket_price, travel_time, transportation FROM one_way_ticket
  WHERE ticket_price < (
      SELECT ticket_price FROM one_way_ticket
      WHERE city_destination = 'Bariloche' AND city_origin = 'Paris'
  )
  AND city_origin = 'Paris';
´´´

## Nicht Skalar:
Eine nicht-skalare Unterabfrage gibt mehrere Zeilen und Spalten zurück. Sie wird häufig mit Operatoren wie IN oder EXISTS verwendet, um komplexere Bedingungen in der Hauptabfrage zu ermöglichen. Ein Beispiel ist die Abfrage von Benutzern aus europäischen Ländern:

´´´
SELECT name, age, country
FROM users
WHERE country IN (
    SELECT name FROM country WHERE region = 'Europa'
);

´´´