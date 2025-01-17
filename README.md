# A Machine Learning App for Studying the U.S. Supreme Court Database
[![Static Badge](https://img.shields.io/badge/pypi-v1.3.0-blue)](https://pypi.org/project/SCDB-ML-app/1.3.0/)  
[![Static Badge](https://img.shields.io/badge/license-APGL3.0-green)](https://github.com/havurquijo/Project-SCDB/blob/v1.0.1-alpha/LICENSE.txt)  
[![Static Badge](https://img.shields.io/badge/data_analyzed%3A-SCDB-AD1313)](http://scdb.wustl.edu/about.php)  
[![Static Badge](https://img.shields.io/badge/running_on%3A-AWS(ec2)-red)](https://scdb-ml.alcantara-urquijo.com.br/)  

## Technologies and programming languages utilized
1. Python -> Mining and processing data, also creating the predictive model and web page app.
2. Flask -> Based in python for creating the web page.
3. HTML -> Structuring the web page.
4. CSS -> To style the web page.
5. JavaScript -> Triguering actions like notifications.
6. Versioning -> PyPi and Github
7. Deployment -> Server in AWS EC2 technology

# Table of Contents

1. [Introduction](#introduction)
2. [Features](#features)
3. [Installation](#installation)
4. [Usage](#usage)
    1. [Running the App](#running-the-app)
    2. [Endpoints](#endpoints)
5. [Data](#data)
    1. [Dataset Description](#dataset-description)
    2. [Preprocessing](#preprocessing)
6. [Machine Learning Model](#machine-learning-model)
    1. [Model Selection](#model-selection)
    2. [Training the Model](#training-the-model)
    3. [Model Evaluation](#model-evaluation)
7. [Prediction](#prediction)
    1. [DecisionDirection Variable](#decisiondirection-variable)
    2. [Prediction Accuracy](#prediction-accuracy)
8. [Deployment](#deployment)
9. [Contributing](#contributing)
10. [License](#license)
11. [Contact](#contact)

# Introduction

This application leverages machine learning techniques to analyze the U.S. Supreme Court Database. Built with Python and Flask, this app utilizes the scikit-learn library, specifically the Decision Tree Classifier, to predict the variable `decisionDirection` with up to 96% accuracy. The primary goal of this project is to provide insights into the Supreme Court's decisions and to offer a predictive model for legal researchers, students, and enthusiasts.

By integrating Flask for the web framework and scikit-learn for machine learning, the application offers a user-friendly interface and robust analytical capabilities. Users can interact with the app to train the model and generate predictions based on the data provided by the Supreme Court site. This README.md provides detailed instructions on installation, usage, and the underlying methodologies used in this project.

This project is also deployd into a AWS server running online. See the link in the section befor the table of content (#a-machine-learning-app-for-studying-the-u.s.-supreme-court-database)


# Features

- **Historical Data Analysis**: Explore and analyze historical Supreme Court decisions using various filters and parameters (incoming in future releases).
- **Predictive Modeling**: Utilize the Decision Tree Classifier to predict the outcome of Supreme Court decisions (`decisionDirection` variable) with up to 96% accuracy. (In future releases, other machine learning models may be used).
- **Interactive Dashboard**: A user-friendly interface that allows users to interact with the data, view trends, and generate visualizations.
- **Data Visualization**: Generate charts and graphs to visualize decision trends, justice voting patterns, and other relevant statistics (incoming in future releases).
- **Custom Predictions**: Train the model with different parameters to generate custom predictions on Supreme Court decisions.
- **Model Insights**: Understand the model's decision-making process with feature importance and decision tree visualization.
- **Responsive Design**: Ensure the app is accessible on various devices, including desktops, tablets, and smartphones.
- **Documentation and Tutorials**: Provide comprehensive documentation and tutorials to help users understand and use the application effectively.


# Installation
You can install this application in your machine and access the webpage in your localhost by installing it throught PyPi installer,

```shell
pip install SCDB-ML-app
```
For installing an specific version use:
```shell
pip install SCDB-ML-app==version(like 1.0.0)
```
For updating to the lattest version use teh following code:
```shell
pip install --update SCDB-ML-app
```

# Usage
## Running the App
If installed you should import it and then run it into a python enviroment as:
```python
from scdb_ml_app import SCDB_ML_app as flskapp

if __name__ == "__main__":
    flaskapp.app.run('0.0.0.0')
```
This will run the aplication in all the available address at the port 5000.

If you download the aplication via [Github](https://github.com/havurquijo/Project-SCDB) then, after unzip it go to the main directory and run the app as:
In the powershell of Windows,
```shell
py -m scdb_ml_app.SCDB_ML_app 
```
That way it's granted to run the app as a module of python and the internal relative imports will work.


# Data
## Dataset Description
The Supreme Court Database is the definitive source for researchers, students, journalists, and citizens interested in the U.S. Supreme Court. The Database contains over two hundred pieces of information about each case decided by the Court between the 1791 and 2022 terms. Examples include the identity of the court whose decision the Supreme Court reviewed, the parties to the suit, the legal provisions considered in the case, and the votes of the Justices.[Database webpage](http://scdb.wustl.edu/index.php)

The data we are using in this application is the Modern release and includes terms from 1946 up to 2022. It contains 82,538 records of the votes of the 9 judges for each case, covering more than 9,000 cases. Each column has an attributed variable which has a numerical value for all registers, those variables are:

1. caseId 
2. docketId
3. caseIssuesId
4. voteId
5. dateDecision
6. decisionType
7. usCite
8. sctCite
9. ledCite
10. lexisCite
11. term
12. naturalCourt
13. chief
14. docket
15. caseName
16. dateArgument
17. dateRearg
18. petitioner
19. petitionerState
20. respondent
21. respondentState
22. jurisdiction
23. adminAction
24. adminActionState
25. threeJudgeFdc
26. caseOrigin
27. caseOriginState
28. caseSource
29. caseSourceState
30. lcDisagreement
31. certReason
32. lcDisposition
33. lcDispositionDirection
34. declarationUncon
35. caseDisposition
36. caseDispositionUnusual
37. partyWinning
38. precedentAlteration
39. voteUnclear
40. issue
41. issueArea
42. decisionDirection
43. decisionDirectionDissent
44. authorityDecision1
45. authorityDecision2
46. lawType
47. lawSupp
48. lawMinor
49. majOpinWriter
50. majOpinAssigner
51. splitVote
52. majVotes
53. minVotes
54. justice
55. justiceName
56. vote
57. opinion
58. direction
59. majority
60. firstAgreement
61. secondAgreement

## Preprocessing
If the data provided by the site is not downloaded to the server when trying to train the model, the application will redirect to a page to execute the download. After that, the application will take the variables used in the Decision Tree Classifier machine learning algorithm and produce a file with the extension *.csv containing the chosen variables. Additionally, a process to eliminate NaN values will occur.

The variable we want to analyze is the `decisionDirection`, which indicates the direction of each judge's decision for each case. It can take up to three values that indicate the political direction of each decision:

1. If it's liberal
2. If it's conservative
3. If it isn't specified

For simplicity, we deleted the unspecified values of this variable during preprocessing. A few registers survive the preprocessing process, but enought to make a prediction model.


# Machine Learning Model
## Model Selection


## Training the Model


## Model Evaluation


# Prediction
## DecisionDirection Variable


## Prediction Accuracy


# Deployment


# Contributing


# License
SCDB-ML-app is a deployed app to analyze the U.S. Supreme Court Database
Copyright (C) 2024  HERMES A. V. URQUIJO

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as
published by the Free Software Foundation, either version 3 of the
License, or (at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

# Contact


