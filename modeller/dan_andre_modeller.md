# Særlige udtræk


Nogle eksterne og interne samarbejdspartnere får leveret særlige formater. Her til inspiration nogle af de kommandoer som bruges til dette. 


## Hele landet i én geotif, webmercator

* Til brug i ESRI
* 2,4 m opløsning
* epsg:3857
* geotiff

```
set GDAL_CACHEMAX=28000
gdalwarp -of GTiff -t_srs epsg:3857 -CO COMPRESS=DEFLATE -CO BIGTIFF=YES -r NEAR -tr 2.4 2.4 DTM_20160318.vrt g:\DK_DTM_24_20160318.tif
```

