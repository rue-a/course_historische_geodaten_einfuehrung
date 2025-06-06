---
title: Introduction to Raster Data
teaching: 15
exercises: 10
source: Rmd
---

::::: questions
- What format should I use to represent my data?
- What are the main data types used for representing geospatial data?
- What are the main attributes of raster data?
::::::

:::::::::::::::::::::::::::::::::::::: objectives
- Describe the difference between raster and vector data.
- Describe the strengths and weaknesses of storing data in raster format.
- Distinguish between continuous and categorical raster data and identify types of datasets that would be stored in each format.
:::::




```{r, include=FALSE}
source("files/setup.R")
```

```{r load-libraries-1, results="hide", echo=FALSE, message=FALSE}
# library(raster)
# library(rgdal)
library(terra)
library(ggplot2)
```

```{r, results="hide", echo=FALSE, message=FALSE}
# load data needed to generate figures
# for demonstration only - learners do not need this data for this lesson
DSM_HARV <- rast("data/NEON-DS-Airborne-Remote-Sensing/HARV/DSM/HARV_dsmCrop.tif")

# convert to a df for plotting
DSM_HARV_df <- as.data.frame(DSM_HARV, xy = TRUE)
```

This episode introduces the two primary types of geospatial
data: rasters and vectors. After briefly introducing these
data types, this episode focuses on raster data, describing
some major features and types of raster data.

## Data Structures: Raster and Vector

The two primary types of geospatial data are raster
and vector data. Raster data is stored as a grid of values which are rendered on a
map as pixels. Each pixel value represents an area on the Earth's surface. Vector data structures represent specific features on the
Earth's surface, and
assign attributes to those features. Vector data structures
will be discussed in more detail in [the next episode]({{ base.url }}/02-intro-vector-data).

The [R for Raster and Vector Data](https://datacarpentry.org/r-raster-vector-geospatial/)
lesson will focus on how to work with both raster and vector
data sets, therefore it is essential that we understand the
basic structures of these types of data, and the types of data
that they can be used to represent.

## About Raster Data

Raster data is any pixelated (or gridded) data where each pixel is associated
with a specific geographical location. The value of a pixel can be
continuous (e.g. elevation) or categorical (e.g. land use). If this sounds
familiar, it is because this data structure is very common: it's how
we represent any digital image. A geospatial raster is only different
from a digital photo in that it is accompanied by spatial information
that connects the data to a particular location. This includes the
raster's extent and cell size, the number of rows and columns, and
its coordinate reference system (or CRS).

![](fig/dc-spatial-raster/raster_concept.png){alt='Raster Concept'}

Source: National Ecological Observatory Network (NEON)
{: .text-center}

Some examples of continuous rasters include:

1. Precipitation maps.
2. Maps of tree height derived from LiDAR data.
3. Elevation values for a region.

A map of elevation for Harvard Forest derived from the [NEON AOP LiDAR sensor](https://www.neonscience.org/data-collection/airborne-remote-sensing)
is below. Elevation is represented as continuous numeric variable in this map. The legend
shows the continuous range of values in the data from around 300 to 420 meters.

```{r elevation-map, echo=FALSE}
# render DSM for tutorial content background
# for demonstration only, code not shown
ggplot() +
  geom_raster(data = DSM_HARV_df , aes(x = x, y = y, fill = HARV_dsmCrop)) +
  ggtitle("Continuous Elevation Map - NEON Harvard Forest Field Site") +
  coord_quickmap()
```

Some rasters contain categorical data where each pixel represents a discrete
class such as a landcover type (e.g., "forest" or "grassland") rather than a
continuous value such as elevation or temperature. Some examples of classified
maps include:

1. Landcover / land-use maps.
2. Tree height maps classified as short, medium, and tall trees.
3. Elevation maps classified as low, medium, and high elevation.

![](fig/USA_landcover_classification.png){alt='USA landcover classification'}

The map above shows the contiguous United States with landcover as categorical
data. Each color is a different landcover category. (Source: Homer, C.G., et
al., 2015, Completion of the 2011 National Land Cover Database for the
conterminous United States-Representing a decade of land cover change
information. Photogrammetric Engineering and Remote Sensing, v. 81, no. 5, p.
345-354)

```{r classified-elevation-map, echo=FALSE, warning=FALSE, message=FALSE}
# Load raster into R
DSM_HARV <- rast("data/NEON-DS-Airborne-Remote-Sensing/HARV/DSM/HARV_dsmCrop.tif")

# convert to a df for plotting in two steps,
# First, to a SpatVector of points
DSM_HARV_pts <- as.points(DSM_HARV)
# Then to a 'conventional' dataframe
DSM_HARV_df  <- as.data.frame(DSM_HARV_pts, geom="XY", xy=TRUE)

library(ggplot2)
library(dplyr)

DSM_HARV_df <- DSM_HARV_df %>%
  mutate(fct_elevation = cut(HARV_dsmCrop, 3,
                             labels = c("Low Elevation", "Middle Elevation",
                                        "High Elevation")
                             )
         )

ggplot() +
  geom_raster(data = DSM_HARV_df , aes(x = x, y = y, fill = fct_elevation)) +
  ggtitle("Classified Elevation Map - NEON Harvard Forest Field Site") +
  coord_equal()
```

The map above shows elevation data for the NEON Harvard Forest field
site. We will be working with data from this site later in the workshop.
In this map, the elevation data (a continuous variable) has been divided
up into categories to yield a categorical raster.

:::::::::::::::::::::::::::::::::::::::  challenge

## Advantages and Disadvantages

With your neighbor, brainstorm potential advantages and
disadvantages of storing data in raster format. Add your
ideas to the Etherpad. The Instructor will discuss and
add any points that weren't brought up in the small group
discussions.

:::::::::::::::  solution

## Solution

Raster data has some important advantages:

- representation of continuous surfaces
- potentially very high levels of detail
- data is 'unweighted' across its extent - the geometry doesn't
  implicitly highlight features
- cell-by-cell calculations can be very fast and efficient

The downsides of raster data are:

- very large file sizes as cell size gets smaller
- currently popular formats don't embed metadata well (more on this later!)
- can be difficult to represent complex information
  
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Important Attributes of Raster Data

### Extent

The spatial extent is the geographic area that the raster data covers.
The spatial extent of an R spatial object represents the geographic edge or
location that is the furthest north, south, east and west. In other words, extent
represents the overall geographic coverage of the spatial object.

![](fig/dc-spatial-raster/spatial_extent.png){alt='Spatial extent image'}

(Image Source: National Ecological Observatory Network (NEON))
{: .text-center}


### Resolution

A resolution of a raster represents the area on the ground that each
pixel of the raster covers. The image below illustrates the effect
of changes in resolution.

![](fig/dc-spatial-raster/raster_resolution.png){alt='Resolution image'}

(Source: National Ecological Observatory Network (NEON))
{: .text-center}

## Raster Data Format for this Workshop

Raster data can come in many different formats. For this workshop, we will use
the GeoTIFF format which has the extension `.tif`. A `.tif` file stores metadata
or attributes about the file as embedded `tif tags`. For instance, your camera
might store a tag that describes the make and model of the camera or the date
the photo was taken when it saves a `.tif`. A GeoTIFF is a standard `.tif` image
format with additional spatial (georeferencing) information embedded in the file
as tags. These tags should include the following raster metadata:

1. Extent
2. Resolution
3. Coordinate Reference System (CRS) - we will introduce this concept in [a
  later episode]({{ base.url }}/03-crs)
4. Values that represent missing data (`NoDataValue`) - we will introduce this
  concept in [a later lesson](https://datacarpentry.org/r-raster-vector-geospatial/01-raster-structure/index.html).

We will discuss these attributes in more detail in [a later
lesson](https://datacarpentry.org/r-raster-vector-geospatial/01-raster-structure/index.html).
In that lesson, we will also learn how to use R to extract raster attributes
from a GeoTIFF file.

:::::::::::::::::::::::::::::::::::::::::  callout

## More Resources on the  `.tif` format

- [GeoTIFF on Wikipedia](https://en.wikipedia.org/wiki/GeoTIFF)
- [OSGEO TIFF documentation](https://trac.osgeo.org/geotiff/)
  

::::::::::::::::::::::::::::::::::::::::::::::::::

## Multi-band Raster Data

A raster can contain one or more bands. One type of multi-band raster
dataset that is familiar to many of us is a color
image. A basic color image consists of three bands: red, green, and blue.
Each
band represents light reflected from the red, green or blue portions of
the
electromagnetic spectrum. The pixel brightness for each band, when
composited
creates the colors that we see in an image.

![](fig/dc-spatial-raster/RGBSTack_1.jpg){alt='RGB multi-band raster image'}

(Source: National Ecological Observatory Network (NEON).)
{: .text-center}

We can plot each band of a multi-band image individually.

```{r demonstrate-RGB-Image, echo=FALSE}
library(terra)
# Use stack function to read in all bands
RGB_stack_HARV <- rast("data/NEON-DS-Airborne-Remote-Sensing/HARV/RGB_Imagery/HARV_RGB_Ortho.tif")

names(RGB_stack_HARV) <- c("Red Band", "Green Band", "Blue Band")

grayscale_colors <- gray.colors(100,
start = 0.0,
end = 1.0,
gamma = 2.2,
alpha = NULL)

# Create an RGB image from the raster stack
plot(RGB_stack_HARV,
col = grayscale_colors,
axes = FALSE)

```

Or we can composite all three bands together to make a color image.

```{r plot-RGB-now, echo=FALSE, message=FALSE}
# Create an RGB image from the raster stack

original_par <- par() # create original par for easy reversal at end
par(col.axis = "white", col.lab = "white", tck = 0)
plotRGB(RGB_stack_HARV, r = 1, g = 2, b = 3,
axes = TRUE,
main = "3 Band Color Composite Image\n NEON Harvard Forest Field Site")
box(col = "white")

```

In a multi-band dataset, the rasters will always have the same extent,
resolution, and CRS.

```{r reset-par, echo=FALSE, results="hide", warning=FALSE}
par(original_par) # go back to original par
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Other Types of Multi-band Raster Data

Multi-band raster data might also contain:

1. **Time series:** the same variable, over the same area, over time.
  We will be working with time series data in the [Raster Time Series Data in R](https://datacarpentry.org/r-raster-vector-geospatial/12-time-series-raster/index.html) episode.
2. **Multi or hyperspectral imagery:** image rasters that have 4 or
  more (multi-spectral) or more than 10-15 (hyperspectral) bands. We
  won't be working with this type of data in this workshop, but you can
  check out the NEON Data Skills
  [Imaging Spectroscopy HDF5 in R](https://www.neonscience.org/hsi-hdf5-r)
  tutorial if you're interested in working with hyperspectral data cubes.
  

::::::::::::::::::::::::::::::::::::::::::::::::::



:::::::::::::::::::::::::::::::::::::::: keypoints

- Raster data is pixelated data where each pixel is associated with a specific location.
- Raster data always has an extent and a resolution.
- The extent is the geographical area covered by a raster.
- The resolution is the area covered by each pixel of a raster.

::::::::::::::::::::::::::::::::::::::::::::::::::


