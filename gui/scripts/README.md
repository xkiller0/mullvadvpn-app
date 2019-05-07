This is a folder with the supporting scripts written in python 2, node, bash.


## Dependency installation notes

1. Run the following command in terminal to install python dependencies:
   `pip install -r requirements.txt`

2. Run `npm install -g topojson-server` to install `geo2topo` tool which is
   used by python scripts to convert GeoJSON to TopoJSON

3. Make sure you have gettext utilities installed.
   https://www.gnu.org/software/gettext/


## Geo data installation notes

Go to http://www.naturalearthdata.com/downloads/50m-cultural-vectors/ and
download ZIP files with the following shapes:

- Admin 0 – Countries
- Admin 1 – States, provinces - boundary lines
- Populated Places - simple dataset is enough

or use cURL to download all ZIPs:

```
curl -L -O https://www.naturalearthdata.com/http//www.naturalearthdata.com/download/50m/cultural/ne_50m_admin_0_countries.zip
curl -L -O https://www.naturalearthdata.com/http//www.naturalearthdata.com/download/50m/cultural/ne_50m_admin_1_states_provinces_lines.zip
curl -L -O https://www.naturalearthdata.com/http//www.naturalearthdata.com/download/10m/cultural/ne_10m_populated_places.zip
curl -L -O https://www.naturalearthdata.com/http//www.naturalearthdata.com/download/50m/cultural/ne_50m_populated_places.zip
```

Extract the downloaded ZIP files into `scripts` folder.
Make sure the following folders exist after extraction:

- ne_50m_admin_0_countries
- ne_50m_admin_1_states_provinces_lines
- ne_10m_populated_places
- ne_50m_populated_places

or use the following script:

```
unzip ne_50m_admin_0_countries.zip -d ne_50m_admin_0_countries/
unzip ne_50m_admin_1_states_provinces_lines.zip -d ne_50m_admin_1_states_provinces_lines/
unzip ne_10m_populated_places.zip -d ne_10m_populated_places/
unzip ne_50m_populated_places.zip -d ne_50m_populated_places/
```

## Geo data extraction notes

Run the following script to produce a TopoJSON data used by the app:

```
python extract-geo-data.py
```

and finally generate the R-Tree cache:

```
npx ts-node prepare-rtree.ts
```

At this point all of the data should be saved in `gui/geo-data/out` folder.

## App integration notes

Once you've extracted all the geo data, run the integration script that will
copy all files ignoring intermediate ones into the `gui/assets/geo` folder:

```
python integrate-into-app.py
```