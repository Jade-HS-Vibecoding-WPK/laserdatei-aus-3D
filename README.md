# LaserPrep
*unfold your ideas*

**LaserPrep** macht aus einem 3D-Modell (z. B. aus Archicad) fertige Laserdateien für den Architektur-Modellbau.
Die App legt jedes Bauteil flach hin, verkleinert es auf den Modellmaßstab, ordnet alle Teile platzsparend auf der
Pappe an und speichert sie als SVG oder DXF, mit der richtigen Laser-Farbcodierung. Dazu gibt es eine
Bauanleitung als PDF und als drehbares 3D-Modell.

**Online ausprobieren:** https://jade-hs-vibecoding-wpk.github.io/laserdatei-aus-3D/

Ohne Installation, ohne Anmeldung. Alles läuft im Browser, die Modelle verlassen deinen Rechner nicht.

---

## So geht's – Schritt für Schritt

Die Seite ist ein Raster aus Kacheln. Man füllt sie der Reihe nach aus; erledigte Kacheln zeigen eine kurze
Zusammenfassung und lassen sich jederzeit wieder öffnen.

| Kachel | Was man dort macht |
|---|---|
| **01 Pappe** | Pappsorten eintragen: Name, Breite × Höhe, Dicke, Anzahl der Platten. Mehrere Sorten sind möglich. Wer noch keine Pappe hat, klickt „Ich habe noch keine Pappe“ – LaserPrep schlägt dann das handelsübliche Format mit dem wenigsten Rest vor (begrenzt auf die Größe des Laserbetts). |
| **02 Datei** | OBJ- oder IFC-Datei auf die Seite ziehen oder auswählen. Das Modell erscheint in 3D (ziehen = drehen, rechte Maustaste = verschieben, Rad = zoomen). |
| **03 Maßstab** | 1:50, 1:100, 1:200 oder frei; dazu die Einheit, in der das CAD-Modell gezeichnet ist (mm oder m). Das Modell wird im CAD 1:1 gezeichnet, verkleinert wird erst hier. |
| **04 Farben** | Welche Farbe für Schneiden, Anritzen, Orientierungsrahmen und Gravur steht. Standard siehe unten, frei änderbar. |
| **05 Gehrung / Kanten** | Wie die Ecken zusammenkommen (siehe „Kanten-Varianten“). |
| **06 Auswahl** | Bauteile sind automatisch in Gruppen sortiert (Außenwände, Innenwände, Bodenplatte, Decken, Dach, Treppe, Sonstiges). Hier wählt man, was gelasert wird, welche Pappe jede Gruppe bekommt und welche Fassaden-Textur. |
| **07 Bauteile** | Liste aller Bauteile mit Größe. Maus über einen Namen → das Teil leuchtet im Modell und in der Vorschau. |
| **08 Vorschau** | Alle Platten mit den angeordneten Teilen, daneben ein kleines 3D-Modell. Hier gibt es Lupe, Maßband, Bauanleitung und den Download. |

### Kanten-Varianten (Kachel 05)
- **Stumpf** – Teile genau wie im Modell. Schnell, an den Ecken überlappen die Platten um die Pappdicke.
- **Materialstärke ausgleichen** – die kleinere Platte wird um die Dicke der Platte gekürzt, auf die sie stößt;
  außen bündig. Hat eine Gruppe eine eigene Pappe, zählt deren Dicke.
- **Gehrung von Hand** – eine blaue Anritzlinie zeigt, bis wohin man die Kante schräg abschleift (saubere 45°-Ecke).
- **Auffalten** – aneinanderstoßende Flächen einer Gruppe bleiben ein Stück (ein „Netz“), die Knicke werden blau
  angeritzt und gefaltet. Würde sich das Netz überlappen oder nicht auf die Pappe passen, wird dort geschnitten.

### Fassaden-Texturen (Kachel 06)
Je Gruppe wählbar: Mauerwerk, Klinker, Holzschalung, Plattenfassade, Dachziegel – oder eine **eigene Strichdatei**
(SVG oder DXF hochladen). Die Linien werden in der Gravur-Farbe auf die Außenseite der Teile gelasert, Fenster
bleiben frei. Texturen gibt es nur bei „stumpf“ und „Materialstärke ausgleichen“ (beim Anritzen oder Falten läge die
falsche Seite oben).

### Treppen
Treppen werden automatisch in **Trittstufen, Setzstufen und Wangen** zerlegt, damit man sie einzeln lasern und
zusammenkleben kann. Bei Archicad-IFC-Dateien, die eine Treppe mehrfach enthalten, wird nichts doppelt gelasert.

### Vorschau (Kachel 08)
- **Hervorheben:** Maus über ein Teil auf der Platte oder Klick ins 3D-Modell → dasselbe Teil leuchtet überall orange.
- **Lupe:** Schalter „Lupe“ – ein runder Ausschnitt zeigt die Stelle unter der Maus dreifach vergrößert.
- **Maßband:** Schalter „Maßband“ – Maus auf eine Kante zeigt ihre Länge, zwei Klicks messen eine Strecke.
  Angezeigt wird das Maß auf der Pappe und im echten Gebäude. Esc löscht die Messung.
- **Abstand:** Abstand zwischen den Teilen und zum Plattenrand (Standard 5 mm).

### Bauanleitung
Mit Häkchen wählt man, was hineinkommt: **Teileliste** (mit Plan jeder Platte), **Bauschritte**, **Bilder vom Modell**,
**Kanten & Kleben** (Material, Werkzeug, Tipps zum gewählten Kanten-Modus).
- **„Bauanleitung öffnen“** – druckbare Seite; über „Drucken / als PDF speichern“ wird daraus ein PDF.
- **„Online ansehen“** – Schritt für Schritt mit großem, drehbarem 3D-Modell: aktueller Schritt orange,
  schon gebaute Teile grau, spätere durchsichtig. Weiter mit „Weiter“ oder den Pfeiltasten.

Die Reihenfolge ist Bodenplatte → Außenwände → Innenwände → Treppe → Decken → Dach. Die Teilnummern stehen nur in der
Anleitung, nicht auf der Pappe – am besten die Teile nach dem Lasern gleich auf den Plattenplan legen.

### Download
Format wählen – **SVG**, **DXF** oder **DWG** – und herunterladen: eine Datei pro Platte, z. B.
`testhaus_1-50_Graupappe_1.svg`. DWG ist ein geschlossenes Autodesk-Format, das eine Webseite nicht sicher schreiben
kann; bei „DWG“ bekommt man darum eine DXF-Datei und öffnet sie in AutoCAD → „Speichern unter“ → „AutoCAD-Zeichnung (*.dwg)“.

---

## Laser-Konventionen (Standard)

| Farbe | RGB | Bedeutung |
|---|---|---|
| Rot | 255, 0, 0 | Schneiden |
| Blau | 0, 0, 255 | Anritzen (Gehrung, Faltkanten) |
| Gelb | 255, 255, 0 | Orientierungsrahmen (Plattengröße) |
| Schwarz | 0, 0, 0 | Gravur (Fassaden-Texturen) |

- Alle Linien als Haarlinie (0,00 mm).
- Keine doppelten Linien: Vor dem Speichern wird geprüft, dass keine Linie zweimal geschnitten wird.
- In der DXF liegt jede Funktion auf einer eigenen Ebene (`SCHNEIDEN`, `ANRITZEN`, `ORIENTIERUNG`, `GRAVUR`), alle Maße in mm.

---

## Welche Dateien gehen?

- **OBJ** – jedes Objekt in der Datei wird ein Bauteil (eine Platte).
- **IFC** (z. B. Export aus Archicad) – übernommen werden Wände, Decken/Böden, Dächer und Treppen. Fenster und Türen
  fallen weg, in den Wänden bleiben ihre Öffnungen. Für IFC braucht die Seite einmal Internet, weil der IFC-Leser
  vom CDN geladen wird.

**Tipp für den Export:** Jedes Bauteil sollte ein eigenes Objekt sein, das Modell 1:1 gezeichnet.

### Beispielmodelle zum Ausprobieren
Im Ordner `beispiel/`:
- `testhaus.obj` – kleines Haus mit Fenstern und Tür
- `testhaus.ifc` – dasselbe als IFC mit Flachdach
- `testhaus_walmdach.ifc` – Haus mit Walmdach (schräge Teile)
- `testtreppe.obj` – gerade Treppe mit 6 Stufen und Bodenplatte

---

## Technik

- Eine einzige, statische Webseite: `index.html` mit JavaScript – kein Server, kein Build-Schritt, keine Anmeldung.
- SVG und DXF werden direkt in der Seite als Text erzeugt.
- Veröffentlicht über GitHub Pages. Lokal geht es auch: `index.html` im Browser öffnen.

### Verwendete Bibliotheken
- [three.js](https://threejs.org) r160 – 3D-Darstellung und OBJ-Import, MIT-Lizenz
- [web-ifc](https://github.com/ThatOpen/engine_web-ifc) 0.0.78 – IFC-Dateien lesen, MPL-2.0-Lizenz
  (unverändert per CDN eingebunden)
- [Space Grotesk](https://fonts.google.com/specimen/Space+Grotesk) – Schrift, SIL Open Font License (OFL), über Google Fonts

---

## Projekt

Entstanden im Wahlpflichtkurs „Vibecoding KI-Werkstatt“ an der Jade Hochschule (Wintersemester 2026/27) –
gebaut aus dem Architekturstudium heraus, ohne Programmierkenntnisse, zusammen mit Claude Code.
Wie es geplant und Schritt für Schritt gebaut wurde, steht in [PLAN.md](PLAN.md).

Lizenz: [MIT](LICENSE)
