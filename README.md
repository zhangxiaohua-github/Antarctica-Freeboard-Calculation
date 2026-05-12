# Project: Antarctica Freeboard Calculation
For tide gauge sites on Antarctica, calculate freeboard using ICESAT-2 and tide gauge.
Extension:
(1)Comparing results with GNSS-IR and tide gauge
(2)Generating freeboard within 25 km away from coast using SSH model and tide gauge, linking to ICESAT-2 ATL10 (> 25 km freeboard) to have a whole freeboard coverage of Antarctica

## Tide Gauge data
### TG data source
(1) GLOSS/IOC 
website: https://www.ioc-sealevelmonitoring.org

|     Station Name      |Time Coverage|   Sensor Type   |Completeness(%)|Benchmark|Co-GNSS |     lat, lon     | link |
|:--------------------: |:-----------:|:---------------:|:-------------:|:-------:|:-----: |:---------------: | :--: |
|        ROTHERA        | 2015 - 2026 | Pressure + Radar|       89      |   Yes   |   Yes  |-67.5667, -68.1333| https://www.ioc-sealevelmonitoring.org/station.php?code=rothe |
|ARGENTINE ISLANDS(vern)| 2008 - 2026 | Pressure + Radar|       98      |   Yes   |   Yes  |-65.25  , -64.27  | https://www.ioc-sealevelmonitoring.org/station.php?code=vern | 
|    PUERTO SOBERANIA   | 2013 - 2026 | Pressure + Radar|       56      |   Yes   |   Yes  |-62.4793, -59.6629| https://www.ioc-sealevelmonitoring.org/station.php?code=prat3 | 
|	  ohig3         | 2020 - 2026 | Pressure + Radar|       48      |    NO   |    NO  |-63.3203, -57.8987| https://www.ioc-sealevelmonitoring.org/station.php?code=ohig3 | 
|         SYOWA         | 2008 - 2026 |      Pressure   |       93      |    NO   |   Yes  |-69.0078, 39.5703 | https://www.ioc-sealevelmonitoring.org/station.php?code=syow | 
|    DUMONT D'URVILLE   | 2008 - 2026 |      Pressure   |       55      |    NO   |   Yes  |-66.6519, 140.0017| https://ioc-sealevelmonitoring.org/station.php?code=dumo | 


Note: 
- Benchmark information and Co-GNSS are needed to be checked on PSMSL
website: https://psmsl.org/data/obtaining/

- ohig3 is not shown on PSMSL

- SYOWA is metric station.
Here, PSMSL has two kinds of station, metric and RLR (Revised Local Reference).
RLR: This TG station data has time series with a uniform tide gauge zero. 
     The process method of PSMSL is locatd at the benchmarh with 7000 mm below.
     And benchmark also have the leveling information.

Metric: This TG station data has time series with raw data, no a uniform tide gauge zero. 
        Do not know the tide gauge zero. 
        So we can not trust the absolute height unless tide gauge zero can be determined, but still can use its relative height to do harmonic analysis.

- SYOWA TG data for 1988 onwards are from a differential pressure sensor and are automatically corrected for air pressure; having a fixed benchmark of TGBM 1040, is principally re-measured on Jan. However, the levelling information is very irregular (means the information of TGBM 1040 is not sufficient). Under this situdation, the solution is that if we know the benchmark information, we can set a tide gauge zero, then we have a uniform standards. However, we can not know the benchmark information.

(2) geodesy.linz.govt.nz 
maintained by New Zeland, including two tide gauges in Antarctica.
https://www.linz.govt.nz/products-services/data/types-linz-data/sea-level-data/sea-level-data-downloads

|Station Name|Time Coverage|Sensor Type|Completeness(%)|         Benchmark     |Co-GNSS |     lat, lon     |
|:----------:|:-----------:|:---------:|:-------------:|:---------------------:|------- |:---------------: |
|    ROBT    | 2007 - 2025 |  Pressure |      good     |LINZ geodetic code B93M|checking|-77.0333, 163.1833|
|    SCOT    | 2016 - 2025 |   unknown |      good     |LINZ geodetic code DJRB|checking|-77.8500, 166.7667|


### Download TG data
For GLOSS, we can use C11 to download data; but for LINZ data, we should mannually download from https://www.linz.govt.nz/products-services/data/types-linz-data/sea-level-data/sea-level-data-downloads.

### Process TG data
1. tide gauge sensor type



## ICEsat-2 
### Introduction
information from: https://nsidc.org/data/atl07/versions/1

1. ICESat-2 elevation data include observations from 2018 to present. ATLAS is its core sensor.
Types of altimetry data include:

Land ice height
Sea ice height
Land and vegetation height
Sea ice freeboard
Ocean surface height
Inland water surface data

2. Products:
ATL06:
ATL07: 
ATL08: 
ATL10:
ATL12:
ATL13:

3. ATLAS equipment on ICEsat-2 simultaneously emits 6 laser beams arranged in three pairs. Each pair includes one strong and one weak beams. This means that when satellite travels over an area, this 6 beams will simultaneously scan land surface. 
  
4. ICEsat-2 ATL07 structure
ICEsat-2 has two versions: v6 and v7. They have different revisions, v6 has 4 revisions and v7 has 2 revisions (shown on the B1).

But the structure is not related to revisions. Although v6 has 4 revisions, but they share the same structure.

This is to say, there are only three different data structure. v6 has the 1st kind of structure, and v7 have two different data structure, but this sturcture is not related to its revisions cause we found the two files could have different structure although with the same 007rr.

5. ATLAS orientation and beams
sc_orient=1 (Forward):  GT1R, GT2R, GT3R are strong
sc_orient=0 (Backward): GT1L, GT2L, GT3L are strong

6. Plot tracks
ICESat-2 reference ground tracks with dates and times can be downloaded as KMZ files from NASA's ICESat-2 | Technical Specs page,
below the Orbit and Coverage table.

### check ICEsat-2 around TG
we firstly determine if ICEsat-2 tracks around existing some stations 
website: NSIDC  https://nsidc.org/data/icesat-2/products 

(1) GLOSS/IOC 
|   Station Name    | Exsiting ICEsat-2 | distance to the closet tracks |
| :---------------: | :---------------: | :---------------------------: |
|      ROTHERA      |        Yes        |         about 5 km            |
| ARGENTINE ISLANDS |        Yes        |         about 5 km            |
| PUERTO SOBERANIA  |        Yes        |         about 1 km            | 
|      ohig3        |        Yes        |         about 2 km            |
|      SYOWA        |        Yes        |         about 2 km            |
| DUMONT D'URVILLE  |        Yes        |         about 1 km            | 

(2) geodesy.linz.govt.nz
| Station Name |Exsiting ICEsat-2 | distance to the closet tracks |
| :----------: |:---------------: | :---------------------------: |
|     ROBT     |        Yes       |          about 2 km           |
|     SCOT     |        Yes       |          about 5 km           | 

### Download ICEsat-2
I downloaded ICEsat-2 around 8 stations.

          station  granules_queried  files_downloaded  files_per_granule 
          ROTHERA                73               221                3.0 
ARGENTINE_ISLANDS                76               204                2.7 
 PUERTO_SOBERANIA                57               192                3.4 
            OHIG3               103               258                2.5 
            SYOWA                89               288                3.2 
  DUMONT_DURVILLE               105               305                2.9 
             ROBT               198               524                2.6 
             SCOT               196               547                2.8 
 
### Process ICEsat-2 ATL07
1. determine data structure 

2. Extract height from ICEsat-2 ATL07
Extract `height_segment_height` from sample files of all three structural variants,
applying the following quality control filters:

| Level | Field | Filter |
|---|---|---|
| Granule | `qa_granule_pass_fail` | == 0 (pass) |
| Beam | `sc_orient` | selects strong beams only |
| Segment | `height_segment_quality` | == 1 (good) |
| Segment | `height_segment_type` | -1 = off_pointing, 0 = could, 1 = ice, 2~9 = lead |
| Segment | `height_segment_ssh_flag` | 0 = ice surface, 1 = sea surface (lead) , -1 = fill value|

**Strong beam mapping by `sc_orient`:**
- `sc_orient = 1` (Forward):  GT1R, GT2R, GT3R are strong
- `sc_orient = 0` (Backward): GT1L, GT2L, GT3L are strong

**sea_ice** = height_segment_ssh_flag == 0 && height_segment_type == 1
cause even height_segment_ssh_flag == 0, height_segment_type still could be -1, 0, 2-9 which should be ignored.

Therefore, extract quality-filtered sea ice height segments from one .h5 file.
    Filters:
      1. qa_granule_pass_fail == 0
      2. Strong beams only (determined by sc_orient)
      3. height_segment_quality == 1
      4. height_segment_type == 1  (sea ice surface only)
      5. height_segment_ssh_flag == 0  (sea ice, not sea surface)
      6. height_segment_height < HEIGHT_VALID_MAX  (remove fill values)
      7. Within radius_km of station center

## Unify to Ellipsoid

                        ELLIPSOIDAL LINKS FOR RLR DATA

PSMSL are able to publish estimates of the height of our RLR data above a
reference ellipsoid (GRS80) in some cases, where a permanent GNSS station has 
been installed near the tide gauge, and the two instruments have been connected
through levelling. In these cases the link is listed on the station's RLR
diagram page. Estimates are provided by Système d'Observation du Niveau des 
Eaux Littorales (SONEL). Full details are included at the page

http://www.psmsl.org/data/obtaining/ellipsoid.php

The zip files contain a file (ellipsoidal_links.csv) that lists the stations
for which such a link has been made.

1. The ellipsoid height of RLR or benchmark of TG
(1) ROTHERA
RLR Ellipsoid information: https://psmsl.org/data/obtaining/rlr.diagrams/1931.php
The ellipsoid height of RLR datum above the reference ellipsoid:

(2) ARGENTINE ISLANDS(vern)
NO

(3) PUERTO SOBERANIA 
No

(4) ohig3
No

(5) SYOWA
No

(6) DUMONT D'URVILLE
No

(7) ROBT
https://www.geodesy.linz.govt.nz/gdb/  B93M

REFERENCE BENCH MARKS		
----------------------		  
CAPE ROBERTS TGBM1, LINZ geodetic code B93M   Ellipsoidal height (m):  	-54.586
ROB3, LINZ geodetic code ROB3 

SUMMARY OF TIDE GAUGE ZERO BELOW B93M (metres)
-----------------------------------------------

Calibration Date:	Value (m):
December 1991		7.668
December 1992		7.824
November 1994		8.992
December 1996		9.015
November 2000		8.556
January  2002		8.446
December 2002		8.332
December 2003		8.336
November 2004		8.307
November 2005		8.327
November 2006		8.318
November 2007 		8.310
November 2008 		8.234
November 2011		7.993
November 2012		8.022
November 2013		8.019
November 2014		7.997
November 2015		8.075
December 2016		8.050		
November 2017		8.013
November 2018		8.215
October  2019		9.534 - unreliable
November 2021		7.766
November 2022		7.726
November 2023		7.691
November 2024		7.768
November 2025  		7.820

(8) SCOT
https://www.geodesy.linz.govt.nz/gdb/  DJRB Ellipsoidal height (m):  	-44.748

REFERENCE BENCH MARKS		
----------------------		  
BM A, LINZ geodetic code DJRB  

===========================================================

SUMMARY OF TIDE GAUGE ZERO (TG0) BELOW DJRB (metres)
-----------------------------------------------

Calibration Date

December 2016	11.364
November 2017	11.369
November 2018	11.573
November 2019	11.232
November 2020	11.409
November 2021	11.533
November 2022	11.678
November 2023	11.698
November 2024	11.934
November 2025 	11.067