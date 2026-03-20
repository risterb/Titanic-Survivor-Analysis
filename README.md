<h1 align="center">Surviving the Titanic: Passenger Data Analysis</h1>

## Summary
This project explores passenger data from the Titanic to identify key factors that influenced passenger survival chances. The analysis highlights that surviving was not random, but rather tied to socioeconomical factors, gender, age and family structure. 

## Skills Demonstrated
- Exploratory Data Analysis (EDA)
- Data Visualization: Built visual insights using Seaborn and Matplotlib
- Statistical Thinking
- Python & Libraries
  - pandas
  - numpy
  - seaborn
  - matplotlib

## Dataset

<p align="center">
</p>

The dataset contains information on 891 passengers, including:
- Demographics (age, sex)
- Ticket class (proxy for socioeconomic status)
- Fare and cabin information
- Family structure onboard
- Survival outcome

## Key Findings
##  1.Survival was strongly influenced by gender
Female passengers had a significantly higher survival rate than males. This aligns with evacuation behavior prioritizing women.

![png](Visuals/Titanic_Data_Project_33_1.png)

## 2. Class was a major determinant of survival
Passengers in first class were far more likely to survive than those in third class. This suggests unequal access to safety during the evacuation.

![png](Visuals/Titanic_Data_Project_32_1.png)

## 3. Children were more likely to survive than adult males
When grouping passengers into male, female, and child, children showed higher survival rates, indicating age-based prioritization.

## 4. Survival varied by a combination of factors
The interaction between class, age, and gender is critical. For example, younger passengers in higher classes had the highest survival rates, while older passengers in lower classes had the lowest.

![png](Visuals/Titanic_Data_Project_35_1.png)

## 5.Survival declines with age, but class significantly moderates this effect
Survival probability decreases as age increases, but this decline is much steeper for lower-class passengers. First-class passengers maintain relatively higher survival rates across all age groups, while third-class passenger experience the lowest survival likelihood.

![png](Visuals/Titanic_Data_Project_36_1.png)

## Data Approach
Below are selected code snippets that highlight key steps in data preparation, feature engineering, and analysis.

### Creating meaningful passenger categories
def male_female_child(passenger):
    age, sex = passenger
    if age < 16:
        return 'child'
    else:
        return sex

titanic_df['person'] = titanic_df[['Age','Sex']].apply(male_female_child, axis=1)

### Identifying passengers traveling alone vs with family
def solitary(family):
    SibSp, Parch = family
    if SibSp + Parch == 0:
        return 'alone'
    else:
        return 'with family'

titanic_df['onboarded party'] = titanic_df[['SibSp','Parch']].apply(solitary, axis=1)

### Analyzing survival across multiple variables
sns.lmplot(x='Age', y='Survived', hue='Pclass', data=titanic_df, x_bins=[10,20,40,60,80])

### Comparing survival rates across classes
sns.catplot(x='Pclass', y='Survived', data=titanic_df, kind='point')
