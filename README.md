# Radiant-Solution

The solution that allowed me to take 2nd place in the Radiant Earth Spot the Crop XL Challenge and 3rd place in the Radiant Earth Spot the Crop Challenge.

Solution description:

1. Converted images into csv tables. Images were loaded alternately using the **gdal** library. Next, vegetation indices were extracted for each field in the picture and their values were aggregated by the average and median value. I also tried not to take into account areas closed by clouds using the **s2cloudless** library, but this only worsened the score. 
