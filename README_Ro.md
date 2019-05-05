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
 
## 2. Erstelle eine Plausibilitätsprüfung, die im Objekt-Dokument prüft, ob ein Objekt, das Sammlungsgegenstand ist, oder war einen Künster- oder Werkstatteintrag hat. 
Das Regelwerk sieht vor, dass innerhalb eines Objektdatensatzes, sofern es sich um einen aktuellen oder ehemaligen Sammlungsgegenstand handelt, immer ein Künstler- oder ein Werkstatteintrag vorhanden sein muss. Ist dieser nicht vorhanden, so muss zumindest eine 
Datierung und ein Eintrag im Feld 5130 (stilistisch-geografische Herkunft) im Datensatz vorliegen.

### Redaktioneller Vorteil
Die Generierung einer Liste von unvollständigen oder fehlerhaften Objekt-Dateien mit den geschilderten Anforderungen, kann die bisherige Erfassungsumgebung nicht selber leisten. Um die Redaktion in ihrer Arbeit zu unterstützen, würde ein maschinelles Verfahren 
zur Erstellung einer solchen Liste viel Zeit ersparen. Das Ergänzen der fehlenden Einträge kann jedoch nur manuell erfolgen. 
  
# Vorgehensweisen
## zu 1.:
1. Erstelle einen Export aller Künstlerdokumente (KUE-Datei) aus der Erfassungsumgebung der HIDA4 Datenbank in XML (?). 
2. Erstelle ein Skript, dass alle Künstlerdokumente ohne VG-Bild-Kunst Eintrag ermittelt.
3. Erstelle ein namens(varianten-) basiertes Matching mittels der entsprechenden CSV-Datei zu Künstlern mit Onlinerechten über www.bildkunst.de/service/kuenstlersuche/online.html
4. Erstelle automatisch bei einem exacten Match einen "VG-Bild-Kunst vertreten" Eintrag in das entsprechende Feld.
5. Generiere eine Liste aller übrig gebliebenen Künstler für ein manuelles Matching.

## zu 2.:
1. Filter in HiDA4 alle Objektdokumente, die Sammlungsdokumente sind oder waren (Feld: ob28 besetzt).
2. Exportiere die Datei im XML-Format.
3. Schreibe ein Skript, dass alle Objekte herausfilter, die keinen Künstler- oder Werkstatteintrag haben (ob30/3100 unbesetzt) und denen ein Eintrag im Datierungsfeld (5060), sowie in Feld 5130 (stilistisch-geografische Herkunft) fehlt.
4. Erstelle eine Liste aller Objekte auf die Nr.3 zutrifft.

## Diskussion:
zu 1.: Ich werde nicht drum herum kommen Teile dieser Vorgehensweise händisch zu machen. Der Export aus HIDA, der Download aus VG-Bild-Kunst, oder gibt es da noch andere Möglichkeiten?

allgemein: Welches der beiden Varianten findest du besser @pdinger?
