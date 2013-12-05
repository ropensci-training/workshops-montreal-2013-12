### spocc - Make some maps!

### Load libraries


```r
library(spocc)
library(rCharts)
```


### spocc unifies access to biodiversity data across sources


```r
out <- occ(query = "Accipiter striatus", from = "gbif")
out@gbif@data  # a data.frame
```

```
##                                 name       key longitude latitude prov
## 1  Accipiter striatus Vieillot, 1808 773408845    -97.28   32.876 gbif
## 2  Accipiter striatus Vieillot, 1808 768992325    -76.10    4.724 gbif
## 3  Accipiter striatus Vieillot, 1808 773414146   -122.27   37.771 gbif
## 4  Accipiter striatus Vieillot, 1808 773440541    -98.00   32.800 gbif
## 5  Accipiter striatus Vieillot, 1808 773423188    -76.54   38.688 gbif
## 6  Accipiter striatus Vieillot, 1808 773432602   -122.78   38.613 gbif
## 7  Accipiter striatus Vieillot, 1808 773430206   -117.06   32.552 gbif
## 8  Accipiter striatus Vieillot, 1808 833024105   -105.16   40.678 gbif
## 9  Accipiter striatus Vieillot, 1808        NA        NA       NA gbif
## 10 Accipiter striatus Vieillot, 1808 579130954    -74.44   40.541 gbif
## 11 Accipiter striatus Vieillot, 1808 579131911    -76.70   39.889 gbif
## 12 Accipiter striatus Vieillot, 1808 579132307    -75.55   39.605 gbif
## 13 Accipiter striatus Vieillot, 1808 579134716    -96.98   32.641 gbif
## 14 Accipiter striatus Vieillot, 1808 579138808    -73.57   41.003 gbif
## 15 Accipiter striatus Vieillot, 1808 579149929   -123.96   49.236 gbif
## 16 Accipiter striatus Vieillot, 1808 579157816    -70.40   41.685 gbif
## 17 Accipiter striatus Vieillot, 1808 579125251    -84.13   33.976 gbif
## 18 Accipiter striatus Vieillot, 1808 579127561    -90.07   30.015 gbif
## 19 Accipiter striatus Vieillot, 1808 579128452   -105.21   39.666 gbif
## 20 Accipiter striatus Vieillot, 1808 818461023   -111.73   33.361 gbif
```

```r
out@ebird@data  # empty
```

```
## data frame with 0 columns and 0 rows
```

```r
out@gbif@meta  #  metadata, your query parameters, time the call executed, etc. 
```

```
## $source
## [1] "gbif"
## 
## $time
## [1] "2013-12-05 10:29:25 PST"
## 
## $query
## [1] "Accipiter striatus"
## 
## $type
## [1] "sci"
## 
## $opts
## $opts$taxonKey
## [1] 2480612
## 
## $opts$return
## [1] "data"
```


And you can squash together data from sources easily


```r
out <- occ(query = "Accipiter striatus", from = c("gbif", "bison"))
occtodf(out, "data")
```

```
##                                 name longitude latitude  prov
## 1  Accipiter striatus Vieillot, 1808    -97.28   32.876  gbif
## 2  Accipiter striatus Vieillot, 1808    -76.10    4.724  gbif
## 3  Accipiter striatus Vieillot, 1808   -122.27   37.771  gbif
## 4  Accipiter striatus Vieillot, 1808    -98.00   32.800  gbif
## 5  Accipiter striatus Vieillot, 1808    -76.54   38.688  gbif
## 6  Accipiter striatus Vieillot, 1808   -122.78   38.613  gbif
## 7  Accipiter striatus Vieillot, 1808   -117.06   32.552  gbif
## 8  Accipiter striatus Vieillot, 1808   -105.16   40.678  gbif
## 9  Accipiter striatus Vieillot, 1808        NA       NA  gbif
## 10 Accipiter striatus Vieillot, 1808    -74.44   40.541  gbif
## 11 Accipiter striatus Vieillot, 1808    -76.70   39.889  gbif
## 12 Accipiter striatus Vieillot, 1808    -75.55   39.605  gbif
## 13 Accipiter striatus Vieillot, 1808    -96.98   32.641  gbif
## 14 Accipiter striatus Vieillot, 1808    -73.57   41.003  gbif
## 15 Accipiter striatus Vieillot, 1808   -123.96   49.236  gbif
## 16 Accipiter striatus Vieillot, 1808    -70.40   41.685  gbif
## 17 Accipiter striatus Vieillot, 1808    -84.13   33.976  gbif
## 18 Accipiter striatus Vieillot, 1808    -90.07   30.015  gbif
## 19 Accipiter striatus Vieillot, 1808   -105.21   39.666  gbif
## 20 Accipiter striatus Vieillot, 1808   -111.73   33.361  gbif
## 21                Accipiter striatus    -72.50   42.774 bison
## 22                Accipiter striatus    -72.50   42.769 bison
## 23                Accipiter striatus    -72.50   42.769 bison
## 24                Accipiter striatus    -72.50   42.769 bison
## 25                Accipiter striatus    -72.50   42.769 bison
## 26                Accipiter striatus    -72.50   42.769 bison
## 27                Accipiter striatus    -72.50   42.769 bison
## 28                Accipiter striatus    -72.50   42.769 bison
## 29                Accipiter striatus    -72.50   42.769 bison
## 30                Accipiter striatus    -72.50   42.769 bison
```



### Make a map using Shiny locally (uses rCharts)

Try changing the species names to whatever you like and press **Submit**

Or change the background map, or the color palette. 


```r
mapshiny()
```



### Make a map using rCharts


```r
spp <- c("Danaus plexippus", "Accipiter striatus", "Pinus contorta")
dat <- occlist(query = spp, from = "gbif", gbifopts = list(georeferenced = TRUE))
dat <- occtodfspp(dat, "data")
maprcharts(data = dat)
```



### Make a map using GitHub gists

If you have a Github Account, you can get an interactive map on Github in one line of code. The map will open in your default browser. 


```r
mapgist(data = dat, color = c("#976AAE", "#6B944D", "#BD5945"))
```

