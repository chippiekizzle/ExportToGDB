# ExportToGDB
Export Rasters to a File Geodatabase in Jupyter Notebook within ArcGIS Pro

------------------------------------

Save your project on the Desktop with no spaces in the name

Remove all files from your ArcGIS Pro Contents pane (including basemaps) before running this code unless you want all of them in your GDB

Go to Insert → New Notebook, copy and paste the code below

Replace “Chippie” with your name or username (check your file pathway)

Make sure all \ are changed to /

Make sure you’re working in “Map1” in ArcGIS Pro. If not, change “Map1” below in the code to the name of your current map (“Map” or “Map2” for example)

Click Run at the top!

If this doesn’t work, you may need to manually export all .tif files to your geodatabase 

--------------------------------------------

Jupyter Notebook code in ArcGIS Pro:

import arcpy
from arcpy import env
env.workspace = "C:/Users/Chippie/Desktop/Lab10/Lab10"
outputGDB = "C:/Users/Chippie/Desktop/Lab10/Lab10/Lab10.gdb/"
aprx = arcpy.mp.ArcGISProject("current")
arcpy.CheckExtension("SPATIAL")
for m in aprx.listMaps():
    if m.name == "Map1":
        #try:
        for lyr in m.listLayers():
            print(lyr.name)
            Ras = arcpy.Raster(lyr.dataSource)
            output = "%s/%s" % (outputGDB, lyr.name)
            output = output[:-4]
            arcpy.CopyRaster_management(Ras, output)
            #arcpy.RasterToGeodatabase_conversion(Ras, "Z:/users/chippie/Lab10/Lab10.gdb")
        #except:
            #warnings
