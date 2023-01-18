# Alzheimers-Risk-Factors

## Purpose 
This project explores MRI scan data on demented and non-demented individuals. The goal of the project is to identify a set of risk factors associated with those identified with Alzheimer-onset dementia. Given the relatively unpredictable nature of Alzheimer's (since it is typically not detected until symptoms are displayed), it is of interest to the medical community to identify if a particular set of risk factors can be identified as relatively accurate predictors of Alzheimer-onset dementia. Thus, we seek to explore the classification problem through identifying a set of "predictors" or risk factors associated with those identified with Alzheimer-onset dementia. Our target is Group (Demented, Nondemented, or Converted...which we reclassify as Demented).

## Dependencies
* pyspark
* scipy
* sklearn
* pandas
* numpy
* seaborn

## Dataset Description 
The data utilized was extracted from [Kaggle](https://www.kaggle.com/datasets/jboysen/mri-and-alzheimers?datasetId=1980&language=R)'s repository of datasets. The data used here consists of a collection of 150 subjects aged 60 to 96. Each subject was scanned on two or more visits, separated by at least one year for a total of 373 imaging sessions. For each subject, 3 or 4 individual T1-weighted MRI scans obtained in single scan sessions are included. The subjects are all right-handed and include both men and women. 72 of the subjects were characterized as non-demented throughout the study. 64 of the included subjects were characterized as demented at the time of their initial visits and remained so for subsequent scans, including 51 individuals with mild to moderate Alzheimer’s disease. Another 14 subjects were characterized as non-demented at the time of their initial visit and were subsequently characterized as demented at a later visit.

Even though this data is titled as "longitudinal," we consider the classification of Dementia through MRI ID as the test "unit". In the classification problem, we focus on the 'Group' variable which has levels = Demented (we include Converted with demented) & Nondemented. So, our target is binary.

## Machine Learning Techniques
There will be 5 different models that are utilized and the associated hyperparameters tested for the models:
1. Decision Tree
    * k: 2, 3, 4, 5, 6
    * maxDepth: 2, 3, 4, 5, 6
    * minInstancesPerNode: 10, 15, 20, 25
2. Random Forest
    * k: 1, 2, 3, 4, 5, 6
    * numTrees: 5, 10, 15, 20
3. K-NN Classifier
    * k: 5, 7, 9, 11, 13, 20, 25
4. XGBoost Classifier
    * maxDepth: 2, 5, 10
    * maxBins: 10, 20, 40
    * maxIter: 5, 10, 20
5. Logistic Regression


All models will be done using PySpark and PCA as a step in building a pipeline to select features.

## Results
The models yielded the following results:

![](https://github.com/xaviergenelin/Alzheimers-Risk-Factors/blob/main/results.png)

The Logistic regression resulted in the following coefficients: 
- For a one unit increase in Age, one's log odds of having Dementia decreases by .0017.
- For a one unit increase in log(MMSE), one's log odds of having Dementia decreases by 15.58.
- For a one unit increase in eTIV, one's log odds of having Dementia increases by .02
- For a one unit increase in nWBV (brain volume), one's log odds of having Dementia decreases by 9.9
- For a one unit increase in ASF, one's log odds of having Dementia increases by 25.
- For a one unit increase in EDUC (years of education), one's log odds of having Dementia decreases by .02.

