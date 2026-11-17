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
- [ ] Farbcodierung: Rot (Haarlinie 0,00 mm) = Schneiden, Blau = Anritzen, Gelb = Orientierungsrahmen, Schwarz = Gravur (Farben als Standard kann man aber auch individuell ändern) *(teilweise: Farben einstellbar; in der SVG gibt es bisher nur Schneiden + Orientierungsrahmen, Anritzen/Gravur folgen)*
- [x] Materialplatte frei einstellbar (Breite × Höhe in mm), Teile automatisch darauf verteilen *(mehrere Sorten und Platten, Teile gedreht und dicht ineinander gelegt)*
- [x] 2D-Vorschau der Laserplatte(n) im Browser
- [ ] Export als SVG und DXF *(SVG fertig, DXF fehlt)*

### Should (wäre gut)
- [x] Aufbau als Bento-Grid: 7 Schritte nacheinander abfragen (01 Pappe, 02 Datei, 03 Maßstab, 04 Farben, 05 Gehrung, 06 Bauteile, 07 Vorschau)
- [x] Mehrere Pappsorten (Name, Größe, Dicke, Anzahl) und mehrere Platten
- [x] „Ich habe noch keine Pappe“: LaserPrep schlägt das handelsübliche Format mit dem wenigsten Rest vor (begrenzt aufs Laserbett)
- [x] Farben individuell zuordnen (Funktion ↔ Farbe)
- [ ] Bauteile in Gruppen (Außenwände, Innenwände, Decke, Dach), automatisch vorsortiert und änderbar; Pappe je Gruppe wählen *(teilweise: Gruppen + Auswahl was gelasert wird; Pappe je Gruppe fehlt)*
- [ ] Teilenummern als Gravur auf jedes Teil (und in der 3D-Vorschau anzeigen, wo das Teil hingehört) *(teilweise: Nummer + Name in der Vorschau, Hervorheben im 3D-Modell; Gravur in der Datei bewusst nicht)*
- [ ] Teile in der Vorschau einzeln drehen/verschieben
- [x] Warnung, wenn ein Teil größer als die Materialplatte ist

### Could (wenn Zeit bleibt)
- [ ] Materialstärke eingeben und Steckverbindungen (Nut/Falz) einplanen *(teilweise: Materialstärke-Feld da)*
- [ ] Auswahl „Kanten“ – wie Platten an Ecken zusammenstoßen:
  - [x] stumpf (Umrisse wie flach gelegt)
  - [x] Materialstärke ausgleichen (Stoß auf Außenkante, größere Platte läuft durch)
  - [x] Gehrung von Hand (blaue Anritzlinie zum Abschrägen)
  - [x] Auffalten (Flächen als ein Stück, Knicke blau)
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

- 17.11.: Mauszeiger als **Punkt**: orange auf weißen/hellen Flächen, weiß auf Orange (aktive Kachel, orange
  Buttons). Über Buttons, Feldern und anklickbaren Kacheln wird er etwas größer. Die App schaut dafür unter
  dem Punkt nach der Hintergrundfarbe. Auf Touch-Geräten (ohne Maus) bleibt der normale Zeiger.

- 17.11.: **Intro-Animation** beim Öffnen (gut 3,5 s): Die ganze Seite ist orange, ein leuchtender Laserpunkt
  fährt Buchstabe für Buchstabe die Umrisse von „LaserPrep“ (über die volle Bildschirmbreite) nach, die
  Buchstaben füllen sich weiß, danach wird „unfold your ideas“ kleiner darunter eingelasert. Dann fliegt der
  Titel nach oben links genau auf den echten Titel (wird dabei schwarz), das Orange blendet aus und die normale
  Ansicht erscheint. Läuft bei jedem Öffnen; Klick oder Taste überspringt. Wer im Betriebssystem
  „Bewegung reduzieren“ eingestellt hat, sieht kein Intro. Eigenes kleines Skript, damit das Intro auch
  verschwindet, falls three.js nicht lädt.

- 17.11.: Neuer Button **„Ich habe noch keine Pappe“** in Kachel 01. Statt der Pappsorten gibt man dann nur
  die Größe des Laserbetts (Standard 600 × 450 mm) und die Pappdicke ein. In der Vorschau probiert LaserPrep die
  handelsüblichen Formate A4, A3, A2, A1, 50 × 70 und 70 × 100 cm (beide Ausrichtungen, nur was ins Laserbett passt)
  und schlägt das vor, bei dem insgesamt am wenigsten Pappe gebraucht wird (bei Gleichstand: weniger Platten),
  z. B. „Vorschlag: 1 × A3 · Teile füllen etwa 34 % der Pappe“. „Übernehmen“ trägt den Vorschlag als eigene
  Pappe ein. Getestet mit dem Testhaus: 1:50 → 1 × A3, 1:100 → 1 × A4, 1:25 → 1 × A2, Laserbett 300 × 220 bei 1:30
  → 5 × A4; zu große Teile oder zu kleines Laserbett werden gemeldet. „stumpf“ mit eigener Pappe unverändert.
  Hinweis: Die Ausnutzung ist noch niedrig, weil die Teile nur zeilenweise liegen – platzsparendes Anordnen
  verbessert später auch den Vorschlag.

- 17.11.: **Farben zuordnen** in Kachel 04: Für Schneiden, Anritzen, Orientierung und Gravur gibt es je ein Farbfeld
  (Klick öffnet die Farbauswahl), daneben der Farbname. Haben zwei Funktionen dieselbe Farbe, warnt die App.
  „Standardfarben wiederherstellen“ setzt Rot/Blau/Gelb/Schwarz zurück. Vorschau und SVG benutzen sofort die
  gewählten Farben (bisher Schneiden + Rahmen, weil es noch keine Anritz- oder Gravurlinien gibt). Der Browser merkt
  sich die eigenen Farben für das nächste Mal. Mit Standardfarben ist die SVG Zeichen für Zeichen wie vorher.

- 17.11.: **Kachel 05 Gehrung** zeigt jetzt alle vier Kanten-Varianten als Karten mit je zwei kleinen Skizzen:
  links die Ecke im Schnitt (wie die Platten zusammenstoßen), rechts das Teil, wie es aus dem Laser kommt
  (Schnitt- und Anritzlinien in den Farben aus Kachel 04). Stumpf und Materialstärke ausgleichen sind wählbar;
  „Gehrung von Hand“ und „Auffalten“ sind schon zu sehen, aber als „kommt bald“ gesperrt. Kachel 05 geht dafür
  jetzt über die ganze Breite, die Bauteilliste (06) steht darunter.

- 17.11.: **Gehrung von Hand** fertig (Karte in Kachel 05 freigeschaltet). An jedem Stoß gehen beide Platten bis zur
  äußeren Ecklinie; das ist die rote Schnittkante. Auf der Innenseite liegt eine blaue Anritzlinie im Abstand
  Dicke ÷ tan(Innenwinkel ÷ 2) von der Kante – bei 90° genau 1 × Pappdicke, an den Walmdach-Graten (132°) 0,45 ×,
  am First (110°) 0,7 ×. Von der Linie bis zur Kante wird schräg abgeschliffen. Damit die angeritzte Seite nach
  innen kommt, werden Teile, deren flache Ansicht die Außenseite zeigt, gespiegelt. Freie Kanten, Tür-/Fensterkanten
  und Löcher bekommen keine Linie. In der SVG steht eine eigene Gruppe in der Anritz-Farbe aus Kachel 04.
  Getestet (1:50, 2 mm): OBJ-Testhaus Wände 120 × 68 / 80 × 68 mm, Linien 2 mm innen, an der Tür unterbrochen;
  Walmdach: Dachdreiecke 91,4 × 55,8 mm, Linien parallel zu den Graten. Stumpf bleibt unverändert (keine blaue Gruppe).

- 17.11.: **Platzsparend anordnen**: Die Teile liegen nicht mehr zeilenweise, sondern werden gedreht und mit ihrer
  echten Form ineinandergeschoben. So funktioniert es: Die Pappe wird in ein Raster aus etwa 1,5-mm-Kästchen geteilt,
  jedes Teil wird in mehreren Drehungen gerastert (0°, 90°, 180°, 270° und so, dass eine der längsten Kanten
  waagerecht liegt). Die großen Teile kommen zuerst; jedes Teil kommt an die Stelle oben links, an der es am wenigsten
  nach unten ragt, ohne andere Teile oder den Abstand zu verletzen. Teile werden nie gespiegelt (wichtig für die
  Gehrung), Anritzlinien drehen mit. Neues Feld **„Abstand (mm)“** in Kachel 07 (Standard 5 mm) für den Abstand
  zwischen den Teilen und zum Rand. Wirkt auch auf mehrere Platten und den Formatvorschlag.
  Getestet mit dem Walmdach-Haus (1:50): alle 10 Teile auf einer Platte, Trapeze gedreht nebeneinander; der
  Formatvorschlag nutzt die Pappe jetzt zu etwa 51 % statt 34 %. Rechenzeit etwa 10 ms pro Neuberechnung.
  Hinweis: Die Anordnung ändert sich dadurch auch bei „stumpf“ (andere Lage der Teile, gleiche Umrisse).

- 17.11.: **Teile in der Vorschau erkennen**: Jedes Teil auf der Pappe trägt seine Nummer und seinen Namen
  (z. B. „07 Dachflaeche_Sued“, bei kleinen Teilen nur „07“, Nummer wie in der Bauteilliste) – sichtbar nur auf dem
  Teil unter der Maus, in der Schrift der App (Space Grotesk). Der Schriftzug steht
  nur in der Vorschau, nicht in der Laserdatei (so gewünscht). Fährt man mit der Maus über ein Teil, wird es orange
  hinterlegt, alle anderen Teile werden blass; gleichzeitig leuchtet das Bauteil im 3D-Modell orange, der Rest des
  Hauses wird durchsichtig, und der Name in der Bauteilliste wird orange. Umgekehrt zeigt die Maus auf einem Namen
  in der Bauteilliste das Teil auch in der Vorschau. Getestet mit dem Walmdach-Haus.

- 17.11.: **Bauteil im 3D-Modell anklicken**: Ein kurzer Klick auf eine Wand, Decke oder Dachfläche wählt das Bauteil
  aus. Es leuchtet orange, der Rest des Hauses wird durchsichtig, in der Vorschau wird der passende Zuschnitt
  hervorgehoben (mit Nummer + Name, Rest blass, die Seite scrollt bei Bedarf hin) und in der Bauteilliste markiert.
  Die Auswahl bleibt, bis man im 3D-Modell ins Leere klickt; Darüberfahren über andere Teile zeigt diese kurz an.
  Wer die Maus beim Klicken bewegt, dreht nur das Modell. Hinweiszeile im 3D-Feld ergänzt.

- 17.11.: **Neue Kachel 06 „Auswahl“** – welche Bauteile werden gelasert? Die Kacheln dahinter heißen jetzt
  07 Bauteile und 08 Vorschau. Oben stehen sieben Gruppen als Häkchen-Karten mit Anzahl: Außenwände, Innenwände,
  Dach, Decken, Bodenplatte, Treppe, Sonstige Bauteile (leere Gruppen sind blass). Darunter „Eigene Bauteile aus
  deiner Datei“: alle gefundenen Teile einzeln mit Häkchen, nach Gruppen sortiert (Maus auf dem Namen zeigt das Teil
  im 3D-Modell). Gruppen-Häkchen schalten die ganze Gruppe; ist nur ein Teil gewählt, zeigt das Häkchen einen Strich.
  Abgewählte Teile fehlen in Vorschau und SVG, sind im 3D-Modell blass und in der Bauteilliste durchgestrichen
  („nicht gelasert“). Standard: alles gewählt.
  Einsortieren: 1. IFC-Typ und Unterart (IfcSlab BASESLAB = Bodenplatte, FLOOR = Decke, ROOF/IfcRoof = Dach,
  IfcStair = Treppe, IfcWall = Wand; Außen/Innen aus Pset_WallCommon → IsExternal, falls vorhanden),
  2. Name (Wand, Dach, Boden, Decke, Treppe …), 3. Lage (senkrecht = Wand, schräg = Dach, unterste waagerechte
  Platte = Bodenplatte, oberste = Dach, dazwischen = Decke). Wand außen oder innen: von 9 Punkten auf der Wand wird
  waagerecht nach beiden Seiten geschaut; trifft man auf einer Seite meist keine andere Wand, ist sie außen.
  IFC liest jetzt zusätzlich Treppen, Stützen, Träger, Platten und sonstige Bauteile ein.
  Getestet: OBJ-Testhaus (4 Außenwände, Decke, Bodenplatte), Walmdach (4 Dachflächen → Dach), Testhaus mit
  zusätzlicher Trennwand (→ Innenwand) und Treppe (→ Treppe); Decke abwählen → 5 von 6 Teilen auf der Platte.

- 17.11.: **Überlappende Teile beim Anordnen behoben.** Ursachen: (1) Besteht ein Teil aus mehreren getrennten
  Stücken, hat das Anordnen nur das größte Stück beachtet – die anderen konnten unter fremden Teilen liegen.
  (2) Sehr spitze Ecken ragten zwischen den drei Messlinien pro Rasterzeile heraus und wurden übersehen.
  Neu: Alle Stücke eines Teils werden gerastert, und ein Kästchen gilt als belegt, sobald eine Kante, eine Ecke
  oder die Fläche es berührt. Weil das Raster das Teil jetzt sicher ganz abdeckt, fällt das bisherige
  „+1 Kästchen zur Sicherheit“ weg (mindestens 1 Kästchen Luft bleibt, auch bei Abstand 0 mm).
  Neue Prüfhilfe `laserprep.ueberlappungen()` vergleicht auf jeder Platte alle Teile paarweise mit ihrer echten
  Form (Überschneidung, Abstand kleiner als „Abstand (mm)“, zu nah am Plattenrand).
  Getestet: OBJ-Testhaus, IFC-Testhaus, Walmdach und ein eigenes Testmodell (Teile aus 2–3 getrennten Flächen,
  spitze Dreiecke, Nadeln, Kamm mit Zacken, Rauten) – je stumpf/ausgleichen/Gehrung, 1:20/1:50/1:75/1:100/1:200,
  Abstand 0/2/5 mm, Pappe 300 × 200 / 600 × 450 / 1000 × 700 und „Ich habe noch keine Pappe“: 720 Fälle,
  0 Überlappungen (vorher 1491 Funde im eigenen Testmodell, die Testhäuser waren schon sauber).
  Platzbedarf: Testhäuser nie mehr Platten als vorher, in 93 von 405 Fällen liegt die letzte Platte sogar weniger
  weit belegt, in 3 Fällen minimal mehr; Formatvorschlag insgesamt 1 % weniger Pappe; Walmdach 1:50 weiter A3 mit 51 %.

- 17.11.: **Auffalten** fertig (Karte in Kachel 05 freigeschaltet). Teile derselben Gruppe aus Kachel 06
  (z. B. alle Außenwände), die an einer Ecke zusammenstoßen, werden ein Stück („Netz“). An jeder Faltkante gehen
  beide Platten bis zur äußeren Ecklinie (kein Versatz), das Nachbarteil wird um diese Linie in die Ebene des ersten
  Teils geklappt. Die Faltkante wird blau angeritzt, alle anderen Stöße werden geschnitten wie bei „Materialstärke
  ausgleichen“, damit das Modell an den Schnittkanten schließt. Keine Klebelaschen. Die längsten gemeinsamen Kanten
  werden zuerst gefaltet; würde ein Knick das Netz sich selbst überlappen lassen oder zu groß für die Pappe machen,
  wird dort geschnitten statt geknickt (Meldung nennt die Anzahl). Teile verschiedener Gruppen hängen nie zusammen.
  Das Netz läuft als ein Teil durch das Anordnen; beim Darüberfahren leuchten alle Teile des Netzes.
  Getestet: OBJ-Testhaus → Band aus 4 Außenwänden 398 × 64 mm mit 3 Knicken (letzte Ecke geschnitten und um 2 mm
  gekürzt), Tür und Fenster bleiben; Walmdach → 4 Dachflächen ein Netz mit 3 Knicken (First geschnitten);
  kleine Pappe (250 × 180, 200 × 150 …) teilt die Netze automatisch. 183 Fälle (3 Modelle, 1:20–1:200, Abstand
  0/2/5 mm, 4 Pappgrößen, Formatvorschlag): 0 Überlappungen, alle Umrisse geschlossen. Stumpf, ausgleichen und
  Gehrung liefern Zeichen für Zeichen dieselbe SVG wie vorher (27 Vergleichsfälle).

- 17.11.: **Vorschau mit 3D-Modell und Lupe** (Kachel 08). Links neben den Platten steht ein zweites, kleineres
  3D-Modell (eigene Kamera, gleiche Szene). Es bleibt beim Scrollen im Bild und lässt sich drehen und zoomen.
  Ein Klick auf ein Bauteil wählt es aus wie im großen Modell; hervorgehobene Teile leuchten in beiden Modellen
  orange. Im schmalen Fenster steht das kleine Modell über den Platten.
  **Lupe:** Fährt die Maus über eine Platte, folgt ihr ein runder Kreis (180 px) mit dem Bereich darunter in
  3-facher Größe, inklusive Hervorhebung und Teilname. Die Lupe lässt die Maus durch, das Hervorheben
  funktioniert also weiter. Auf Touch-Geräten gibt es keine Lupe. Die Laserdatei (SVG) ändert sich nicht.
  Getestet mit OBJ-Testhaus und Walmdach: Modell und Platten nebeneinander (Fenster 1400 px), Klick im kleinen
  Modell markiert Wand_Nord in Liste und Vorschau, die Lupenmitte zeigt dieselbe Stelle wie die Maus.

- 17.11.: **Lupe flackert nicht mehr.** Ursache: Die vergrößerte Kopie in der Lupe hat die Maus selbst „gefangen“,
  sobald ein Teil unter dem Mauszeiger lag. Die App dachte dann, die Maus sei nicht mehr über der Platte, und
  blendete die Lupe aus; beim nächsten Bild kam sie wieder (an, aus, an …). Jetzt lässt die Kopie die Maus immer
  durch. Getestet: 20 Mausschritte quer über die Platte, Lupe durchgehend sichtbar (vorher jeder zweite Schritt aus).

- 17.11.: **Lupe mit Schalter.** In Kachel 08 neben „Abstand“ gibt es den Knopf „Lupe: aus / an“. Standard ist aus;
  der Browser merkt sich die Wahl für das nächste Mal. Der orange Ring um die Lupe ist weg, sie hat nur noch einen
  leichten grauen Schatten. Auf Touch-Geräten gibt es weder Lupe noch Knopf.
  Getestet: aus → keine Lupe, an → Lupe erscheint, wieder aus → Lupe verschwindet.

## Nächste Schritte
1. Pappe je Gruppe wählen (Gruppen gibt es jetzt in Kachel 06).
2. Doppelte Linien entfernen.
3. DXF-Export.
4. Echtes Archicad-Modell testen (OBJ und IFC).
