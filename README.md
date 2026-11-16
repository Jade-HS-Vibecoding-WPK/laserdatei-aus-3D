# LaserPrep
*unfold your ideas*

Anhand eines 3D-Modells wird eine Laserdatei erstellt.

## Benutzung
`index.html` im Browser öffnen und eine OBJ- oder IFC-Datei auf die Seite ziehen
(oder „OBJ- oder IFC-Datei wählen“ klicken).
Zum Ausprobieren liegen Testmodelle in `beispiel/testhaus.obj`, `beispiel/testhaus.ifc` (Flachdach)
und `beispiel/testhaus_walmdach.ifc` (Walmdach).

Aus IFC-Dateien werden Wände, Decken/Böden und Dächer übernommen. Fenster und Türen werden
weggelassen – in den Wänden bleiben nur ihre Öffnungen. Für IFC braucht die Seite Internet,
weil der IFC-Leser beim ersten Mal vom CDN geladen wird.

## Verwendete Bibliotheken
- [three.js](https://threejs.org) r160 – 3D-Darstellung und OBJ-Import, MIT-Lizenz
- [web-ifc](https://github.com/ThatOpen/engine_web-ifc) 0.0.78 – IFC-Dateien lesen, MPL-2.0-Lizenz
  (unverändert per CDN eingebunden)
