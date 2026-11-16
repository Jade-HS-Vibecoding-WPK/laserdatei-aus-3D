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
- [ ] OBJ-Datei hochladen und 3D-Vorschau anzeigen
- [ ] Jedes Objekt als Platte erkennen und flach legen (Umriss + Öffnungen)
- [ ] Maßstab wählen (1:50, 1:100, 1:200, frei)
- [ ] Doppelte/überlappende Linien automatisch entfernen
- [ ] Farbcodierung: Rot (Haarlinie 0,00 mm) = Schneiden, Blau = Anritzen, Gelb = Orientierungsrahmen, Schwarz = Gravur (Farben als Standard kann man aber auch individuell ändern)
- [ ] Materialplatte frei einstellbar (Breite × Höhe in mm), Teile automatisch darauf verteilen
- [ ] 2D-Vorschau der Laserplatte(n) im Browser
- [ ] Export als SVG und DXF

### Should (wäre gut)
- [ ] Teilenummern als Gravur auf jedes Teil (und in der 3D-Vorschau anzeigen, wo das Teil hingehört)
- [ ] Teile in der Vorschau einzeln drehen/verschieben
- [ ] Warnung, wenn ein Teil größer als die Materialplatte ist

### Could (wenn Zeit bleibt)
- [ ] Materialstärke eingeben und Steckverbindungen (Nut/Falz) einplanen
- [ ] IFC-Dateien direkt aus Archicad einlesen
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

## Nächste Schritte
1. Testmodell `beispiel/testhaus.obj` erzeugen (4 Wände, Decke, Boden, ein Fenster, eine Tür).
2. Erstes Feature: OBJ hochladen und 3D-Vorschau anzeigen.
