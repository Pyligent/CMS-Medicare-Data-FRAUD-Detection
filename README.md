# CMS Medicare Data FRAUD Detection

## 1 Project Overview

This project is dedicated to building big data solutions with tangible applications at the intersection of healthcare and insurance industry. This Capstone project will build a Medicare Fraud Detection model to analyze open data and predict/detect the fraudulent Medicare providers based on fraud patterns, anomaly analysis and geo-demographic metrics, with FDA drug data’s help this model is also trying to figure out the Opiate prescriptions and Overdoses related fraudulence. All datasets will be based solely on publicly available Medicare data from the Centers for Medicare and Medicaid Services (CMS), FDA/openFDA and other open data resources.

### 1.1	Introduction and Background
Healthcare is a major industry in the U.S. with both private and government run programs. The costs of healthcare continue to rise, in part due to the increasing population of the elderly. U.S. healthcare spending from 2012 to 2014 has increased by 6.7% to reach $3 trillion and Medicare spending accounts for 20% of all health-care spending in the U.S. at about $600 billion. This rising elderly population, combined with the increased costs of Medicare, need cost-cutting solutions, where the reduction in fraud is one way to help recover costs and reduce overall payments. 
The impact of healthcare fraud is estimated to be between 3% to 10% of the nation’s total healthcare spending and continuing to adversely impact the Medicare program and its beneficiaries (NHCAA 2017). Government has initialized the programs, such as the Medicare Fraud Strike Force (OIG 2017), enacted to help combat fraud, but continued efforts are needed to better mitigate the effects of fraud. These are our project’s basic introduction and background; also it shows that there are huge business opportunities for Medicare Fraud Detection systems.

### 1.2 Problem Statement
Build a free and innovative data science tool that predicts fraud in the medical insurance industry using anomaly analysis and geo-demographic metrics. Said tool can be offered to insurance providers, health care providers, patients, pharmacy, and doctors and will enable company gain credibility in the industry, combat the increasing costs of healthcare, and costly impact of fraud. 

## 2. Problem Statement
Build a free and innovative data science tool that predicts fraud in the medical insurance industry using anomaly analysis and geo-demographic metrics. Said tool can be offered to insurance providers, health care providers, patients, pharmacy, and doctors and will enable Pulseinsights gain credibility in the industry, combat the increasing costs of healthcare, and costly impact of fraud. 

### 2.1 Define the problem

Healthcare fraud is a main problem that causes substantial monetary loss in Medicare/Medicaid and insurance industry. The Centers for Medicare and Medicaid Services (CMS) have setup Medicare Part D programs since 2006. CMS relies on it to detect and prevent fraud, waste and abuse in Part D program. But using the traditional methods, the fraud detection is conducted on random samples by human experts. The consequences are the samples might be misleading or manual detection is costly. According to Office of Inspector General report: Since 2006, the Medicare Fraud has rapidly increased. The fraud patterns include the following four types:

•	Fraud by Service Providers (Doctors, hospitals, pharmacies)
•	Fraud by Insurance subscribers (patient or patient’s employers)
•	Fraud by insurance carriers
•	Conspiracy Frauds (involved with all parties)

Also along with fraud the following patterns reported by OIG report:

•	Commonly abuse drug/opioid has grown faster than spending for all Part D drugs
•	Pharmacies with questionable billing raise concerns about pharmacy-related fraud schemes 
•	Geographic hotspots for certain non-controllable drugs points to possible fraud and abuse

This project will try to use the machine learning method to address the above problems and detect the fraudulence Medicare claims from the CMS open datasets and other use open data. 

### 2.2 Project Objectives

The objectives of this project will be

•	Build a simple Data Model to show the relationships among the different datasets and identify the key feature-sets for fraud detections
•	Build a comprehensive machine learning model to detect fraud pattern based on the different features: Service Providers (Doctors, Pharmacies), Insurance subscribers (patients), Geo-demographic and commonly abuse drugs prescriptions 
•	Setup a benchmark metrics to measure and evaluate the experimental result
•	Market-ready product 

## 3.	Datasets

We will use the following open datasets:
•	Part D Prescriber dataset 
•	Excluded (LEIE) dataset
•	Payment Received dataset
•	FDA Drug ingredients dataset
•	Others: Part D Opioid Prescriber Summary

### 3.1	Medicare Provider Utilization and Payment Data (Part D Prescriber) 
This dataset contains 21 columns and includes the following key information
•	All prescriptions aggregated at the physician and drug level
•	All information on utilization, payments, and submitted charges by National Provider Identifier (NPI), Healthcare Common Procedure Code, and Place of Service 
•	All information on the physician (NPI, Name, City, Practice, etc.) 

The overall features will be used to investigate the general fraud detections
•	The number of different drugs prescribed
•	The sum of the number of prescriptions, 
•	The sum of the number of days prescribed, 
•	The sum of the total cost
•	The variance of these three sums quantities
•	The maximum of these three sums quantities

The Prescribing pattern features to figure out the prescribe-related fraud
•	The number of different drugs prescribed
•	The sum of the number of prescriptions
•	The sum of the number of days prescribed
•	The sum of the total cost
•	The variance of these three sums quantities
•	The maximum of these three sums quantities

The drug pattern features to classify the commonly abuse drug-related fraud
•	Average Number of Prescriptions per Beneficiary
•	Number of Pharmacies associated with each prescriber
•	Average number of types of drugs per beneficiary
•	Percentage of Schedule II/III drugs (contain the potential abuse drug ingredients)
•	Percentage of Brand-Name drugs (expensive drugs)
•	Percentage of beneficiaries with an excessive supply of a drug 

Other features, such as the provider location or specialty will be combined with the above features to detect the fraud.

### 3.2	List of Excluded Individuals and Entities (LEIE) database
This database contains a list of individuals and entities that are excluded from participating in federally funded healthcare programs (i.e. Medicare) due to previous healthcare fraud. We could treat the LEIE dataset as the semi-labeled data, because LEIE is the fraudster-based target but not a fraud one. We will explore the LEIE data through the NPI feature to join with Part D or Payment dataset, the other way is that we should map the Part D dataset with LEIE exclusion rules. 
In the LEIE dataset, the Column EXCLTYPE is exclusion rules. If EXCLTYPE value equals 1128(a)*, then exclusion years are five, 1128(c)(g)(i) is ten years and 1128(c)(g)(ii) is permanent exclusion. We may check if any claims from exclusion NPI appeared in Part D, then we can label it as fraud. That is the one way to transfer LEIE data into the labeled data.

Feature sets link Part D and LEIE
•	NPI, Unique provider identification number
•	Medical provider’s specialty (or practice)
•	Number of procedures/services the provider performed
•	Number of distinct Medicare beneficiaries receiving the service
•	Number of distinct Medicare beneficiary / per day services performed
•	Average of the charges that the provider submitted for the service
•	Average payment made to a provider per claim for the service performed
•	EXCLUSION-label: Mapped fraud labels from the LEIE database

### 3.3	Payments Received by Physician from Pharmaceuticals
Physicians in the US are required to declare all payments received from pharmaceutical companies. In addition to “payments received” basic information (ex: amount, date, type) this datasets contains many other useful data elements such as physician ownership in company, consulting fees, charity indicator, dispute status etc. The whole datasets are includes three parts: General Payment, Research Payment and Physician Ownership Details. 

Key Features
•	The sum of general payment
•	Name of drug associated the payments

### 3.4	FDA Drug Ingredients Data and Opioid Drug list from CMS
This dataset contains 
•	FDA-approved brand name and generic prescription and over-the-counter human drugs and biological therapeutic products.
•	The majority of patient information, labels, approval letters, reviews, and other information are available for drug products approved since 1998

We also will try to use the Opioid drug list from CMS to identify the possible drug-related fraud. The data is available through https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/Downloads/OpioidDrugList.zip

## 4.	Methodology and Analytics technique

### 4.1	Methodology
The methodology of this project will follow the below procedures:
•	Data exploration, cleansing and preparation
•	Build a simple data model to join all datasets
•	Feature engineering to choose the effective feature sets for the different fraud patterns
•	Build a machine learning model to detect the different fraud patterns

### 4.2	Analytics Technique
•	Descriptive Analytics for Fraud Detection
Descriptive analytics or unsupervised learning aims at finding unusual anomalous behavior deviating from the average behavior or norm. When used for fraud detection, unsupervised learning is often referred to as anomaly detection, since it aims at finding anomalous and thus suspicious observations. Unsupervised learning can be useful for fraud detection and thus have no labeled historical data set available (such as LEIE). It can also be used in existing fraud models by uncovering new fraud mechanisms. We will try to use the nearest-neighbour based techniques, Clustering-based methods and other algorithms.


•	Predictive Analytics for Fraud Detection
In predictive analytics, the aim is to build an analytical model predicting a target measure of interest. The target is then typically used to steer the learning process during an optimization procedure. Two types of predictive analytics can be distinguished depending on the measurement level of the target: regression and classification. 
We will use the logistic Regression and Random Forest Classification to build the machine-learning model. If possible, we will use the ensemble and boosting model to optimize the model.

### 4.3	Challenges in handling huge Data Sets
Normally, the size of CMS Medicare Part D data is more than 3Gbytes. Given the facts in huge capacity of Medicare data, we need more efficient ways to handling the data. There are lots of challenges with pre-processing, querying and analyzing data. We have tried three possible ways to address these challenges:
•	Google Cloud Big-Query API
Part D data is integrated with Google Cloud platform and Google provides cloud-based query API. We could use Python to do SQL query to Pandas Data-frame. But the limitation is the size of query is limited below one Gbytes.
•	PostgreSQL or MySQL 
Use Python packages, we can SQL query the data from some local SQL servers. But the problem is it can’t process the huge data efficiently. Also need a lots work on SQL servers.
•	Apache Spark and PySpark
So far, Spark is the fastest way to handling the huge data due to the in-memory computation and distributing computing framework. We will try to use PySpark as the mainly data technique to handling data. 


### 5.	Evaluation and Performance Metrics

We will use the Area Under receiver operating characteristic Curve (AUC) performance metric. AUC is used to assess the capabilities of binary classification methods. The ROC curve is used to characterize the trade-off between true positive rate and false positive rate, depicting a learner’s performance across all decision thresholds. Perfect classification is indicated by an AUC value of 1, with a range from 0 to 1. Due to the severe class imbalance of the testing data, AUC is used as the performance measure for our experiment.

## Jupyter Notebook

All notebooks are available in this Github. 

### 6 8.	Reference

CMS Part D datasets:
https://www.cms.gov/Research-Statistics-Data-and-Systems/Statistics-Trends-and-Reports/Medicare-Provider-Charge-Data/Part-D-Prescriber.html
LEIE Datasets:
https://oig.hhs.gov/exclusions/exclusions_list.asp
Office of Inspector General Reports
https://oig.hhs.gov/reports-and-publications/portfolio/index.asp
FDA datasets
https://www.fda.gov/Drugs/InformationOnDrugs/ucm079750.htm#collapseOne
Google Cloud Query – Part D Data
https://bigquery.cloud.google.com/table/bigquery-public-data:medicare.part_d_prescriber_2014?tab=preview
