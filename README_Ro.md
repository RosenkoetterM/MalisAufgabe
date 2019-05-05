#Die Arbeitsumgebung
Das Deutsche Dokumentationszentrum für Kunstgeschichte Bildarchiv Foto Marburg (DDK) erfasst Kunst- und Architektur-Objekte für die Online-Publikation www.bildindex.de. Das dabei verwendete Erfassungssystem HiDA4 ist eine hierarchische SQL-Datenbank, mit der man 
unterschiedliche Dokumenttypen erfassen kann. Kunst- und Architektur-Objekte werden in der Objekt-Dokumenttyp, das auch Hauptdokumenttyp ist, erfasst. Daran angeknüpft sind Seitendokumente, die für das kontrollierte Vokabular sorgen in Form einer Thesaurusdatei, 
oder weitere Entitäten wie Georeferenzierungen, Künstler oder Werkstätten.
Die Erfassung folgt nach dem Regelwerk: MIDAS (Marburger Index). 

#Ideen
Zwei Ideen stehen zur Auswahl, wobei Idee 1 mein Favorit ist
## 1. VG Bild-Kunst Vertretung Matching
Das Regelwerk sieht vor, dass wenn ein Künstler im Objekt-Dokument erfasst wird, dieser auch im Künstlerdokument (Seitendokument) angelegt sein muss. In diesem müssen folgende Felder ausgefüllt sein: 
beforzugte und gegebenfalls alternative Namenansetzung, Geburtsdaten und Geburtsort, sowie der Urheberechtsvermerk. Letzterer steuert unter Anderen im Online-Portal Bildindex, ob die Objekte zum Künstler im Internet gezeigt werden dürfen, oder nicht. Bislang gibt 
es kein (semi-)maschinelles Verfahren, das das Urheberrechtsmanagement steuert. 

## 2. Erstelle eine Plausibilitätsprüfung, die im Objekt-Dokument prüft, ob ein Objekt, das Sammlungsgegenstand ist, oder war einen Künster- oder Werkstatteintrag hat. 
Das Regelwerk sieht vor, dass innerhalb eines Objektdatensatzes, sofern es sich um einen aktuellen oder ehemaligen Sammlungsgegenstand handelt, immer ein Künstler- oder ein Werkstatteintrag vorhanden sein muss. Ist dieser nicht vorhanden, so muss zumindest eine 
Datierung und ein Eintrag im Feld 5130 (stilistisch-geografische Herkunft) im Datensatz vorliegen.
  
#Vorgehensweisen
##zu 1.:
1. Erstelle einen Export aller Künstlerdokumente (KUE-Datei) aus der Erfassungsumgebung der HIDA4 Datenbank in XML (?). 
2. Erstelle ein Skript, dass alle Künstlerdokumente ohne VG-Bild-Kunst Eintrag ermittelt.
3. Erstelle ein namens(varianten-) basiertes Matching mittels der entsprechenden CSV-Datei zu Künstlern mit Onlinerechten über www.bildkunst.de/service/kuenstlersuche/online.html
4. Erstelle automatisch bei einem exacten Match einen "VG-Bild-Kunst vertreten" Eintrag in das entsprechende Feld.
5. Generiere eine Liste aller übrig gebliebenen Künstler für ein manuelles Matching.

### Diskussion:
Ich werde nicht drum herum kommen Teile dieser Vorgehensweise händisch zu machen. Der Export aus HIDA, der Download aus VG-Bild-Kunst, oder gibt es da noch andere Möglichkeiten?


##zu 2.:
1. Filter in HiDA4 alle Objektdokumente, die Sammlungsdokumente sind oder waren (Feld: ob28 besetzt).
2. Exportiere die Datei im XML-Format.
3. Schreibe ein Skript, dass alle Objekte herausfilter, die keinen Künstler- oder Werkstatteintrag haben (ob30/3100 unbesetzt) und denen ein Eintrag im Datierungsfeld (5060), sowie in Feld 5130 (stilistisch-geografische Herkunft) fehlt.
4. Erstelle eine Liste aller Objekte auf die Nr.3 zutrifft.


