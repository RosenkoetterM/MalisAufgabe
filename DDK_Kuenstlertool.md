# Die Arbeitsumgebung

Das Deutsche Dokumentationszentrum für Kunstgeschichte Bildarchiv Foto Marburg (DDK) erfasst Kunst- und Architektur-Objekte für die Online-Publikation www.bildindex.de. Das dabei verwendete Erfassungssystem HiDA4 ist eine hierarchische SQL-Datenbank, mit der man 
unterschiedliche Dokumenttypen erfassen kann. Kunst- und Architektur-Objekte werden in der Objekt-Dokumenttyp, das auch Hauptdokumenttyp ist, erfasst. Daran angeknüpft sind Seitendokumente, die für das kontrollierte Vokabular in Form einer Thesaurusdatei, 
oder weitere Entitäten wie Georeferenzierungen, Künstler oder Werkstätten sorgen.
Die Erfassung folgt nach dem Regelwerk: MIDAS (Marburger Index). Das Regelwerk sieht vor, dass wenn ein Künstler im Objekt-Dokument erfasst wird, dieser auch im Künstlerdokument (Seitendokument) angelegt sein muss. In diesem müssen folgende Felder ausgefüllt sein: 
beforzugte und gegebenfalls alternative Namenansetzung, Geburtsdaten und Geburtsort, sowie der Urheberechtsvermerk
und falls vorhanden die Personennormdatei der GND. Der VG Bild-Kunst Eintrag ist essentiell für das Rechtemanagement,
denn es regelt unter anderem die Bildrechte für die Online-Publikation www.bildindex.de. Der GND-Eintrag ist mittlerweile obligatorisch und Grundlage von Linked Open Data als Teil der digitalen Strategie im Haus.

Im Zuge der Migration von der bisherigen Arbeitsumgebung HiDA4 auf APS, werden alle Dokumenttypen auf ihre Vollständigkeit und Plausibilität geprüft. 

## Redaktionelle Vorteile durch ein semi-maschinelles Verfahren
Derzeit gibt es rund 98330 Künstlerdokumente in der HIDA-Datenbank. Die Prüfung von VG-Bild-Kunst und der Personennormdatei erfolgt 
bislang manuell bei der Erstellung neuer Künstlerdokumente. Eine komplett intelektuelle Prüfung aller bisherigen Künstlerdokumente auf ihre Vollständigkeit und Plausibilität, ist bei der Datenmenge und aufgrund von Ressourcenknappheit nicht zumutbar. 

## Ziel
Das hier zu entwickelnde "Künstlerdokumenttool" soll zwei der wichtigsten Eigenschaften einer Künstlerdatei maschinell prüfen und gegebenenfalls ergänzen. Der Personennormdatei der GND und dem VG Bild-Kunst. 

# Künstlerdokumenttool - Ein erster Workflow-Entwurf
## 1. Personenabgleich:
1. Erstelle einen Export aller Künstlerdokumente (KUE-Datei) aus der Erfassungsumgebung der HIDA4 Datenbank in XML.
2. Suche alle Künstler-Dokumente ab mit Mehrfachvergabe von ULAN, GND, VIAF.
3. Erstelle eine Liste mit allen doppelt vergebenen IDs zur Bereinigung an die Redaktion
3.a. Generierte Liste im Exel-Format an Redaktion per Mail.
4. Erstelle eine Liste mit allen Künstlerdateien, die noch keine Anbindung an mindestens eine Normdatei haben.
5. Matche alle Künstlerdaten, die noch keine Normdatei haben mit den Personendatensätzen der GND
5a. pattern Match mit: 
 | Bezeichnung | HiDA4 Feldnummer | Beispiel | Kommentar |
 | --- | --- | ---| --- |
 | KUE-Dok.-Nr. | 3000 | 02553162 | Interne Dokumentnummer, die nicht doppelt vorkommen darf. |
 | Künstlername | 3100 | Raffael | Normierter Ansetzung nach: Nachname, Vorname|
 | Zweitname | 3105 | Santi, Raffaello & Sanzio, Raffaello & Sanzio, Raffaele & Raffaello Santi & Raphael Urbinas & Raphaello | Normierte Ansetzung nach: Nachname, Vornahme; Aufzählzeichen: & |
 | Geburtsdatum | 3270 | 1483.03.26/1483.03.28 | Standard ISO Norm (yyyy-mm-dd) wird nicht eingehalten. Alternatives Datum: */* (semantisches *oder* in Midas).
 | Sterbedatum | 3330 | 1520.04.06 | siehe Geburtsdatum |
 | Geburtsort | 3290 | Urbino? | Sollen Fragezeichen generell hier ignoriert werden? |
 | Norm-ID-NR. | 30gn | gnd118597787 | Die eigentliche GND-Nummer wird nicht als URI abgelegt, sonder als reine ID mit dem Präfix der jeweiligen Normdatei. |

## 2. VG Bild-Kunst Vertretung
2. Ermittel alle Künstlerdokumente ohne VG-Bild-Kunst Eintrag ermittelt.
3. Erstelle ein namens(varianten-) basiertes Matching mittels der entsprechenden CSV-Datei zu Künstlern mit Onlinerechten über www.bildkunst.de/service/kuenstlersuche/online.html
4. Erstelle automatisch bei einem exacten Match einen "VG-Bild-Kunst vertreten" Eintrag in das entsprechende Feld.
5. Generiere eine Liste aller übrig gebliebenen Künstler für ein manuelles Matching.

## Offene Fragen
zu 1.1.: Wäre es ratsam mit einer kleineren Testmenge an Künstlerdaten zu arbeiten?
zu 1.2.: Ist es evtl. sinnvoller sich nunächst nur auf GND zu fokussieren?
zu 1.3.a.: Kann es hier zu Problemen mit ASCII kommen? Zeichenumsetzung von HiDA4 ist hierbei problematisch. Auf was muss ich achten? Siehe dazu Tabelle 1.5.a. Kommentar zu Zweitname und Geburtsdatum.
zu 1.5.: Bislang gibt es noch keine Schnittstelle zum Abrufen oder Bereitstellen der Daten. Wie hole ich mir die csv-Dateien aktuell herunter?
zu 1.5.a.: Wenn weder Geburts- noch Sterbedatum vorhanden sind sollte die erste (3300) und letzte Erwähnung (3360) abgefragt werden?


