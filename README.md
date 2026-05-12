# Course Project: Antarctica Freeboard Calculation Using ICEsat-2 and Tide Gauge

Sea ice plays a crucial role in climate regulation, ocean circulation, and ecosystem maintenance. It is commonly quantified using two key metrics: sea ice extent and thickness. Freeboard, an important indicator of sea ice thickness, represents the portion of ice above the water surface. This report estimates freeboard in Antarctica by combining ICESat-2 and tide gauge data. 

For the tide gauge data, time windows with values clearly outside the normal range were first removed. To address data jumps, an offset correction was applied based on the assumption that sea level did not change dramatically within two months before and after data jump. Anomalous spikes and outliers were then removed to obtain a smooth time series. Finally, the tide gauge data in local coordinates were converted to ellipsoid heights by incorporating benchmark and tide gauge zero information. For the ICESat-2 ATL07 data, strong beams within 3 km of the tide gauge were selected according to the satellite’s flight direction. After quality filtering, the ice surface height in ellipsoid coordinates was calculated. By combining the ellipsoid heights from both datasets, the freeboard variation trend was derived.
<img width="1388" height="710" alt="image" src="https://github.com/user-attachments/assets/773da9b1-a195-4c37-a16a-608fa032f535" />

<img width="1370" height="768" alt="image" src="https://github.com/user-attachments/assets/c6765683-6525-4e3e-ac68-66e89fbed140" />

<img width="1450" height="844" alt="image" src="https://github.com/user-attachments/assets/3c512d7c-dc90-4027-85e2-72241bcdb19f" />

<img width="1426" height="840" alt="image" src="https://github.com/user-attachments/assets/63e1626f-3960-41ab-9b44-a3bedb257442" />

The experimental results show that although freeboard exhibits a periodic variation, the presence of negative values challenges the applicability of this method. These negative values are likely attributable to the poor measurement quality of the tide gauge, which stems from a lack of maintenance and regular calibration, as well as the incomplete spatial and temporal matching between the tide gauge and ICESat-2 data. 
<img width="1106" height="1012" alt="image" src="https://github.com/user-attachments/assets/d7fc1aae-2d3f-4447-9547-04cb30d0baff" />

**Note: This serves as a course project rather than a formal research project; consequently, there may be certain limitations regarding the rigor of the methodology and the derived conclusions. For further details, please refer to the above report.**
