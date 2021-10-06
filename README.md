# Radiant-Solution

The solution that allowed me to take 2nd place in the Radiant Earth Spot the Crop XL Challenge and 3rd place in the Radiant Earth Spot the Crop Challenge.

## Solution description:

1. __(make_train_data.ipynb, make_train_data.ipynb)__ Converted images into csv tables. Images were loaded alternately using the **gdal** library. Next, vegetation indices were extracted for each field in the picture and their values were aggregated by the average and median value. I also tried not to take into account areas closed by clouds using the **s2cloudless** library, but this only worsened the score. 
2. The areas and coordinates of the fields were also calculated. But the jupyter-notebook with this process is stored on an old laptop that was left in another city. I'll upload it later.
3. 
