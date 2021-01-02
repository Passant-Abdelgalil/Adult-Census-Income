# Description:
This notebook uses Adult Census Dataset from Kaggle and predict an individual income based on some features

## Data Description:
This data was extracted from the 1994 Census bureau database by Ronny Kohavi and Barry Becker (Data Mining and Visualization, Silicon Graphics). A set of reasonably clean records was extracted using the following conditions: ((AAGE>16) && (AGI>100) && (AFNLWGT>1) && (HRSWK>0)). The prediction task is to determine whether a person makes over $50K a year.
<a href = "https://www.kaggle.com/uciml/adult-census-income">Data</a>
### Features:
* Age
* workclass
* fnlwgt
* education
* education.num
* marital.status
* occupation 
* relationship
* race
* sex
* capital.gain
* capital.loss
* hours.per.week
* native.country
* **Target Values**: income

## Machine Learning Pipeline:
1. **Problem Definition**:
   predicting individual income based on provided features
2. **Data Exploration**:
   * Age distribution was right skewed so we had to handle this
   * fnlwgt distribution was right skewed so also we had to handle this
   * native.country has some rare values that can be combined together
   * relation has some values that can be combined together
   * capital.gain affects individual income although there are many zeros
   * unlike capital.gain, capital.loss doesn't affect the income greatly and has many zeros
   * hours per week affects income.
   * Education & education.num are Two equivilant columns, so we choose eductaion.num to keep.
3. **Data Preparation**
   * Drop missing values in form of '?' values.
   * Apply *log* to Age values to make it nearly normally distributed.
   * Apply *Log* to fnlwgt values to make it nearly normally distributed.
   * Drop Education column
   * Drop capital.loss column
   * change native.country values to be {United-states, Not-Unitied-states}.
   * change ['Married-Spouse-absent', 'Widowed', 'Divorced'] in relation column to be 'Separated'.
   * Encoding Categorical columns in the dataset using pandas function *get_dummies*.
   * split data to Train set and Test set with ratios 70%, 30% respectively.
4. **Model Training**
   * model : GradientBoostingClassifier with default values but with max_depth = 5.
5. **Model Evaluation**
   * Accuracy: 86.09%
