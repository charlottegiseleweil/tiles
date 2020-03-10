# My Evil Hack to Host Tiles for Free: Usage 
(all commands from command line)

## Dependencies
Needs Python, GDAL, and this repo

## 1/ Make colorscale in format color.txt
With QGIS, you can export a .qml colorscale file (Layer Propertie > Style > Style (dropdown menu at the bottom) > Save style)
Use my code qml_to_colortxt.py (to make color.txt from QGIS colorscale)
```python qml\_to\_colortxt.py --qml color.qml --txt color.txt```

## 2/ Make tileset
### 2a/ Coloring step
```gdaldem color-relief raster.tif color.txt temp/colored_raster.tif ```

### 2b/ Build tiles 
``` python gdal2tilesXYZ.py -v -x -e -z 3-13 -r near temp/colored_raster.tif tileset_Folder ``` 

### Usage example
```
gdaldem color-relief temp/Aedes_pl_PEM_pop_viz.tif color_riesgo_dengue.txt temp/colored_raster.tif 
python gdal2tilesXYZ.py -v -x -e -z 3-13 -r near temp/colored_raster.tif ../tiles/amazon/Dengue_PEM_Peor_Lluvio 
``` 
## 3/ Push it to this repo
And link the corresponding URL to call your tileset in a map!
URL will be : https://charlottegiseleweil.github.io/tiles/{project}/{tileset}/{x}/{y}/{z} (I think, double check the end;) )

______


##### Notes on gdal2tiles.py
* [gdal2tiles.py readme](https://www.gdal.org/gdal2tiles.html) 
* gdal2tiles.py makes TMS tilesets. For XYZ tilesets (compatible with Leaflet) use gdal2tiles_XYZ.py with arg -x or --xyz
* -x, —xyz : additional option that allows tiles to be generated in the XYZ format
* -z : Zoom levels


