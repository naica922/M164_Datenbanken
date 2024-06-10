# Checkpoint
Ref. Integrität: Was ist das? Machen Sie ein Beispiel dazu!
Die Definition von referentieller Integrität ist, dass Beziehungen zwischen Tabellen in einer relationalen Datenbank konsistent bleiben. 
Ein Fremdschlüssel in einer Tabelle verweist immer auf einen gültigen Eintrag in einer anderen Tabelle.

Welche Constraints kann eine Beziehung haben? (Tipp: Mehr als eine!)
Sie kann die Beziehung NOT NULL, UNIQUE, PRIMARY KEY, FOREIGN KEY und CHECK haben

Was ist der Unterschied zwischen LEFT JOIN und RIGHT JOIN?
Left Join gibt alle Datensätze aus der Linken Tabelle und die Passenden aus der rechten zurück wobei right join das gleiche macht aber aus der rechten Tabelle.

Wie wird eine 1:1-Beziehung und eine c:m-Beziehung umgesetzt? Warum?
Durch einen Fremdschlüssel der auch als UNIQUE und NOT NULL geltet. Das durch eine Zwischentabelle welche beide PKs als FKs enthaltet.

Was ist der Nachteil, wenn eine Beziehung nur mit Primär- und Fremdschlüssel definiert werden, d.h. ohne die Constraint-Anweisung?
Es gibt dann keine weiteren Sicherungen bezüglich der Integrität. Es könnten also doppelte Einträge möglich sein oder Null werte in fremdschlüssel spalten.

Welche Folge hat einen Eintrag eines Fremdschlüsselwertes, der als ID-Wert in der verbundenen Tabelle nicht vorhanden ist?
a) mit Contraint-Anweisung auf dem FS
Es gibt einen Fehler aus 
b) ohne Contraint-Anweisung auf dem FS
Er kann eingefügt werden auch wenn der FK nicht existiert