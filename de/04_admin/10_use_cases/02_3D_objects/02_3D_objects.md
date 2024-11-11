---
description: >-
  Hilfen zur Darstellung von 3D Objekten in Goobi anstelle von Bildern
---

# Umgang mit 3D Objekten

Anstelle von zweidimensionalen Bildern können im `images` Ordner auch 3D-Objekte gespeichert und in der Goobi-Oberfläche angezeigt werden. Grundsätzlich kann Goobi folgende 3D-Formate anzeigen:

```bash
.obj
.ply
.stl
.fbx
.gltf
.glt
.x3d
```

Volle Unterstützung für Texturen existiert jedoch nur für die Formate `.obj`, `.gltf` und `.glb`. Daher sollte nach Möglichkeit eines dieser Formate verwendet werden. Für das `.gltf` und `.glb` Format wird eine DRACO-Kompression unterstützt.

## Zusätzliche Ressourcen

Oft benötigt ein 3D-Objekt zusätzliche Ressourcen-Dateien um korrekt angezeigt zu werden. Dies sind üblicherweise Bilddateien für Oberflächentexturen sowie `.mtl` Dateien mit Materialdefinitionen für `.obj` Dateien. Diese Dateien sollten immer in einem eigenen Dateiordner neben der Objektdatei gespeichert werden, der genauso heißt wie die Objektdatei ohne Dateiendung. `.mtl` Dateien können beliebig benannt werden, während die Benennung der Bilddateien durch die 3D-Objektdatei oder die `.mtl` Datei vorgegeben ist.

```bash
1234/images/myObject.obj
1234/images/myObject/materials.mtl
1234/images/myObject/textures01.jpg
1234/images/myObject/textures02.jpg
1234/images/anotherObject.glb
1234/images/andYetAnotherObject.gltf
1234/images/andYetAnotherObject/textures.jpg
```

## Bekannte Probleme

* Sehr große 3D-Objekte mit über einer Millionen Kanten können von Browsern oft nicht oder nur sehr schleppend dargestellt werden. Es ist ratsam, nur kleinere Dateien in Goobi zu verwenden.
* Bei Verwendung einer `.mtl` Datei wird manchmal kein Bild angezeigt. Dies kann am Inhalt der .mtl Datei selbst liegen, wenn diese folgende Zeile enthält:\
  `Tr 1.0` oder `d 0.0`\
  Dies setzt die Transparenz des Objektes auf 100%, wodurch es überhaupt nicht dargestellt wird. Stattdessen muss die Zeile lauten:\
  `Tr 0.0` oder `d 1.0`
* Die Darstellung des Objektes kann außerdem beeinflusst werden durch folgende Zeile:\
  `illum 1` beziehungsweise `illum 2`\
  Die Option `illum 1` unterdrückt spiegelnde Reflektionen am Objekt, `illum 2` ermöglicht sie. Spiegelnde Reflektionen können ein Objekt überbelichtet erscheinen lassen, andererseits aber auch die dreidimensionale Gestalt hervorheben.

\