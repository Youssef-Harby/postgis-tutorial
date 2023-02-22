# Lesson 3

## To create a spatial table in PostGIS, you need to use SQL commands to define the table structure and the type of geometry that will be stored in the table. Here's an example of how to create a simple spatial table with a point geometry:

1. First, connect to your PostGIS database using psql or any other PostgreSQL client (the end of lesson 2).

2. Create a new table using the `CREATE TABLE` statement. In this example, we will create a table named `"my_points"` with three columns: `"id"`, `"name"`, and `"geom"`. The "geom" column will store the point geometry.
    ```sql
    CREATE TABLE public.my_points (
        id SERIAL PRIMARY KEY,
        name VARCHAR(50),
        geom GEOMETRY(POINT, 4326)
    );
    ```
    In this example, we use the **GEOMETRY** type to define the column **"geom"**. The first argument specifies the geometry type (POINT in this case), and the second argument specifies the spatial reference system (SRID) using EPSG code **4326**, which corresponds to **WGS 84** coordinate system.
3. Insert some data into the table. Here's an example of how to insert a single point:
    ```sql
    INSERT INTO public.my_points (name, geom)
    VALUES ('My Point', ST_SetSRID(ST_MakePoint(-122.419416, 37.774929), 4326));
    ```
    In this example, we use the ST_MakePoint function to create a new point with longitude -122.419416 and latitude 37.774929. We use the ST_SetSRID function to set the SRID of the point to 4326 before inserting it into the table.
4. Query the data in the table. Here's an example of how to select all points in the table:
    ```sql
    SELECT * FROM public.my_points;
    ```
    This will return a result set with one row containing the "id", "name", and "geom" columns for the point we just inserted.

    ```bash
    tutorial=# SELECT * FROM public.my_points;
    id |   name   |                        geom                        
    ----+----------+----------------------------------------------------
    1 | My Point | 0101000020E6100000D3DA34B6D79A5EC06ADC9BDF30E34240
    (1 row)
    ```
You can use similar SQL commands to create tables with other geometry types, such as LINESTRING, POLYGON, or MULTIPOINT, and insert data into them.