# Radiant-Solution

The solution that allowed me to take 2nd place in the Radiant Earth Spot the Crop XL Challenge and 3rd place in the Radiant Earth Spot the Crop Challenge.

## Important

Thanks a lot to the Zindi team who organized this competition, and to all the participants. It was extremely interesting to take part, and a great joy to get into the winners after a hard struggle at the end.

## Disclaimer

All models were trained in Kaggle Kernel. During the solution process, more than 50 different models were built, starting with a simple CatBoostClassifier and its stratification, ending with LightAutoML.  In addition, various data samples were used. All these models have not been saved, but they can be reproduced if necessary. The best methods of building models can be seen in notebook __(create_models.ipynb)__. Also, all files with submissions have names by which you can roughly understand the method of obtaining this submission.

If you have any questions, write them to me.

__If my solution turned out to be useful for you, put a ⭐️!)__

## Solution description:

1. __(make_train_data.ipynb, make_train_data.ipynb)__ 
Converted images into csv tables. Images were loaded alternately using the **gdal** library. Next, vegetation indices were extracted for each field in the picture and their values were aggregated by the average and median value. I also tried not to take into account areas closed by clouds using the **s2cloudless** library, but this only worsened the score. 
3.__(upload it when I get home)__ 
The areas and coordinates of the fields were also calculated. But the jupyter-notebook with this process is stored on an old laptop that was left in another city. I'll upload it later.
4. __(process_ts_to_table.ipynb)__ 
After that, I translated the time series into tables on which ML models can be trained.
5. __(generate_features.ipynb)__ 
To get stronger features, I generated them in this laptop. 
  - Firstly, the days were selected in which the cloud cover was low and emissions in the calculation of vegetation indices were minimal. These days were visually selected according to the average NDVI index for all observations.
  - Next, the following set of features was generated: the rates of change of indices, std, mean, max, min, the day when the index was at the maximum and at the lows before and after the maximum, the duration from the day of the minimum to the day of the maximum, the days when the index exceeded the quantile.
6. __(generate_geo_features.ipynb)__ 
The geographical feature turned out to be quite strong (it was tested on the importance of catboost features). Therefore, I have worked through this data as well. The following features were generated: the number of fields in a given radius, labels of the nearest fields, the number of fields by class. The search for the nearest ones was carried out using the Threeball method from sklearn.
8. __(unite_data.ipynb)__ 
In this notebook, raw and aggregated data are combined into one dataset and stored in the feather format. This format saves space (it's important for mac users 😅) and speeds up file download.
9. __(create_models.ipynb)__ 
The main notebook in which the fate of my decision was decided. Initially, I worked exclusively with CatBoostClassifier, using various data samples, model parameters and stratification (KFold, StratifiedKFold). But in the last week it became clear that catboost is not able to issue a competitive account. So I decided to try (for the first time) LightAutoML. And it really boosted my score a lot. On data with geo features, it was possible to get a result of ~0.74, without geo features ~0.76.
10. __(make_sub_from_all.ipynb)__
But combining the predictions of models with geo and without geo really improved the score. The average of these solutions immediately gave a score of ~0.68. 
The main and best solution was obtained by taking the median of all the solutions received during the competition (individually they gave a score from ~0.68 to ~0.8). And damn it, it worked - __sub_all_all.csv__ gave a score of 0.67125 and a __top 3__ in this competition.
