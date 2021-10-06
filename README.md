# Radiant-Solution

The solution that allowed me to take 2nd place in the Radiant Earth Spot the Crop XL Challenge and 3rd place in the Radiant Earth Spot the Crop Challenge.

## Solution description:

1. __(make_train_data.ipynb, make_train_data.ipynb)__ Converted images into csv tables. Images were loaded alternately using the **gdal** library. Next, vegetation indices were extracted for each field in the picture and their values were aggregated by the average and median value. I also tried not to take into account areas closed by clouds using the **s2cloudless** library, but this only worsened the score. 
2. The areas and coordinates of the fields were also calculated. But the jupyter-notebook with this process is stored on an old laptop that was left in another city. I'll upload it later.
3. __(process_ts_to_table.ipynb)__ After that, I translated the time series into tables on which ML models can be trained.
4. __(generate_features.ipynb)__ To get stronger features, I generated them in this laptop. 
> Firstly, the days were selected in which the cloud cover was low and emissions in the calculation of vegetation indices were minimal. These days were visually selected according to the average NDVI index for all observations.
> Next, the following set of features was generated: the rates of change of indices, std, mean, max, min, the day when the index was at the maximum and at the lows before and after the maximum, the duration from the day of the minimum to the day of the maximum, the days when the index exceeded the quantile.
6. __(generate_geo_features.ipynb)__ The geographical feature turned out to be quite strong (it was tested on the importance of catboost features). Therefore, I have worked through this data as well. The following features were generated: the number of fields in a given radius, labels of the nearest fields, the number of fields by class. The search for the nearest ones was carried out using the Threeball method from sklearn.
7. __(unite_data.ipynb)__ In this notebook, raw and aggregated data are combined into one dataset and stored in the feather format. This format saves space (it's important for mac users 😅) and speeds up file download.
8. __(create_models.ipynb)__ 
9. __(sub_all_all.csv)__
