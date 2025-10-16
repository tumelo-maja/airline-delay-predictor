# Flight Delay Predictor

## Dataset Content

The TranStats Airline On-Time Performance dataset records information about flights in the U.S., including delay causes and timing. Each record represents a monthly summary of flights for a given airport and airline. Count of flights delayed and delay duration are included in each record.

## Project Goals

* Discover hidden flight delay patterns and trends by airline-airport-month (AAM)
* Predict if a given AAM combination will likely have above-average delays.
* Estimate the expected delay duration for the given AAM combination.
* Present results through an interactive dashboard.

## Business Requirements

### Business Requirement 1: Discover Delay Patterns

**Objectives:**

* Describe any seasonal or regional delay trends/patterns.
* Identify airlines, airports or months most affected by flight delays.
* Quantify, in proportions, the contributions of various delay factors/causes to the overall flight delays.

**Benefit to user(s):**

* Airports/Airlines can anticipate/plan for expected delays and allocate resources/personnel as applicable to the delay type.
* Long term use, systemic issues requiring interventions can be identified if the flight delays are non-environmental.

### Business Requirement 2: Predict Monthly Delay Risk

**Objectives:**

* Predict the likelihood that an airline-airport pair will experience flight delays for a given month. Likelihood to be presented as a probability.

**Benefit to user(s):**

* Enables capacity forecasting and planning by airline/airport operators.
* Allows for performance evaluation between airlines and airport for different months.

ML Task: Classification

### Business Requirement 3: Predict Delay Duration

**Objectives:**

* Predict the average delay duration for AAM combination if likely to occur.

**Benefit to user(s):**

* Airlines/airports operators can estimated the service disruption levels.
* Helps set passengers expectations and to effectively/accurately communicate expected delays.

ML Task: Regression/Classification

## Hypothesis and how to validate?

The hypotheses listed below are aligned to individual business requirements (BR's).

* **Hypothesis 1:** Flight delays have a pattern across seasons, airlines and airports, with higher delays during peak travel seasons/ winter months at major airports.
  * Descriptive statistics / clustering - EDA and plots can be useful describing relationships between variables.
  * Validation: timeseries plots, correlations r2 >= 0.8, silhoutte scores.

* **Hypothesis 2:** Delays causes/factors differ across airports/airlines and seasons.
  * Clustering analysis 

* **Hypothesis 3:** Flight delay risk and duration can be predicted from historical flight data.
  * Delay risk: Regression/Classification
  * Delay duration: Multiclass Classification - F1 => 0.7, confusion matrix
  * Validation using Recall/precision, f1 etc.

## The rationale to map the business requirements to the Data Visualizations and ML tasks

* **Business Requirement 1:** Discover Delay Patterns/Trends
  * **Analysis:** Timeseries trends by airport/month, correlation plots, heatmaps of delay causes.
  * **ML Task:** clustering (unsupervised) to group airports/airlines with similar delay patterns
  * **Output:** Delay trends and cluster insights for airports/airlines.

* **Business Requirement 2:** Predict Delay Risk
  * **Analysis:** Feature exploration and importance plots
  * **ML Task:** Binary classification (check if average delay exceeded - 2 classes, 0 - No, 1 - Yes)
  * **Output:** Probability of high-delay risk per AAM combination.

* **Business Requirement 3:** Predict Delay Duration
  * **Analysis:** Delay distribution plots and confusion matrix
  * **ML Task:** Multiclass classification (discretized delay durations classes)
  * **Output:** Predicted delay duration class for a given AAM combination.

## ML Business Case

---

### Model 1: Delay Pattern Analysis - Clustering

**Goal:** To group records with similar delays by airline and airport to identify patterns/trends. There is no target variable for unsupervised learning ML task.

* **Data inputs:** Training data to fit the model will be a subset of the TranStats Airline On-Time Performance dataset.
  * Train data - features: all variables.
* **Output:** Airport/airline cluster label, defined as an additional column appended to the dataset. This column represents the cluster's suggestions of groups. It is a categorical and nominal variable represented by numbers starting at 0.
* **Validation:** average silhouette score >= 0.45. The ML model would be considered a failure if the model suggests more than 15 clusters which would be difficult interpret.
* **Heuristics:** Currently, there is no approach to grouping airports/airlines by delay characteristics.

### Model 2: Predict Delay Risk - Binary Classification

**Goal:** To predict whether a given AAM combination will experience a higher delay, more than the average delay for that AAM combination.

* **Data inputs:** Training data to fit the model will be a subset of the TranStats Airline On-Time Performance dataset.
  * Train data - features: all variables, target: delay.
* **Output:** Delay risk label (Yes/No) with a probability score. The target variable is a categorical. Binary classification will used for analysis. Model types to be consider include Logistic Regression, Random Forest etc.
* **Validation:** Recall >= 0.8, Precision >= 0.75.
* **Heuristics:** Currently, there is no approach to predict if a delay is likely for a given AAM combination.

### Model 3: Predict Delay Duration - Multiclass Classification

**Goal:** To predict the expected delay duration for a given AAM combination.

* **Data inputs:** Training data to fit the model will be a subset of the TranStats Airline On-Time Performance dataset.
  * Train data - features: all variables, target: discretized classes of delay duration.
* **Output:** Delay risk label (Yes/No) with a probability score. The target variable is a categorical. Binary classification will used for analysis. Model types to be consider include Logistic Regression, Random Forest etc.
* **Validation:** F1 >= 0.75.
* **Heuristics:** Currently, there is no approach to predict flight delay levels for a given AAM combination.

## Dashboard Design

### Page 1: Quick Project Summary

* Project summary
* Dataset description
* Business requirements

### Page 2: Flight Delay Patterns/Trends

* Plots and elements for Business Requirement 2.

### Page 3: Predict Delay Risk

* Plots and elements for Business Requirement 3.

### Page 4: Predict Delay Risk

* Plots and elements for Business Requirement 4.

### Page 5: Predict Delay Risk

* Plots and elements for Business Requirement 5.

## Unfixed Bugs

* ipython error - https://github.com/explosion/spacy/issues/13871. solution: `pip install ipython==7.23.1`
* You will need to mention unfixed bugs and why they were not fixed. This section should include shortcomings of the frameworks or technologies used. Although time can be a significant variable to consider, paucity of time and difficulty understanding implementation is not a valid reason to leave bugs unfixed.

## Deployment
### Heroku

* The App live link is: https://YOUR_APP_NAME.herokuapp.com/ 
* Set the runtime.txt Python version to a [Heroku-24](https://devcenter.heroku.com/articles/python-support#supported-runtimes) stack currently supported version.
* The project was deployed to Heroku using the following steps.

1. Log in to Heroku and create an App
2. At the Deploy tab, select GitHub as the deployment method.
3. Select your repository name and click Search. Once it is found, click Connect.
4. Select the branch you want to deploy, then click Deploy Branch.
5. The deployment process should happen smoothly if all deployment files are fully functional. Click now the button Open App on the top of the page to access your App.
6. If the slug size is too large then add large files not required for the app to the .slugignore file.


## Main Data Analysis and Machine Learning Libraries
* Here you should list the libraries you used in the project and provide an example(s) of how you used these libraries.


## Credits 

* In this section, you need to reference where you got your content, media and extra help from. It is common practice to use code from other repositories and tutorials, however, it is important to be very specific about these sources to avoid plagiarism. 
* You can break the credits section up into Content and Media, depending on what you have included in your project. 

### Content 

- The text for the Home page was taken from Wikipedia Article A
- Instructions on how to implement form validation on the Sign-Up page were taken from [Specific YouTube Tutorial](https://www.youtube.com/)
- The icons in the footer were taken from [Font Awesome](https://fontawesome.com/)

### Media

- The photos used on the home and sign-up page are from This Open-Source site
- The images used for the gallery page were taken from this other open-source site



## Acknowledgements (optional)
* Thank the people who provided support through this project.

