# WeRateDogs

![header_image](https://github.com/VanessaAttaFynn/WeRateDogs/blob/main/images/Untitled-1.png)

## WeRateDogs Twitter Data Wrangling Report

The data wrangling efforts in this document, were categorize into quality and tidiness issues based on the nature of the issue that is being solved.


## Quality

Opening up the **`image_predictions`** table, at a glance I spotted 2 quality issues.

1. In the columns p1, p2 and p3, breeds that have more than one word are separated by underscores

2. In the same columns some names start with caps while others are small

I fixed these issues with `.replace()` and `pandas.DataFrame.str.lower()`

I continued going through the dataset, but kept finding myself asking *"What was p1 again?"*. I quickly documented this:

3. The columns - jpg_url,p1,p1_conf,p1_dog,p2,p2_conf,p2_dog,p3,p3_conf,p3_dog - are not descriptive enough

I renamed these columns using pandas' `.rename()` function

Next I moved to my **`twitter_archive`** data where I found:

4. The source column had link tags around its content

I solved that problem by slicing of these tags with the array slicing method.

Next I found that:

5. The timestamp column had some extra +0000 which measures the milliseconds.

I found it irrelevant so I removed it in a similar way as I did with the tags in the source column.

In the twitter_archive data name column, with the `.unique()` function I found and listed invalid entries and some misspellings. I documented the issue:

6. Name column has invalid names and misspellings

This problem was resolved using the `.replace()` function. These values were replaced with `numpy.nan` for easy manipulation of null values in future works.

On assessing the twitter_archive data with the .info() and .value_counts() functions, I noticed that though the dog stage(doggo, pupper,puppo, floofer) columns had 'no null' it had the value 'None' and ‘a’ which are actually missing values.I documented this as:

7. missing data in *dog stage(doggo, pupper,puppo, floofer)* columns but recorded with *None* and *a*

This problem was solved by using the `.replace()` function and `numpy.nan`.

In the *tweets_data* table, I would be merging tweets_data with other datasets so I would need the id column to be rename as tweet_id. I quickly documented this issue as:

8. id column should be tweet_id

I used the .rename() function in pandas to handle this issue.



## Tidiness

In **twitter_archieve** table, using the .info() function I found that there were 4 columns most of its values missing and had no relevance to any analysis.

9. Drop *'idle'* columns

Using the drop function I removed these columns from the dataset.

Next, using the `.unique()` function I found that there were ratings that had invalid denominators. Now I was going to :

10. Create new rating(/10) column and drop old rating columns

I recorded the correct ratings, replaced and recalculated the ratings which sets all ratings to the standard(/10) and saved this new rating in the *rating(/10)* column and the old rating columns.

For the sake of later analysis, I needed to optimize the structure of the twitter_archive table as it had different columns for each dog stage. So the plan was to:

11. create dog stage(puppo,pupper,doggo,floofer)

I used the `.melt()` function to tranform the dataframe then removed duplicated values before merging it back into the original dataframe😎

Finally, for the last part of my data wrangling process, I wanted all my:

12. `tweets_data` and `twitter_archive` to be in the same table

I merged the two tables so I could have all my tweets and tweet info all in one dataset like I mentioned earlier!

I concluded my wrangling process by saving these 2 tables `twitter_archive_clean` and `image_preditions` in the twitter_archive_master.csv and image_prediction_master.csv files.



Thanks for Reading!!🎉

_______
