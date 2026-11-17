# PLAN – LaserPrep
*unfold your ideas*

## Idee
Eine kleine Web-App für Architekturstudierende: Man lädt ein 3D-Modell (OBJ, z. B. aus Archicad) hoch,
die App legt jedes Bauteil (Wand, Decke, Boden, Fassadenplatte) flach hin und erzeugt daraus eine
Laserdatei (SVG und DXF) für den Modellbau – im gewünschten Maßstab und mit Laser-Farbcodierung.

## So funktioniert es (für Nicht-Programmierer erklärt)
1. **Hochladen:** Du ziehst eine OBJ-Datei in die App. Das Modell ist im CAD im Maßstab 1:1 gezeichnet.
2. **Zerlegen:** Jedes Objekt in der OBJ-Datei gilt als eine Platte. Die App sucht die größte Fläche der
   Platte (z. B. die Wandvorderseite) und „klappt" sie flach auf den Tisch.
3. **Umriss zeichnen:** Von dieser Fläche nimmt die App nur die Außenkante und die Löcher
   (Fenster, Türen) – das sind die Schnittlinien.
4. **Skalieren:** Alles wird auf den gewählten Modellmaßstab (1:50, 1:100, 1:200 …) verkleinert.
5. **Anordnen:** Die Teile werden nebeneinander auf die Materialplatte gelegt (Größe einstellbar).
   Passt nicht alles drauf, kommt eine zweite Platte dazu. Alles so platzsparend wie möglich.
6. **Exportieren:** Download als SVG und DXF, Schnittlinien rot (R 255), Anritzlinie blau (B255), Orientierungslinie gelb (R255 G255) und schwarz als Gravur, Flächen oder Schriften mit Flächenfüllung. Bei der Schriftart darauf achten, dass diese in Auto-CAD hinterlegt ist. Linienstärke 0,00 mm (Haarlinie)
7. **Anpassungen** die bei Punkt 6 genannten Farben sind die Standardeinstellungen, man kann sie aber auch individuell ändern.

## MVP – Must, Should, Could

### Must (läuft am Freitag)
- [x] OBJ-Datei hochladen und 3D-Vorschau anzeigen
- [x] Jedes Objekt als Platte erkennen und flach legen (Umriss + Öffnungen)
- [x] Maßstab wählen (1:50, 1:100, 1:200, frei)
- [ ] Doppelte/überlappende Linien automatisch entfernen
- [ ] Farbcodierung: Rot (Haarlinie 0,00 mm) = Schneiden, Blau = Anritzen, Gelb = Orientierungsrahmen, Schwarz = Gravur (Farben als Standard kann man aber auch individuell ändern)
- [ ] Materialplatte frei einstellbar (Breite × Höhe in mm), Teile automatisch darauf verteilen *(teilweise: mehrere Sorten und Platten, Teile zeilenweise; wirklich platzsparend fehlt noch)*
- [x] 2D-Vorschau der Laserplatte(n) im Browser
- [ ] Export als SVG und DXF *(SVG fertig, DXF fehlt)*

### Should (wäre gut)
- [x] Aufbau als Bento-Grid: 7 Schritte nacheinander abfragen (01 Pappe, 02 Datei, 03 Maßstab, 04 Farben, 05 Gehrung, 06 Bauteile, 07 Vorschau)
- [x] Mehrere Pappsorten (Name, Größe, Dicke, Anzahl) und mehrere Platten
- [ ] Farben individuell zuordnen (Funktion ↔ Farbe)
- [ ] Bauteile in Gruppen (Außenwände, Innenwände, Decke, Dach), automatisch vorsortiert und änderbar; Pappe je Gruppe wählen
- [ ] Teilenummern als Gravur auf jedes Teil (und in der 3D-Vorschau anzeigen, wo das Teil hingehört)
- [ ] Teile in der Vorschau einzeln drehen/verschieben
- [x] Warnung, wenn ein Teil größer als die Materialplatte ist

### Could (wenn Zeit bleibt)
- [ ] Materialstärke eingeben und Steckverbindungen (Nut/Falz) einplanen *(teilweise: Materialstärke-Feld da)*
- [ ] Auswahl „Kanten“ – wie Platten an Ecken zusammenstoßen:
  - [x] stumpf (Umrisse wie flach gelegt)
  - [x] Materialstärke ausgleichen (Stoß auf Außenkante, größere Platte läuft durch)
  - [ ] Gehrung von Hand (blaue Anritzlinie zum Abschrägen)
  - [ ] Auffalten (Flächen als ein Stück, Knicke blau)
- [x] IFC-Dateien direkt aus Archicad einlesen *(Wände, Decken/Böden, Dächer; noch mit echtem Archicad-IFC testen)*
- [ ] Fugen/Fensterlinien auf Fassaden als Gravur übernehmen
- [ ] PDF-Export

## Etappen (an die Kurstage gekoppelt)
| Tag | Etappe | Ziel |
|---|---|---|
| Mo 16.11. | Idee & Plan | PLAN.md und CLAUDE.md stehen, Testmodell (OBJ) liegt im Ordner |
| Di 17.11. | Grundgerüst & Aussehen | OBJ hochladen, 3D-Vorschau, Teile flach legen, 2D-Vorschau – im Swiss Style |
| Mi 18.11. | Daten | Echtes Archicad-Modell testen, Maßstab, Linien bereinigen, Farbcodierung |
| Do 19.11. | Fertig & veröffentlichen | SVG/DXF-Export, Anordnung auf Platten, online über GitHub Pages. Am besten 12 Uhr Freeze, Poster vorbereiten |
| Fr 20.11. | Polieren & präsentieren | README fertig, Abgabe bis 16 Uhr, Präsentation |

## Technik (kurz)
- Eine einzige Webseite (`index.html`) mit JavaScript – kein Server, keine Installation nötig.
- three.js (kostenlose 3D-Bibliothek, MIT-Lizenz) für das Einlesen der OBJ-Datei und die 3D-Vorschau.
- SVG und DXF werden von der App selbst als Text geschrieben.
- Veröffentlichung über GitHub Pages (kostenlos, direkt aus dem Repo).

## Annahmen
- Modell ist im CAD 1:1 in Metern oder Millimetern gezeichnet (Einheit wählbar in der App).
- Jedes Bauteil ist in der OBJ-Datei ein eigenes Objekt (Archicad exportiert das so).
- Bauteile sind ebene Platten (keine gebogenen Wände).

## Stand
- 16.11.: Repo geklont, Interview geführt, PLAN.md und CLAUDE.md angelegt.
- 16.11.: App-Name festgelegt: **LaserPrep – unfold your ideas** (in README, PLAN, CLAUDE).
- 16.11.: Laser-Standards festgelegt: Rot 255,0,0 = Schneiden, Blau 0,0,255 = Anritzen,
  Gelb 255,255,0 = Orientierung, Schwarz = Gravur (gefüllt). Alle Linien 0,00 mm Haarlinie
  (in SVG dünnste sichtbare Linie, in DXF echte 0,00 mm).
- 16.11.: Testmodell `beispiel/testhaus.obj` erzeugt: Einheit mm, Y = oben, 6 Objekte
  (Boden, Decke, Wand_Sued mit Tür + Fenster, Wand_Nord mit Fenster, Wand_West, Wand_Ost mit Fenster).
  Netz geschlossen (jede Kante gehört zu genau 2 Flächen).
- 16.11.: Alles auf GitHub (`main`). Git ist auf diesem Rechner mit GitHub verbunden.
- 16.11.: Erstes Feature fertig: `index.html` – OBJ per Ziehen oder Button „OBJ-Datei wählen“ laden,
  3D-Vorschau (drehen, verschieben, zoomen), hellgrau mit Kanten wie ein Kartonmodell.
  Rechts eine Bauteilliste; Maus auf einen Namen → Bauteil leuchtet orange. Akzentfarbe: Orange (#ff6a00).
  Getestet mit `beispiel/testhaus.obj`: alle 6 Bauteile erkannt, Tür und Fenster sichtbar.
  three.js r160 (MIT) per CDN, in README genannt.

- 16.11.: Zweites Feature fertig: kleine Version der Laserdatei.
  Jedes Bauteil wird flach gelegt (größte ebene Fläche → 2D, Rand = Außenumriss + Löcher;
  Öffnungen am Wandrand werden Teil des Außenumrisses). Einstellungen rechts: Einheit mm/m
  (Standard mm), Maßstab 1:50/1:100/1:200/frei (Standard 1:50), Platte B × H (Standard 600 × 450 mm).
  Teile liegen zeilenweise mit 5 mm Abstand auf der Platte, 2D-Vorschau unter dem 3D-Modell,
  Hinweis wenn etwas nicht passt. Hauptbutton „SVG herunterladen“: Maße in mm, rot = Schnitt,
  gelb = Plattenrahmen, Haarlinie 0,01 mm. Getestet mit dem Testhaus: 6 Umrisse, Boden 120 × 80 mm,
  Südwand mit Tür (am Rand) und Fenster.
- Beobachtung: Im Testhaus haben nur Wand_Sued echte Öffnungen. Wand_Nord und Wand_Ost sind
  in der OBJ in Abschnitte geteilt, aber alle Abschnitte sind geschlossen (kein Fenster-Loch).
- 16.11.: Drittes Feature fertig: IFC-Dateien laden (zusätzlich zu OBJ).
  Bibliothek web-ifc 0.0.78 (MPL-2.0) per CDN; sie wird nur geladen, wenn eine IFC-Datei kommt,
  und holt ihren Rechenkern (WASM) ebenfalls vom CDN – klappt darum ohne eigenen Server.
  Übernommen werden IfcWall, IfcWallStandardCase, IfcSlab, IfcRoof; Fenster und Türen werden
  weggelassen (in der Wand bleibt das Loch). Jedes Bauteil wird ein Mesh mit seinem IFC-Namen,
  Flachlegen und SVG laufen unverändert. Einheit wird bei IFC automatisch auf „m“ gestellt
  (web-ifc liefert Meter), beim nächsten OBJ wieder zurück.
  Testdatei `beispiel/testhaus.ifc` (IFC4, mm, gleiche Maße wie das OBJ-Testhaus + flaches Dach,
  2 Fenster, 1 Tür): 7 Bauteile, Südwand mit Fenster-Loch + Tür am Rand, Nordwand mit Fenster-Loch.
- 16.11.: Zweite Testdatei `beispiel/testhaus_walmdach.ifc`: gleiches Haus mit Walmdach (35°, 20 cm Überstand),
  als IfcRoof mit 4 Dachplatten (IfcSlab). Ergebnis: 10 Teile, Dachflächen in wahrer Größe flach gelegt
  (Süd/Nord Trapez 128 × 53,7 mm, Ost/West Dreieck 88 × 53,7 mm bei 1:50). Gehrungen an den Graten fehlen noch.
  Bauteilliste repariert: Nummer, Name und Maß stehen immer in einer Zeile; sehr lange Namen werden mit
  „…“ gekürzt, der ganze Name erscheint beim Darüberfahren mit der Maus.
- 16.11.: Viertes Feature fertig: Auswahl **„Kanten“** unter „Laserdatei“ mit „stumpf“ (Standard, genau wie bisher)
  und „Materialstärke ausgleichen“ + Feld „Materialstärke (mm)“ (echte Pappdicke, Standard 2 mm).
  Entscheidungen: Die **größere Platte läuft durch**, die kleinere wird gekürzt (bei gleich großen die zuerst
  genannte); die Dicke kommt **immer aus dem Feld**, nicht aus dem CAD.
  So funktioniert es: Jede Platte hat eine Außenseite (vom Hausinneren weg). Wo sich die Außenseiten zweier
  Platten treffen, liegt die äußere Ecklinie. Außenkanten nah an so einer Linie sind Stöße. Die durchlaufende
  Platte geht bis zur Ecklinie, die gekürzte endet innen an ihr (bei 90° genau 1 × Pappdicke, bei schrägen
  Ecken so, dass nichts übersteht). Freie Kanten, Tür-/Fensterkanten und Löcher bleiben, Dachüberstände
  über Wänden zählen nicht als Stoß. Die Außenmaße des Hauses stimmen dadurch unabhängig davon, wie dick
  die Wände im CAD gezeichnet sind.
  Getestet (1:50, 2 mm): OBJ-Testhaus Wände 120 × 64 / 76 × 64 mm statt 120 × 60 / 70,4 × 60;
  IFC-Testhaus Wände 120 × 60 / 76 × 60 statt 120 × 56 / 72 × 56; Walmdach: Trapeze laufen an den Graten
  durch (131,4 × 55,8 bzw. 53,9 mm), Dreiecke gekürzt (87,6 × 53,5 mm), First Süd läuft durch.
  „stumpf“ liefert Zeichen für Zeichen dieselbe SVG wie vorher. In der Meldung steht, wie viele Stoßkanten angepasst wurden.
  Noch offen: Bei schrägen Stößen (Grate, First) bleibt außen eine kleine Kerbe – das löst später „Gehrung von Hand“.

- 17.11.: Fünftes Feature fertig: **neuer Aufbau als Bento-Grid**. Alle Kacheln sind von Anfang an sichtbar und
  werden der Reihe nach abgefragt: 01 Pappe (Größe + Dicke) → 02 Datei (OBJ/IFC, daneben große 3D-Kachel) →
  03 Maßstab (+ Einheit) → 04 Farben (zeigt die Laser-Farben) → 05 Gehrung (Kanten: stumpf / Materialstärke
  ausgleichen) → 06 Bauteile (Liste mit Maßen) → 07 Vorschau (große Kachel mit Platte, Meldung und „SVG herunterladen“).
  Die aktive Kachel hat einen orangen Rahmen und einen „Weiter“-Button, erledigte zeigen eine kurze
  Zusammenfassung und lassen sich zum Ändern anklicken, spätere sind grau. Nach dem Laden einer Datei geht es
  automatisch mit dem Maßstab weiter. Die Pappdicke steht jetzt bei 01 Pappe (früher bei „Kanten“).
  Im schmalen Fenster stehen alle Kacheln untereinander. Rechnung und SVG sind unverändert.
  Entscheidungen für die nächsten Schritte: mehrere Pappsorten (Name, Größe, Dicke, Anzahl);
  Gruppen automatisch vorsortiert und änderbar.

- 17.11.: Sechstes Feature fertig: **mehrere Pappsorten** in Kachel 01. Jede Sorte hat Name, Größe, Dicke und
  Anzahl; mit „+ Pappsorte hinzufügen“ kommt eine neue dazu (× entfernt sie, eine bleibt immer).
  Verteilung (solange es noch keine Gruppen gibt): erst alle Platten der ersten Sorte füllen, was nicht passt,
  kommt auf die nächste Sorte. Teile, die für eine Sorte zu groß sind, wandern gleich weiter.
  Bei „Materialstärke ausgleichen“ gilt für jedes Teil die Dicke der Pappe, auf der es liegt.
  Vorschau: jede benutzte Platte als eigene Karte („Graupappe · Platte 1 von 2“, Größe, Dicke, Anzahl Teile)
  mit eigenem SVG-Button; der Hauptbutton lädt alle Platten nacheinander herunter.
  Dateiname: `testhaus_1-50_Graupappe_1.svg`. Meldungen: „Größer als jede Pappe“ bzw. „Kein Platz mehr,
  alle Platten sind voll … Anzahl erhöhen oder Sorte hinzufügen“.
  Getestet: Standard (1 × Graupappe 600 × 450) gibt Zeichen für Zeichen dieselbe SVG wie vorher;
  2 × 260 × 180 → 2 Platten (4 + 2 Teile); 1 × Graupappe + 1 × Karton 1 mm → Rest auf den Karton.
  Noch offen: Stößt ein Teil an ein Teil auf einer anderen Pappe, wird mit der eigenen Dicke gekürzt
  (richtig wäre die Dicke der durchlaufenden Platte) – das klären wir mit den Gruppen.

- 17.11.: Aussehen überarbeitet: Kacheln mit runden Ecken; die aktive Kachel ist orange gefüllt mit weißer
  Schrift (Buttons darin weiß mit oranger Schrift, Farblegende und Plattenkarten auf weißem Grund),
  erledigte und gesperrte Kacheln sind weiß mit grauer Schrift. Hauptschrift **Space Grotesk** (Google Fonts,
  freie OFL-Lizenz) – Gumroads eigene Schrift Mabry Pro ist kostenpflichtig, darum dieser freie Ersatz.
  Ohne Internet fällt die Seite auf Helvetica/Arial zurück.

## Nächste Schritte
1. Farben individuell zuordnen (Kachel 04).
2. Gruppen (Außenwände, Innenwände, Decke, Dach) und Pappe je Gruppe (Kachel 06).
3. Wirklich platzsparend anordnen (statt zeilenweise).
4. Doppelte Linien entfernen.
5. DXF-Export.
6. Echtes Archicad-Modell testen (OBJ und IFC).
7. Kanten: „Gehrung von Hand“, danach „Auffalten“ (Kachel 05).
