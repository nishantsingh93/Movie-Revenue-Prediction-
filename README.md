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


**Dataset Cleaning:**

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
### III. Exploratory Analysis:
![g](https://user-images.githubusercontent.com/25557540/38494361-8624ad3c-3baa-11e8-823c-b5ee6cbb7209.png)
![prodcomp](https://user-images.githubusercontent.com/25557540/38494259-0c7a76b0-3baa-11e8-9cde-3fbf82cf3408.png)
![tmdbscore](https://user-images.githubusercontent.com/25557540/38494262-0cd23d5a-3baa-11e8-833c-f2a52d09d3ac.png)
![scorevsbudget](https://user-images.githubusercontent.com/25557540/38494260-0c97882c-3baa-11e8-89fc-f0d552d0648e.png)
![scorevsrevenue](https://user-images.githubusercontent.com/25557540/38494261-0cb3a26e-3baa-11e8-83ee-601cc80ce34a.png)
![noofrel](https://user-images.githubusercontent.com/25557540/38494256-0c3ac81c-3baa-11e8-9afe-1317acd7f87f.png)
![popvsbudget](https://user-images.githubusercontent.com/25557540/38494257-0c5dc6e6-3baa-11e8-992a-a7a97e14e9df.png)




******************************************************************************************************************************
******************************************************************************************************************************


### IV. Training Machine Learning Algorithms:
**Scatter Plot:**
![scatterplotmatrix](https://user-images.githubusercontent.com/25557540/38492900-35d069d4-3ba5-11e8-90ee-295020f6e292.png)
* The scatterplot matrices are a great way to roughly determine if you have a linear correlation between multiple variables
* But Scatterplot matrices are not so good for looking at discrete variables
* In our dataset we can see that the variables have non linear correlation

**Correlation plot:**
![correlation plot](https://user-images.githubusercontent.com/25557540/38493373-cff5fa64-3ba6-11e8-8d71-fbd051af52e8.png)

* The correlation plot shows high correlation between <b>revenue</b> & <b>budget</b>, <b>vote_count</b> & <b>popularity</b> and <b>revenue</b> & <b>votecount</b>

#### Linear Regression:

* Intially we run a full model on the full dataset to find correlation between the top predictors and the target variables
* After running the full model we find that our top predictors are <b>budget</b>, <b>runtime </b>, <b>vote_count</b>, <b>genre_Crime</b>, <b> genre_Drama </b>, <b>genre_Animation</b>, <b>genre_Family</b> and <b>holiday_month</b>
* The R square value for the model comes out to be 0.7893
* Now we run the model with our top predictors after splitting the dataset into test, train with 75/25 split ratio and choosing the random sample for each set
* The accuracy for this model is <b>0.7571309</b> 
* We classify the above model as a better model than the previous linear model beacuse of dataset being split into test and train

**Result:**

**Diagnostic plots:**

![diagnostic plots](https://user-images.githubusercontent.com/25557540/38492936-52257fe8-3ba5-11e8-902f-3aefbbcd2e51.png)

* <b>Residuals vs Fitted:</b>  This plot shows that the residuals have non-linear patterns. There is a non-linear relationship between predictor variables and an outcome variable and the pattern shows up in this plot if the model doesn’t capture the non-linear relationship.

* <b>Normal Q-Q:</b>A Q-Q plot compares the quantiles of a dataset and a set of theoretical quantiles from a probability distribution.Therefore it basically compares every observed value against a standard normal distribution with the same number of points. The graph is “skewed right,” meaning that most of the data is distributed on the left side with a long “tail” of data extending out to the right.

* <b>Scale Location:</b> This plot is similar to the residuals versus fitted values plot, but it uses the square root of the standardized residuals. Like the first plot, there should be no discernable pattern to the plot.


* <b>Residuals vs Leverage:</b> The Influence of an observation can be thought of in terms of how much the predicted scores would change  if the observation is excluded. Cook’s Distance is a pretty good measure of influence of an observation. The leverage of an observation is based on how much the observation’s value on the predictor variable differs from the mean of the predictor variable. The more the leverage of an observation , the greater potential that point has in terms of influence. In this plot the dotted red lines are cook’s distance and the areas of interest for us are the ones outside dotted line on top right corner or bottom right corner. If any point falls in that region , we say that the observation has high leverage or potential for influencing our model is higher if we exclude that point. ts not always the case though that all outliers will have high leverage or vice versa. In this case observation #1 & #96 has high leverage and our choices are Justify the inclusion of #1 & #96 and keep the model as is, Include quadratic term as indicated by Residual vs fitted plot and remodel and Exclude observation #1 & #96 and remodel.

#### Ridge Regression:

* Ridge regression uses L2 regularisation to weight/penalise residuals when the parameters of a regression model are being learned. 
* Ridge attempts to minimize residual sum of squares of predictors in a given model. However, ridge regression includes an additional ‘shrinkage’ term – the square of the coefficient estimate – which shrinks the estimate of the coefficients towards zero. The impact of this term is controlled by another term, lambda (determined seperately). 
* Ridge Regression is a commonly used technique to address the problem of multi-collinearity. 
* The glmnet package provides the functionality for ridge regression via glmnet(), it requires a vector input and matrix of predictors.
* Ridge regression involves tuning a hyperparameter, lambda. glmnet() will generate default values for you.
* Ridge regression involves tuning a hyperparameter, lambda, glmnet() runs the model many times for different values of lambda. We can automatically find a value for lambda that is optimal by using cv.glmnet() as follows:
```
ridge_mod = glmnet(x_train, y_train, alpha=0, lambda = lambda)
```


**Result:**
![ridge regression](https://user-images.githubusercontent.com/25557540/38493214-3fddddb6-3ba6-11e8-827d-cead0be5d5be.png)

* Shows the effect of collinearity in the coefficients of an estimator
* Ridge Regression is the estimator used in this example. Each color represents a different feature of the coefficient vector, and this is displayed as a function of the regularization parameter
* The above graph also shows the usefulness of applying Ridge regression to highly ill-conditioned matrices. For such matrices, a slight change in the target variable can cause huge variances in the calculated coefficients. Therefore, it is useful to set a certain regularization (lambda) to reduce this variation (noise).
* When lambda is very large, the regularization effect dominates the squared loss function and the coefficients tend to zero 
* At the end of the path, as lambda tends toward zero and the solution tends towards the ordinary least squares, coefficients exhibit big oscillations. In practise it is necessary to tune lambda in such a way that a balance is maintained between both.


![cross validationrr](https://user-images.githubusercontent.com/25557540/38493242-52799564-3ba6-11e8-9ca9-8e6e39b5eb9f.png)
* cv.glmnet() uses cross-validation to work out how well each model generalises, which we can visualise as:
* The lowest point in the curve indicates the optimal lambda: the log value of lambda that best minimised the error in cross-validation. We can extract this values as
```
opt_lambda <- cv.ridge.out$lambda.min
opt_lambda
```
* The best lambda value is <b>0.01</b>

#### Lasso Regression:


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


![picture1](https://user-images.githubusercontent.com/25557540/38494085-72bb9a04-3ba9-11e8-80e9-95d7db152a81.png)


******************************************************************************************************************************
******************************************************************************************************************************
### V. Conclusion:

<img width="976" alt="screen shot 2018-04-09 at 3 37 26 am" src="https://user-images.githubusercontent.com/25557540/38493528-64b51838-3ba7-11e8-8669-c27fad26faff.png">

******************************************************************************************************************************
******************************************************************************************************************************
### VI. Future Enhancements:

******************************************************************************************************************************
******************************************************************************************************************************
### VII. References:

* https://www.themoviedb.org/
* https://drsimonj.svbtle.com/ridge-regression-with-glmnet
* https://www.r-bloggers.com/ridge-regression-and-the-lasso/
* https://www.r-bloggers.com/random-forests-in-r/


******************************************************************************************************************************
******************************************************************************************************************************
