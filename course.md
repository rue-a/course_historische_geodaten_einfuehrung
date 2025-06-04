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
