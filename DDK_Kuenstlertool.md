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
Das hier zu entwickelnde "Künstlerdokumenttool" soll zwei der wichtigsten 
Eigenschaften einer Künstlerdatei maschinell prüfen und gegebenenfalls ergänzen. Der Personennormdatei der GND und dem VG Bild-Kunst. 

# Künstlerdokumenttool - Ein erster Workflow-Entwurf
## 1. Personenabgleich:
1. Erstelle einen Export aller Künstlerdokumente (KUE-Datei) aus der Erfassungsumgebung der HIDA4 Datenbank in XML 
(?).
2. Suche alle Künstler-Dokumente ab mit mehrfachvergabe von ULAN, GND, VIAF
3. Erstelle eine Liste mit allen doppelt vergebenen IDs zur Bereinigung an die Redaktion
4. Erstelle eine Liste mit allen Künstlerdateien, die noch keine Anbindung an mindestens eine Normdatei haben.
5. Matche alle Künstlerdaten, die noch keine Normdatei haben mit den Personendatensätzen der GND
5a. pattern Match mit: Nachname, Vorname, Geburtsdatum, Sterbedatum, Geburtsort, 

## 2. VG Bild-Kunst Vertretung
2. Ermittel alle Künstlerdokumente ohne VG-Bild-Kunst Eintrag ermittelt.
3. Erstelle ein namens(varianten-) basiertes Matching mittels der entsprechenden CSV-Datei zu Künstlern mit Onlinerechten über www.bildkunst.de/service/kuenstlersuche/online.html
4. Erstelle automatisch bei einem exacten Match einen "VG-Bild-Kunst vertreten" Eintrag in das entsprechende Feld.
5. Generiere eine Liste aller übrig gebliebenen Künstler für ein manuelles Matching.
