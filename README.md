# San Francisco Parcels and an Oakland Proposal on Tent Encampments

I recently found an news article that showed that Oakland City Council is proposing a ban on Tent Encampments within certain distances of certain kinds of buildings.

They propose banning people sleeping outside within 50 feet of Residential, Businesses, and Parks, and within 150 feet of schools.

This seemed like a de facto ban on homelessness, considering it seems like most buildings are either businesses or residential. Then I saw some folks on social media advocating for this policy in San Francisco. In a denser city like SF I imagined that this policy would be even more dramatic.

So to visualize it I made this project.

Blue areas in the map are parcels that count with regards to the policy, and the red border around a blue parcel is the "banned" sleeping area.

![](data/sf-homeless-not-allowed.png)

# Setting up the project

## Requirements

1. Data:
    On SF's data website you can find Parcel Land Use data: https://data.sfgov.org/Housing-and-Buildings/Land-Use/us3s-fp9q.

    * To get the actual data, the zipped shapefiles are here: https://data.sfgov.org/api/geospatial/us3s-fp9q?method=export&format=Shapefile
        * Unzip the file into the `data` directory and rename the parcel shape file to `sf-parcels.shp`
2. Python3

## Running

This uses python3 and Jupyter

1. First set up your virtual environment:
    ```
    $ python3 venv env
    $ source env/bin/activate
    ```
2. Next install the dependencies in `requirements.txt` with pip:
    ```
    (env) $ pip install -r requirements.txt
    ```
3. Run:
    ```
    (env) $ jupyter notebook
    [I 10:16:51.564 NotebookApp] Serving notebooks from local directory: /home/dougli1sqrd/code/sf-parcel-map-studies
    [I 10:16:51.564 NotebookApp] Jupyter Notebook 6.1.4 is running at:
    [I 10:16:51.564 NotebookApp] http://localhost:8888/?token=f7ab0f4afcef3c934e4546897df4f15eb6d970cdc582d400
    [I 10:16:51.564 NotebookApp]  or http://127.0.0.1:8888/?token=f7ab0f4afcef3c934e4546897df4f15eb6d970cdc582d400
    ```
4. Navigate to the URL provided in the log messages above once it has started. Clicking on the `sf_parcels_with_buffers.ipynb` will bring you to the notebook with the maps

## Going through the notebook

There is a section where I define functions `parse_address` and `school_func`. These are used in conjunction with a CSV of SF schools (public and private) containing addresses. The land use data does not include anything clear for "school". So I find which parcels count as schools by parsing each school address, and testing if the address falls within the range given for a parcel, and matching the street.

I create a column of `is_school` in this way on each parcel.

Later on is a function `forbidden_area` which will compute the forbidden sleeping border given a parcel. This works by calling `buffer` on the parcel geometry, expanding the area by however many meters (based on the land use, or school status). There's a catch though, from what I can tell, due to the distortion from the Mercator Projection that is common with maps, at this latitude the measured distance is about 20% more than real. So, what is actually 1000 m is written as 1200 m on the map. I was using Golden Gate Park as an example.

So while ~15 m is actually 50 ft, to accurately be shown on the map, I had to use a value 20% larger, or about 18 m in the buffer. Let me know in a ticket if this is wrong, or if there's a better way to correct for this!
