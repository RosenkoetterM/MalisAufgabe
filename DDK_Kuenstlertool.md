# Die Arbeitsumgebung

Das Deutsche Dokumentationszentrum für Kunstgeschichte Bildarchiv Foto Marburg (DDK) erfasst Kunst- und Architektur-Objekte für die Online-Publikation www.bildindex.de. Das dabei verwendete Erfassungssystem HiDA4 ist eine  SQL-Datenbank, mit der man 
unterschiedliche Dokumenttypen erfassen kann. Kunst- und Architektur-Objekte werden in der Objekt-Dokumenttyp, das auch Hauptdokumenttyp ist, erfasst. Daran angeknüpft sind Seitendokumente, die für das kontrollierte Vokabular in Form einer Thesaurusdatei, 
oder weitere Entitäten wie Georeferenzierungen, Künstler oder Werkstätten sorgen.
Die Erfassung folgt nach dem Regelwerk: MIDAS (Marburger Index). Das Regelwerk sieht vor, dass wenn ein Künstler im Objekt-Dokument erfasst wird, dieser auch im Künstlerdokument (Seitendokument) angelegt sein muss. In diesem müssen folgende Felder ausgefüllt sein: 
beforzugte und gegebenfalls alternative Namenansetzung, Geburtsdaten und Geburtsort, sowie der Urheberechtsvermerk
und falls vorhanden die Personennormdatei der GND. Der VG Bild-Kunst Eintrag ist essentiell für das Rechtemanagement,
denn es regelt unter anderem die Bildrechte für die Online-Publikation www.bildindex.de. Der GND-Eintrag ist mittlerweile soweit vorhanden obligatorisch und Grundlage von Linked Open Data als Teil der digitalen Strategie im Haus.

Im Zuge der Migration von der bisherigen Arbeitsumgebung HiDA4 auf APS, werden alle Dokumenttypen auf ihre Vollständigkeit und Plausibilität geprüft. 

## Redaktionelle Vorteile durch ein semi-maschinelles Verfahren
Derzeit gibt es rund 98330 Künstlerdokumente in der HIDA-Datenbank. Die Prüfung von VG-Bild-Kunst und der Personennormdatei erfolgt 
bislang manuell bei der Erstellung neuer Künstlerdokumente. Eine komplett intelektuelle Prüfung aller bisherigen Künstlerdokumente auf ihre Vollständigkeit und Plausibilität, ist bei der Datenmenge und aufgrund von Ressourcenknappheit nicht zumutbar. 

## Ziel
Das hier zu entwickelnde "Künstlerdokumenttool" soll zwei der wichtigsten Eigenschaften einer Künstlerdatei maschinell prüfen und gegebenenfalls ergänzen. Der Personennormdatei der GND und dem VG Bild-Kunst. 

# Künstlerdokumenttool - Ein erster Workflow-Entwurf
## 1. Personenabgleich:
1. Erstelle einen Export aller Künstlerdokumente (KUE-Datei) aus der Erfassungsumgebung der HIDA4 Datenbank in XML. http://versand.fotomarburg.de/KUE20190523.zip
1.a. Zeichensatz UTF-8 aber Codes für Sonderzeichen (^B) müssen umgewandelt werden mit midasCorereplacementMap.xslt
2. Suche alle Künstler-Dokumente ab mit Mehrfachvergabe von ULAN, GND, VIAF.
3. Erstelle eine Liste mit allen doppelt vergebenen IDs zur Bereinigung an die Redaktion
3.a. Generierte Liste im Exel-Format an Redaktion per Mail.
4. Erstelle eine Liste mit allen Künstlerdateien, die noch keine Anbindung an mindestens eine Normdatei haben.
5. Matche alle Künstlerdaten, die noch keine Normdatei haben mit den Personendatensätzen der GND https://data.dnb.de/opendata/
5a. pattern Match mit:

 | Bezeichnung | HiDA4 Feldnummer | Beispiel | Kommentar |
 | --- | --- | ---| --- |
 | KUE-Dok.-Nr. | 3000 | 02553162 | Interne Dokumentnummer, die nicht doppelt vorkommen darf. |
 | Norm-ID-NR. | 30gn | gnd118597787 | Die eigentliche GND-Nummer wird nicht als URI abgelegt, sonder als reine ID mit dem Präfix der jeweiligen Normdatei. |
 | Künstlername | 3100 | Raffael | Normierter Ansetzung nach: Nachname, Vorname|
 | Zweitname | 3105 | Santi, Raffaello & Sanzio, Raffaello & Sanzio, Raffaele & Raffaello Santi & Raphael Urbinas & Raphaello | Normierte Ansetzung nach: Nachname, Vornahme; Aufzählzeichen: & |
 | Geburtsdatum | 3270 | 1483.03.26/1483.03.28 | Standard ISO 8601 Norm (JJJJ-MM-DD) wird nicht eingehalten. Alternatives Datum: */* (semantisches *oder* in Midas).
 | Sterbedatum | 3330 | 1520.04.06 | siehe Geburtsdatum |
 | Geburtsort | 3290 | Urbino? | Sollen Fragezeichen generell hier ignoriert werden? |
 

## 2. VG Bild-Kunst Vertretung
2. Ermittel alle Künstlerdokumente ohne VG-Bild-Kunst Eintrag. (Feld 3189: gemeinfrei)
3. Erstelle ein namens(varianten-) basiertes Matching mittels der entsprechenden CSV-Datei zu Künstlern mit Onlinerechten über http://www.bildkunst.de/service/kuenstlersuche/onlinerechte.html
3.a. unter Ausschlusskriterium: gemeinfreie Künstler (Sterbedatum <x); 
3.b. Problem: VG-Bild hat keine Lebensdaten. Ein maschineller Match kann zu falschen Ergebnissen führen.
4. Erstelle automatisch bei einem exacten Match einen "VG-Bild-Kunst vertreten" Eintrag in das entsprechende Feld.
5. Generiere eine Liste aller übrig gebliebenen Künstler für ein manuelles Matching.

## Offene Fragen
* zu 1.1.: Wäre es ratsam mit einer kleineren Testmenge an Künstlerdaten zu arbeiten?
> Ja. siehe 2.3.a
* zu 1.2.: Ist es evtl. sinnvoller sich nunächst nur auf GND zu fokussieren?
* zu 1.3.a.: Kann es hier zu Problemen mit ASCII kommen? Zeichenumsetzung von HiDA4 ist hierbei problematisch. Auf was muss ich achten? Siehe dazu Tabelle 1.5.a. Kommentar zu Zweitname und Geburtsdatum.
> Es gibt eine Matching-Tabelle (HiDa nach UTF-8)
* zu 1.5.: Bislang gibt es noch keine Schnittstelle zum Abrufen oder Bereitstellen der Daten. Wie hole ich mir die csv-Dateien aktuell herunter?
> Es liegen Textdaten vor: Hida: XML-Dump, VG Bild: CSV. Vorschlag zum Vorgehen: HiDA in BaseX und VG Bild in SQL-DB bringen und über eine API abfragen.
* zu 1.5.a.: Wenn weder Geburts- noch Sterbedatum vorhanden sind sollte die erste (3300) und letzte Erwähnung (3360) abgefragt werden?
> Wird im besten Falle nicht notwendig sein.

