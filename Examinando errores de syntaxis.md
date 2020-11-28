Modificacion de listfc


```python
import archook
archook.get_arcpy()
```


```python
import arcpy
from arcpy import env
env.workspace = "C:/EsriPress/Python/Data/Exercise11"
fclist = arcpy.ListFeatureClasses()
for fc in fclist
    desc = arcpy.describe(fc)
    print desc.basename + ": " + des.shapeType
```


      File "<ipython-input-7-dc0ca99c59fe>", line 5
        for fc in fclist
                        ^
    SyntaxError: invalid syntax
    



```python
import arcpy
from arcpy import env
env.workspace = "C:/EsriPress/Python/Data/Exercise11"
fclist = arcpy.ListFeatureClasses()
for fc in fclist:
    desc = arcpy.describe(fc)
    print desc.basename + ": " + des.shapeType
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-8-abf275e02eea> in <module>()
          4 fclist = arcpy.ListFeatureClasses()
          5 for fc in fclist:
    ----> 6     desc = arcpy.describe(fc)
          7     print desc.basename + ": " + des.shapeType
    

    AttributeError: 'module' object has no attribute 'describe'



```python
import arcpy
from arcpy import env
env.workspace = "C:/EsriPress/Python/Data/Exercise11"
fclist = arcpy.ListFeatureClasses()
for fc in fclist:
    desc = arcpy.Describe(fc)
    print desc.basename + ": " + des.shapeType
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-10-d404db61b887> in <module>()
          5 for fc in fclist:
          6     desc = arcpy.Describe(fc)
    ----> 7     print desc.basename + ": " + des.shapeType
    

    NameError: name 'des' is not defined



```python
import arcpy
from arcpy import env
env.workspace = "C:/EsriPress/Python/Data/Exercise11"
fclist = arcpy.ListFeatureClasses()
for fc in fclist:
    desc = arcpy.Describe(fc)
    print desc.basename + ": " + desc.shapeType
```

    bike_routes: Polyline
    county: Polygon
    facilities: Point
    parks: Polygon
    

### Debugging 

Debe hacerse en pywin u otra IDE


```python
import arcpy
import os
from arcpy import env
env.workspace = "C:/EsriPress/Python/Data/Exercise11"
fclist = arcpy.ListFeatureclasses()
for fc in fclist:
    desc = arcpy.Describe(fc)
    arcpy.CopyFeatures_management(fc, os.path.join("Results/study.mdb", desc.basename))
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-12-4be3f4e8338f> in <module>()
          3 from arcpy import env
          4 env.workspace = "C:/EsriPress/Python/Data/Exercise11"
    ----> 5 fclist = arcpy.ListFeatureclasses()
          6 for fc in fclist:
          7     desc = arcpy.Describe(fc)
    

    AttributeError: 'module' object has no attribute 'ListFeatureclasses'



```python
from arcpy import env
env.workspace = "C:/EsriPress/Python/Data/Exercise11"
fclist = arcpy.ListFeatureClasses()
for fc in fclist:
    desc = arcpy.Describe(fc)
    arcpy.CopyFeatures_management(fc, os.path.join("Results/study.mdb", desc.basename))
```


```python
import arcpy
import os
from arcpy import env
env.workspace = "C:/EsriPress/Python/Data/Exercise11"
fclist = arcpy.ListFeatureClasses()
for fc in fclist:
    desc = arcpy.Describe(fc)
    arcpy.CopyFeatures_management(fc, os.path.join("Results/mydata.mdb", desc.basename))
```


    ---------------------------------------------------------------------------

    ExecuteError                              Traceback (most recent call last)

    <ipython-input-15-aee5f6e2d1bc> in <module>()
          6 for fc in fclist:
          7     desc = arcpy.Describe(fc)
    ----> 8     arcpy.CopyFeatures_management(fc, os.path.join("Results/mydata.mdb", desc.basename))
    

    C:\Program Files (x86)\ArcGIS\Desktop10.8\arcpy\arcpy\management.py in CopyFeatures(in_features, out_feature_class, config_keyword, spatial_grid_1, spatial_grid_2, spatial_grid_3)
       2578         return retval
       2579     except Exception as e:
    -> 2580         raise e
       2581 
       2582 @gptooldoc('DeleteFeatures_management', None)
    

    ExecuteError: ERROR 000210: Cannot create output Results/mydata.mdb\bike_routes
    Failed to execute (CopyFeatures).
    


Modificando el codigo


```python
import arcpy, os
from arcpy import env

try: 
    env.workspace = "C:/EsriPress/Python/Data/Exercise11"
    fclist = arcpy.ListFeatureClasses()
    for fc in fclist:
        desc = arcpy.Describe(fc)
        arcpy.CopyFeatures_management(fc, os.path.join("Results/mydata.mdb", desc.basename))
except arcpy.ExecuteError:
    print arcpy.GetMessages(2)
except:
    print "There has been a nontoll error"
    
```

    ERROR 000210: Cannot create output Results/mydata.mdb\bike_routes
    Failed to execute (CopyFeatures).
    
    
