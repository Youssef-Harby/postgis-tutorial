# Lesson 1
## What is geospatial data?

Geospatial data, also known as spatial data, refers to information that identifies the geographic location, shape, and size of a physical object or phenomenon on the earth's surface. This data can be represented in the form of maps, satellite images, aerial photographs, and other visualizations.

Geospatial data can be broadly classified into two categories: vector data and raster data. Vector data represents the world as a series of points, lines, and polygons, while raster data represents the world as a grid of pixels.

Geospatial data is used in a wide range of applications such as urban planning, transportation, environmental management, and emergency response. It can help in identifying patterns and trends, analyzing relationships between different phenomena, and making informed decisions about the use of natural resources and land. With the help of specialized tools and software, geospatial data can be visualized, analyzed, and integrated with other types of data to gain deeper insights and knowledge.


## Types of geospatial data:
There are several types of geospatial data that are used to represent different aspects of the earth's surface. The most common types of geospatial data are:

 - Point Data: Point data represents a single location on the earth's surface. This type of data is commonly used to represent features such as landmarks, cities, and other points of interest.

 - Line Data: Line data represents a series of connected points on the earth's surface. This type of data is commonly used to represent features such as roads, rivers, and coastlines.

 - Polygon Data: Polygon data represents a closed shape on the earth's surface, defined by a series of connected lines. This type of data is commonly used to represent features such as land use, administrative boundaries, and buildings.

 - Raster Data: Raster data represents the earth's surface as a grid of cells, with each cell containing a value that represents a specific attribute such as elevation, temperature, or land use.

 - 3D Data: 3D data represents the earth's surface as a three-dimensional model, allowing for more detailed analysis and visualization of features such as terrain, buildings, and infrastructure.

 - Time-Series Data: Time-series data represents changes in geospatial data over time, allowing for the analysis of trends and patterns in phenomena such as weather, land use, and urban growth.

These types of geospatial data can be combined and integrated with other data sources, such as demographic and socio-economic data, to provide a more complete picture of the earth's surface and its features.

## Specifying the spatial reference system (SRS):

When working with geospatial data, it is important to specify the spatial reference system (SRS) of the data. The SRS defines the coordinate system that is used to represent the geographic location of features on the earth's surface. Different SRSs use different units of measurement, datums, and projections to represent the earth's surface, and it is important to use the correct SRS when analyzing or visualizing geospatial data.

To specify the SRS of geospatial data, you can use a code or identifier that represents the SRS. The most common SRS codes are defined by the European Petroleum Survey Group (EPSG) and are often referred to as EPSG codes. For example, the EPSG code for the WGS84 datum, which is commonly used to represent GPS coordinates, is 4326.

In many geospatial data formats, such as shapefiles or GeoJSON files, the SRS is specified in the file metadata or in a separate file. In other cases, such as when working with a database or when processing data using software tools, you may need to explicitly specify the SRS in your code or command.

For example, when working with PostGIS, a popular geospatial database, you can specify the SRS using the ST_SetSRID function. This function sets the SRS of a geometry object to a specified EPSG code, as shown below:

```sql
SELECT ST_SetSRID(ST_MakePoint(-122.4194, 37.7749), 4326);
```
This query creates a point geometry object at the longitude and latitude (-122.4194, 37.7749) and sets its SRS to WGS84 (EPSG code 4326).