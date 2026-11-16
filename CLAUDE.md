# Ziel
Web-App **LaserPrep** (Slogan: „unfold your ideas"): OBJ-Modell (z. B. aus Archicad) hochladen, Bauteile flach legen,
als SVG/DXF für den Lasercutter exportieren. Details, MVP und Stand stehen in PLAN.md.

# Regeln
- Ich studiere Architektur und kann nicht programmieren: jeden Schritt einfach und auf Deutsch erklären.
- Erst fragen, dann bauen. Ein Feature pro Sitzung, klein halten.
- Nach jedem Feature: testen, committen, Stand in PLAN.md aktualisieren.
- Nur im Projektordner arbeiten.
- Nur Bibliotheken mit freier Lizenz (z. B. MIT) verwenden und in der README nennen.
- Keine API-Keys nötig; falls doch einmal, nur in `.env` und nie committen.

# Technik
- Reine statische Webseite: `index.html` + JavaScript, kein Build-Schritt, kein Server.
- three.js per CDN (feste Version) für OBJ-Import und 3D-Vorschau.
- SVG und DXF werden selbst als Text erzeugt.
- Veröffentlichung über GitHub Pages.

# Laser-Konventionen (Standard, in der App individuell änderbar)
- Rot (RGB 255,0,0) = Schneiden
- Blau (RGB 0,0,255) = Anritzen
- Gelb (RGB 255,255,0) = Orientierungslinie/-rahmen
- Schwarz = Gravur (Flächen oder Schriften mit Flächenfüllung)
- Alle Linien als Haarlinie mit 0,00 mm Linienstärke
- Schriften nur in Schriftarten, die in AutoCAD vorhanden sind
- Keine doppelten Linien; Teile platzsparend anordnen
- Modell im CAD 1:1, Modellmaßstab wird erst in der App angewendet

# Gestaltung
- Swiss Style: viel Weißraum, eine Akzentfarbe, klare Schrift
- Ein Hauptbutton pro Ansicht
