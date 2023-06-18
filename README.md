# greenSpaceAnalysis
A project for quantifying green spaces for union councils in Karachi city, Pakistan.
 

## Using deep learning semantic segmentation model

Pixel level annotations for three vegetation classes: Tree, Shrub, Grass are made using Labelbox. A preview of the labeling interface:

<img width="896" alt="Screenshot 2023-06-12 at 9 23 13 PM" src="https://github.com/manzar-123/greenSpaceAnalysis/assets/30038903/35d766ed-2031-4fca-b56f-3f89b7d1b26b">



Raw satellite images are anquired from Google Maps API. ```` Image_location.zip ```` includes the geo-location for each downloaded/labeled image. Source images are not public. 

Manually labeled masks can be accessed at: https://drive.google.com/drive/folders/1JmGr1TuPsozN3zzU1k3Qzw-sSL1OCI_f?usp=sharing. 

The class each pixel number represents:  ````0 - Background, 1 - Tree, 2 - Shurb, 3 - Grass````.





## Using vegetation indices

The codes are borrowed from the Github repo: https://github.com/datasciencecampus/green-spaces. Compared to the source project, the changes were made in ````analyse_polygons.py````, ````calculate_indices.py````, and ````image_loaders.py````. And the goal of the changes is to skip the original image loading process which requires geo-polygon masks, instead, we directly load whole images and do vegetation analysis.


#### Command to run with vndvi index: 
````python green_spaces/analyse_polygons.py -pc 1G -i vndvi -wl "25cm RGB aerial" polygon.geojson````

#### Command to run with VARI index: 
````python green_spaces/analyse_polygons.py -pc 1G -i vari -wl "25cm RGB aerial" polygon.geojson````

#### Command to run with GLI index: 
````python green_spaces/analyse_polygons.py -pc 1G -i greenleaf -wl "25cm RGB aerial" polygon.geojson````


To adjust the threshold of the vegetation indice classifiers, change ````self.__threshold_low```` and ````self.__threshold_high```` in ````vegetation_analysis.py````



#### Input images:
The testing satellite image is put under ````in```` folder. The image name and output file name of vegetation prediction are temporarily hardcoded in ````image_loaders.py```` and ````analyse_polygons.py````. ***This is to be automated when processing multiple images.***


#### Outputs:

The output results are under ````output```` folder. Specifically, the predicted vegetation proportion is reported in ````polygon-25cm RGB aerial-vndvi-summary.txt````, and the predicted vegetation index map is stored in ````vegetation_index_HP0102.npy````, where pixel value 0 indicates vegetation absense; 1 indicates vegetation presence.
 
