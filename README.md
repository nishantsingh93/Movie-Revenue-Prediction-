# Revenue Prediction of TMDB Movie dataset
******************************************************************************************************************************
******************************************************************************************************************************
### I. Introduction:

**Dataset:** 
This Project aims at predicting revenue of movies using supervised learning approach. The [TMDB](https://www.kaggle.com/tmdb/tmdb-movie-metadata/data) dataset contains around 5000 movies and TV series. It is one of the biggest movie database on the web available. The dataset is divided into csv files and many columns are in json format.


**Objective:** 
Given the information  about a movie such as release month, cast, budget, film review, director, production house, language can we predict the total gross revenue for that movie? However by analyzing revenues generated by previous movies, one can build a model which can help us predict the expected revenue for a movie. Such a prediction could bevery useful for the movie studio which will be producing the movie so they can decide on expenses like artist compensations, advertising, promotions, etc. accordingly. Plus investors can predict an expected return-on-investment. Also, it will be useful for movie theaters to estimate the revenues they would generate from screening a particular movie. 

******************************************************************************************************************************
******************************************************************************************************************************
### II. Data Preparation:

**About the Dataset:**

**The Dataset is divided into 2 csv files tmdb_5000_credits.csv & tmdb_5000_movies.csv. The Major columns are:**
* title(String)
* budget(Numeric)
* genres(String)
* homepage(String)
* id(Numeric)
* keywords(String)
* original_language(String)
* original_title(String)
* overview(String)
* popularity(Numeric)
* production_companies(String)
* production_countries(String)
* release_date(DateTime)
* revenue(Numeric)
* runtime(Numeric)
* spoken_languages(String)
* status(String)
* tagline(String)
* title(String)
* vote_average(Numeric)
* vote_count(Numeric)
* movie_id(Numeric)
* cast(String)
* crew(String)


**Dataset Cleaning & Preparation:**

* So I have first tried creating different dataframes for extracting data from the json object. I use jsonlite library to extract the data. 
* Combining the keywords,genres, production_companies, production countries & spoken languages of a movie in a single column.
* Dropping existing unformatted columns in the main dataset, creating a new dataset "movies"
* Adding new columns gross and gross_flag for the purpose of exploratory analysis 
* Drop useless columns( 'homepage','overview','status','title','tagline','original_title', 'original_language', 'spoken_languages', 'production_countries' )
* Extracting month of release date; put into new column
* From Linear Regression using each of 12 months as dummy categories, we saw that months 5, 6, 11 and 12 are important, while the rest are unimportant. We will aggregate this as 'holiday month' (beginning of Summer; beginning of Winter)
* Select Unique Countries & making dummy variables on top 6 frequent countries on the list.
* Converting genre into dummy columns
* Spliting JSON for cast, crew to select director, actors & actoress
* Downloading List of top 100 directors, actors and converting the directors, actors into dummy varible based on the condition that if director/actor of the film  in the top 100 list then assign 1 else 0
* Assigning Dummy variable for Gender
* Converting binary columns to categorical variables
* Scaleing the dataset for uniformity 
******************************************************************************************************************************
******************************************************************************************************************************
### III. Training Machine Learning Algorithms:

#### Linear Regression:
![scatterplotmatrix](https://user-images.githubusercontent.com/25557540/38492900-35d069d4-3ba5-11e8-90ee-295020f6e292.png)
![correlation plot](https://user-images.githubusercontent.com/25557540/38493373-cff5fa64-3ba6-11e8-8d71-fbd051af52e8.png)


**Result:**
**Diagnostic plots:**
![diagnostic plots](https://user-images.githubusercontent.com/25557540/38492936-52257fe8-3ba5-11e8-902f-3aefbbcd2e51.png)

![residualsvsbudget](https://user-images.githubusercontent.com/25557540/38493012-8f77ac04-3ba5-11e8-9af0-8d88366c5e99.png)

* After Splitting dataset to find test R-squared for linear model we get efficiency of 75%

#### Lasso Regression:

**Result:**
![ridge regression](https://user-images.githubusercontent.com/25557540/38493214-3fddddb6-3ba6-11e8-827d-cead0be5d5be.png)
![cross validationrr](https://user-images.githubusercontent.com/25557540/38493242-52799564-3ba6-11e8-9ca9-8e6e39b5eb9f.png)


#### Ridge Regression:

**Result:**
![lasso regression](https://user-images.githubusercontent.com/25557540/38493218-43a9f13c-3ba6-11e8-8326-0cdbfefccf29.png)
![lasso regressionrr](https://user-images.githubusercontent.com/25557540/38493248-57a91f14-3ba6-11e8-9cf6-38cba3dc2fda.png)

#### Regression Trees:

**Result:**
![rt](https://user-images.githubusercontent.com/25557540/38493273-732e9d72-3ba6-11e8-958a-14761ac09a5e.png)
![rt1](https://user-images.githubusercontent.com/25557540/38493431-094821f2-3ba7-11e8-8013-bdcd6bacf2ca.png)

#### Random Forest:

**Result:**
![rf](https://user-images.githubusercontent.com/25557540/38493423-04dbe270-3ba7-11e8-8226-ea3d74a2c980.png)


******************************************************************************************************************************
******************************************************************************************************************************
### IV. Conclusion:

******************************************************************************************************************************
******************************************************************************************************************************
### V. Future Enhancements:

******************************************************************************************************************************
******************************************************************************************************************************
### VI. References:

******************************************************************************************************************************
******************************************************************************************************************************
