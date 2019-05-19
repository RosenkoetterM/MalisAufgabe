# Die Arbeitsumgebung

Das Deutsche Dokumentationszentrum für Kunstgeschichte Bildarchiv Foto Marburg (DDK) erfasst Kunst- und Architektur-Objekte für die Online-Publikation www.bildindex.de. Das dabei verwendete Erfassungssystem HiDA4 ist eine hierarchische SQL-Datenbank, mit der man 
unterschiedliche Dokumenttypen erfassen kann. Kunst- und Architektur-Objekte werden in der Objekt-Dokumenttyp, das auch Hauptdokumenttyp ist, erfasst. Daran angeknüpft sind Seitendokumente, die für das kontrollierte Vokabular sorgen in Form einer Thesaurusdatei, 
oder weitere Entitäten wie Georeferenzierungen, Künstler oder Werkstätten.
Die Erfassung folgt nach dem Regelwerk: MIDAS (Marburger Index). 

# Ideen

Zwei Ideen stehen zur Auswahl, wobei Idee 1 mein Favorit ist. 

## 1. VG Bild-Kunst Vertretung Matching
Das Regelwerk sieht vor, dass wenn ein Künstler im Objekt-Dokument erfasst wird, dieser auch im Künstlerdokument (Seitendokument) angelegt sein muss. In diesem müssen folgende Felder ausgefüllt sein: 
beforzugte und gegebenfalls alternative Namenansetzung, Geburtsdaten und Geburtsort, sowie der Urheberechtsvermerk. Letzterer steuert unter Anderen im Online-Portal Bildindex, ob die Objekte zum Künstler im Internet gezeigt werden dürfen, oder nicht. Bislang gibt 
es kein (semi-)maschinelles Verfahren, das das Urheberrechtsmanagement steuert. 

### Redaktionelle Vorteile durch ein semi-maschinelles Verfahren
Derzeit gibt es rund 98330 Künstlerdokumente in der HIDA-Datenbank. Die Prüfung des VG-Bild-Kunst Eintrages 
erfolgt bislang lediglich manuell bei der Erstellung neuer Künstlerdokumente. Eine komplett intelektuelle Prüfung ist bei der 
Datenmenge nicht zumutbar. Da das Rechtemanagement essentiell für die Online-Publikation der bebilderten Objekte 
ist, sollte ein semi-maschinelles Verfahren einen großteil des Bestandes ohne viel Arbeitszeit zu verbrauchen die 
redaktionelle Arbeit unterstützen. Zudem wird das bisherige Erfassungssystem HIDA4 demnächst auf APS migrieren. Dazu werden nach und nach alle Dokumentstypen geprüft. Bislang wurde nur ein Doublettenabgleich 
bei den Künstlerdokumenten vorgenommen, eine Einschätzung weiterer Fehlerpotentiale ist demnach notwendig. 
 
# Vorgehensweisen
## zu 1.:
1. Erstelle einen Export aller Künstlerdokumente (KUE-Datei) aus der Erfassungsumgebung der HIDA4 Datenbank in XML (?). 
2. Erstelle ein Skript, dass alle Künstlerdokumente ohne VG-Bild-Kunst Eintrag ermittelt.
3. Erstelle ein namens(varianten-) basiertes Matching mittels der entsprechenden CSV-Datei zu Künstlern mit Onlinerechten über www.bildkunst.de/service/kuenstlersuche/online.html
4. Erstelle automatisch bei einem exacten Match einen "VG-Bild-Kunst vertreten" Eintrag in das entsprechende Feld.
5. Generiere eine Liste aller übrig gebliebenen Künstler für ein manuelles Matching.
