# M164_Datenbanken
## 1. Welche Stufen gibt es bei der Wissenstreppe?
Nennen Sie diese der Reihe nach und machen Sie ein Beispiel mit einem Wechselkurs.<br>
1. Zahlen, Ziffern, Buchstaben, Sonderzeichen<br>
2. Daten (Nachrichten)
3. Informationen (Neuigkeitswert)
4. Wissen
5. Kompetenz<br>
Ein Beispiel ist, dass man bei der ersten Stufe auf eine Webseite geht zum Beispiel von einem Restaurant.<br>
Man sieht einzelne Dinge wie Ziffern, Buchstaben in einem Text, Sonderzeichen oder ein Icon. Wenn wir weiter gehen zu der zweiten Stufe sehen wir Daten.<br>
Diese Daten müssen nicht unbedingt einen logischen Zusammenhang haben und können auch einzelne Wörter etc sein. Die Informationen sind dann der nächste Schritt, welcher logisch ist.<br>
Man kann z.B sehen wann ein Restaurant wo öffnet und wie man dort hinkommt. Dies giltet als Information welche auch Sinn ergibt.<br>
Danach hat man dank diesen Informationen Wissen und kann sich aus diesem eine Kompetenz erarbeiten.<br>
Die Kompetenz in meinem Beispiel könnte sein, dass ich den Bus nehme und zum Reataurant fahre um dort zu essen.

## 2. Wie werden Netzwerk-Beziehungen im logischen Modell abgebildet?
In einem logischen Modell werden die Beziehungen mit sogenannten Foreign Keys und Primary Keys abgebildet.
Es enthält Kardinalitäten etc. Um vom konzeptionellen Model ins logische zu kommen braucht man die Many to Many Verknüpfungstabelle. Das Konzeptionelle Modell enthält diese Tabelle nicht und hat nur Kardinalitäten wie m oder mc.

## 3. Was sind Anomalien in einer Datenbasis? Welche Arten gibt es?
Es sind Abweichungen oder Probleme, die auftreten können, wenn Daten inkonsistent, unvollständig oder nicht korrekt strukturiert sind. Man bezeichnet Anomalien als Ursache für Inkonsistenz in einer Datenbank. 
Diese Anomalien können die Integrität, Konsistenz und Zuverlässigkeit der Daten beeinträchtigen.
Die verschiedenen Arten sind Einfügeanomalien, Löschanomalien, Änderungsanomalien, Suchanomalien, Redundanzanomalien und Inkonsistenzanomalien. Ein Beispiel ist, wenn man von einer Person die Adresse löscht aber noch Tabellen darauf verweisen. 
Anomalien sind fast nicht vermeidbar, man kann sie nur durch Constraints und durch Normalisierung reduzieren. 

## 4. Gibt es redundante "Daten"? Warum?
Ja es gibt redundante Daten. Die Bezeichnung davon sind Daten, welche mehrere Male in der Datenbank gepeichert sind aber grundsätzlich die gleichen darstellen. Ein Beispiel ist, wenn man das Alter als Zahl und als Datum gespeichert hat. 
Sie benötigen unnötig viel Speicherplatz und sorgen für verwirrung sowie ungenauigkeit.
Gründe warum sie vorkommen könnten sein, wenn man manuell Sachen verändert und ausversehen etwas doppelt einträgt oder jemand anderes dies tut.

## 5. Datenstrukturierung:
Datenbanken sind stark strukturiert. <br>

Welche zwei Aspekte können strukturiert werden?<br>
Sie können nach der Internen Struktur oder nach der Externen Struktur strukturiert werden.
Die interne Struktur ist, wie die die Organisation der Daten ist und wie die Daten auf der physischen Ebene gespeichert und verwaltet sind.
Die externe Struktur bezieht sich auf wie sie für Benutzer oder Anwendungen präsentiert werden. Dies ist unabhängig von der physischen Speicherung.

Welche Kategorien (Abstufungen) gibt es bei der Strukturierung?<br>
Es gibt Datenelemente z.B Attribute oder Felder in einer Tabelle.
Danach die Datensätze, was Gruppen von Datenelementen sind und eine einzelne Einheit repräsentieren zum Beispiel eine Zeile in der Tabelle.
Danach kommen die Datenbankobjekte also die Organisation von den Datensätzen und zum Schluss noch die Datenbanken. Datenbanken ist die Organisaion von Datenbankobjekten in einer Hirarchie.

Und wie müssen die Daten in einer DB strukturiert sein?<br>
Die Daten müssen den richtigen Datentyp haben also die Art von den Daten nuss übereinstimmen.
Die Daten sollten normalisiert sein, damit man Redundanzen und Anomalien vermeidet. Also in mehrere kleinere Tabellen unterteilen.
Auch die Beziehungen zwischen den Datenobjekten müssen klar definiert werden und man kann eine Inddexierung verwenden. Dies hat den vorteil, dass man schneller auf bestimmte Datensätze zugreiffen kann.


## 6. Bild Beschriftung
1. Entität -> Name der Tabelle
3. Attribute -> Ortschaft, Alter etc.
2. ID -> Definiert den Datensatz und kann als PK gebraucht werden
2. Zeile
4. Attributwerte
5. Entität


## 7. Constraints
Alle die folgenden Begriffe sind Einschränungen auch Constraints genannt:
Primary Key
Foreign Key
Unique
Not Null
Default 
Check