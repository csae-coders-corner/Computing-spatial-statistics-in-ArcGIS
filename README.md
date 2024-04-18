![CC Graphics 2024_Spatialstatistics](https://github.com/csae-coders-corner/Computing-spatial-statistics-in-ArcGIS/assets/148211163/69603a18-1e3e-4543-a4fc-643a62b3465e)

# Computing-spatial-statistics-in-ArcGIS
ArcGIS is a powerful (albeit oft-temperamental) piece of software, which can be used to do any and all spatial data manipulation. For example, you can use ArcGIS to find the shortest distance between any two cities embedded in a network, to calculate the number of hospitals within a radius around a location, or to join data sets at different underlying geographies. But, to utilize its full power and produce reproducible work, it’s necessary to code in it. You can write scripts to run using ArcGIS with python and ArcGIS’s “arcpy” package. To do this you will first need to download python, I highly recommend using anaconda for this, and an IDE for which I recommend pycharm.

I’ll use an example to walk through the setup and illustrate how simple spatial statistics can be computed using ArcGIS and python. In this example I’m interested in calculating average potential crop yields in each Commune of Benin over time. [^1]

>[^1]: In Benin, Communes are the second administrative division.

To do this I’ve downloaded a .csv file from GAEZ which consists of meta data (i.e. year crop type) and a link to the .tif file of yields in raster format. Raster basically means an image, in this case an image with roughly 9x9km pixels.[^2] My problem is that I’m interested in yields at a coarser geography[^3], and only in Benin. Thus, the plan is to loop over each data-set, calculate the average yield within each Commune and export a spreadsheet of this information for each year and crop. In short, I want to convert the upper excel file depicted below which contains links to each .tif file into a series of excel files that look like the lower one which contains information on mean yields by crop by commune (that is by geolevel2).

>[^2]: Pixels are 5 arc-minute (about 9 x 9 km at the equator) grid cells.
>[^3]: That is, I’m interested in calculating yields at the commune level which comprises of several (many) pixels.

![ArcGIS 1](https://github.com/csae-coders-corner/Computing-spatial-statistics-in-ArcGIS/assets/148211163/37bef47b-8e72-473d-923c-0fe361067126)

First, we import packages including arcpy and some other python packages that are needed for the example. Then we set some parameters, including the parallelisation, over-write (whether we overwrite existing files or not) and the home directory as well as “checking out” the necessary extensions in ArcGIS.

![ArcGIS 2](https://github.com/csae-coders-corner/Computing-spatial-statistics-in-ArcGIS/assets/148211163/0a645daa-1013-4753-8042-39b0878b7639)

Having dealt with the housekeeping above we turn to the code proper which is given below. The code is annotated to explain what each line is doing. We loop over each row in the excel file, extract meta information, and then download the associated dataset using the link provided. Once downloaded we perform the spatial operation “ZonalStatistic-sAsTable” which calculates the mean yield across pixels in each of the larger communes in Benin. This command can generate a wide variety of statistics other than the mean. For example, if we are interested in the maximum value, we can change ’MEAN’ in line 55 of the code below to say ’MAX’. Finally, I export the extracted information to a .csv file.

![ArcGIS 3](https://github.com/csae-coders-corner/Computing-spatial-statistics-in-ArcGIS/assets/148211163/f0c4b4ea-e619-422e-b267-bfb4d24d2fdb)

**Luke Milsom, DPhil candidate in the Department of Economics, University of Oxford, 
08 December 2021**
