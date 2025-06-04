# Einführung in Rasterdaten

## Fragen

* Welches Format sollte ich verwenden, um meine Daten darzustellen?
* Welche Haupttypen von Geodaten gibt es?
* Was sind die wichtigsten Eigenschaften von Rasterdaten?

## Lernziele

* Den Unterschied zwischen Raster- und Vektordaten beschreiben.
* Vor- und Nachteile der Speicherung von Daten im Rasterformat beschreiben.
* Zwischen kontinuierlichen und kategorialen Rasterdaten unterscheiden und Beispiele für Datensätze in beiden Formaten benennen.

## Datenstrukturen: Raster und Vektor

Die zwei Haupttypen geografischer Daten sind Raster- und Vektordaten.

Rasterdaten werden als Gitter aus Werten gespeichert, die als Pixel auf einer Karte dargestellt werden. Jeder Pixelwert repräsentiert ein Gebiet auf der Erdoberfläche.

Vektordaten beschreiben spezifische Objekte auf der Erdoberfläche (Punkte, Linien, Polygone) und weisen diesen Attribute zu. Vektordaten werden in einer späteren Lektion behandelt.

## Was sind Rasterdaten?

Rasterdaten sind gepixelte (gerasterte) Daten, wobei jedem Pixel eine geografische Lage zugeordnet ist. Der Wert eines Pixels kann:

* kontinuierlich sein (z. B. Höhe), oder
* kategorial sein (z. B. Landnutzung).

Ein georeferenziertes Raster enthält neben den Bilddaten auch Informationen zu:

* Ausdehnung (Extent)
* Zellgröße (Auflösung)
* Anzahl der Zeilen und Spalten
* Koordinatenreferenzsystem (CRS)

![Rasterkonzept](fig/dc-spatial-raster/raster_concept.png)
*Abbildung: Konzept einer Rasterdatenstruktur (Quelle: NEON)*

Beispiele für kontinuierliche Rasterdaten:

1. Niederschlagskarten
2. Baumhöhen aus LiDAR-Daten
3. Höhenmodelle

![Höhenkarte - NEON Harvard Forest](fig/dc-spatial-raster/DSM_HARV_example.png)
*Abbildung: Kontinuierliche Höhendaten aus dem NEON AOP LiDAR Sensor*

Beispiele für kategoriale Rasterdaten:

1. Landnutzungskarten
2. Baumhöhen klassifiziert in niedrig, mittel, hoch
3. Höhenklassenkarten

![USA Landnutzungsklassifikation](fig/USA_landcover_classification.png)
*Abbildung: Landnutzungskarte der USA mit kategorialen Rasterdaten (Quelle: Homer et al., 2015)*

## Vorteile und Nachteile von Rasterdaten

**Vorteile:**

* Repräsentation kontinuierlicher Flächen
* Hoher Detailgrad möglich
* Gleichmäßige Datenstruktur für einfache Berechnungen

**Nachteile:**

* Große Dateigrößen bei hoher Auflösung
* Schlechte Metadatenintegration in manchen Formaten
* Eingeschränkte Möglichkeiten zur Darstellung komplexer Beziehungen

## Wichtige Eigenschaften von Rasterdaten

### Ausdehnung (Extent)

Die Ausdehnung gibt das geografische Gebiet an, das durch das Raster abgedeckt wird (Nord-, Süd-, Ost- und Westgrenze).

![Ausdehnung](fig/dc-spatial-raster/spatial_extent.png)
*Abbildung: Darstellung der räumlichen Ausdehnung eines Rasters (Quelle: NEON)*

### Auflösung (Resolution)

Die Auflösung beschreibt die Fläche am Boden, die ein einzelner Pixel abdeckt. Höhere Auflösung = kleinere Zellen = mehr Details.

![Auflösung](fig/dc-spatial-raster/raster_resolution.png)
*Abbildung: Auswirkungen unterschiedlicher Auflösung auf Rasterdarstellung (Quelle: NEON)*

## Rasterdatenformate in diesem Workshop

Wir verwenden das **GeoTIFF-Format** (`.tif`). Es enthält:

1. Ausdehnung
2. Auflösung
3. Koordinatenreferenzsystem (CRS)
4. NoData-Werte

Mehr dazu in späteren Lektionen.

## Mehrband-Rasterdaten

Ein Raster kann mehrere **Bänder** enthalten. Ein typisches Beispiel ist ein Farbbild mit drei Bändern (Rot, Grün, Blau).

![RGB Rasterbild](fig/dc-spatial-raster/RGBSTack_1.jpg)
*Abbildung: Drei-Band-RGB-Komposit eines Farbbildes (Quelle: NEON)*

Alle Bänder eines Mehrband-Rasters haben dieselbe:

* Ausdehnung
* Auflösung
* CRS

Weitere Typen von Mehrbanddaten:

1. **Zeitreihen-Raster** (z. B. Temperatur über Zeit)
2. **Multispektral- oder Hyperspektralbilder** (mehr als 4 bzw. mehr als 10 Bänder)

## Schlüsselpunkte

* Rasterdaten bestehen aus Pixeln, die mit geografischen Koordinaten verknüpft sind.
* Rasterdaten besitzen immer eine Ausdehnung und eine Auflösung.
* Die Ausdehnung gibt das geografische Gebiet an, das vom Raster abgedeckt wird.
* Die Auflösung beschreibt, wie groß jeder Pixel auf dem Boden ist.

# Einführung in Vektordaten

## Fragen

* Was sind die wichtigsten Eigenschaften von Vektordaten?
* Was ist der Unterschied zwischen Vektor- und Rasterdaten?

## Lernziele

* Vor- und Nachteile der Speicherung von Daten im Vektorformat beschreiben.
* Die drei Vektortypen benennen und passende Datenarten zuordnen können.

## Was sind Vektordaten?

Vektordaten stellen konkrete Objekte auf der Erdoberfläche dar und verknüpfen diese mit Attributen. Die Geometrie wird durch sogenannte Scheitelpunkte (x-, y-Koordinaten) definiert. Die Anordnung dieser Punkte bestimmt den Geometrietyp:

* **Punkte:** Ein einzelnes x,y-Koordinatenpaar (z. B. Messstationen, Bäume, Probeflächen).
* **Linien:** Verbundene Punkte (z. B. Straßen, Flüsse), wobei jeder Knick einen Scheitelpunkt darstellt.
* **Polygone:** Geschlossene Linien mit mindestens drei Punkten (z. B. Seen, Flächen, Ländergrenzen).

![Vektortypen](fig/dc-spatial-vector/pnt_line_poly.png)
*Abbildung: Punkte, Linien und Polygone (Quelle: NEON)*

## Datentipp

Grenzverläufe (z. B. von Ländern oder Bundesländern) können auch als Linien gespeichert sein. Diese besitzen dann jedoch keine Fläche – im Gegensatz zu Polygonen.

## Vorteile und Nachteile von Vektordaten

**Vorteile:**

* Geometrien transportieren zusätzliche Bedeutung (z. B. durch Wahl von Punkt vs. Polygon)
* Mehrere Attribute pro Objekt möglich (z. B. Stadtname, Bevölkerung)
* Speicherplatz oft effizienter als bei Rasterdaten

**Nachteile:**

* Möglicher Detailverlust gegenüber Rasterdaten
* Datenlücken je nach Erhebungsmethodik
* Komplexere Berechnungen, da Geometrie und Attribute berücksichtigt werden müssen

Vektordaten sind nicht nur in der Geoinformatik verbreitet: Auch CAD-Programme und Computergrafik arbeiten vektorbasiert – allerdings ohne Raumbezug.

## Datenformat in diesem Workshop

Wir verwenden das **Shapefile-Format** (`.shp`). Es speichert:

* **Ausdehnung** – das abgedeckte geografische Gebiet
* **Geometrietyp** – Punkte, Linien oder Polygone (nicht gemischt)
* **Koordinatenreferenzsystem (CRS)**
* **Attribute** – z. B. Namen, Höhenangaben, Kategorien

Ein Shapefile kann immer nur einen Geometrietyp enthalten.

## Herausforderung: Vektortyp erkennen

![Objekte und Ausdehnung](fig/dc-spatial-vector/spatial_extent.png)
*Abbildung: Punkt-, Linien- und Polygonobjekte mit Ausdehnungsrahmen*

Welche Objekte besitzen dieselbe Ausdehnung? Welche nicht?

### Lösung

Linien und Polygone haben dieselbe Ausdehnung. Die Punktobjekte hingegen erstrecken sich nicht so weit in vertikaler Richtung – ihr Umfang ist kleiner.

## Weiterführende Ressourcen

Mehr zu Shapefiles auf [Wikipedia](https://de.wikipedia.org/wiki/Shapefile).

## Warum nicht beides?

Die meisten Dateiformate sind entweder für Raster- oder für Vektordaten gedacht – nicht für beides gleichzeitig. Innerhalb von Vektordaten dürfen oft nur Objekte eines Typs gespeichert werden. Bei Rasterdaten ist eine Kombination unterschiedlicher Datentypen (z. B. Integer + Float) meist nicht erlaubt. Das erleichtert Standardisierung und Verarbeitung.

## Schlüsselpunkte

* Vektordaten repräsentieren Objekte mit eindeutiger Geometrie und Attributen.
* Es gibt drei Geometrietypen: Punkt, Linie und Polygon.
