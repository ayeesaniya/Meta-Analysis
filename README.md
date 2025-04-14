# Project Title - Assessment of heterogeneity and feature selection for predictive modelling in gene expression studies by meta-analysis

Aim: To evaluate the effect of using heterogenous datasets for machine learning in omics datasets

Data type: Microarray gene expression data from publicly available platform

Packages used: Refer the scripts

## Objective 1 : Study of heterogeneity across expression microarray datasets

Challenge - Gene expression data is generated using different platforms (e.g., Affymetrix, Illumina BeadChip). Studies differ in factors such as experimental conditions, population demographics, sample collection methods, and preprocessing techniques. As a result, when multiple datasets are merged to perform any down stream analysis, inconsistencies arise because gene expression measurements may not be directly comparable. Machine learning models trained on heterogeneous data may not generalize well when applied to new datasets.

### Methodology - 
1. Preprocessing of datasets individually - The gene expression data was processed and normalized with respect to the different platforms and annotated with the help HGNC nomenclature. 
2. Create metafile - Merge all the datasets together based on common genes to make a metafile.
3. Batch Correction - Batch correction was performed using ComBat.
4. Differential Gene Expression and Unmerging -  Differential gene expression was performed to determine DEGs and the metafile was unmerged again into respective individual datasets. These datasets were subjected to DGE again.

#### Meta-analysis

5. Meta analysis - Perform meta analysis using the rem_mv function from MetaVolcanoR. Creation of forest and funnel plots of individual genes.
6. Funnel plot value analysis - Create a table which tells whether a dataset in inside/outside the funnel plot for each gene.
   1 - for that gene, the dataset lies inside funnel plot i.e homogenous
   0 - for that gene, that particular dataset is an outlier
   
Outcome - Homogenous and hetrogenous datasets were identified.

## Objective 2 : Study the effect of using homogenous datasets for Machine Learning models

### Methodology - 

1. Metafile creation - Use un-normalized datasets and create a metafile by merging them based on common genes.
2. Data split for test and train -
   - Test data -
       - test1 = one homogenous dataset
       - test2 = one hetrogenous dataset such that the distribution of SCZ/CNT and sample size was same as test1.
   - Train data - The rest of the homogenous datasets were used as train data.
3. Normalization - Individually quantile normalize all datasets in train. Quantile normalize test1 and test2 as well.
4. Batch correction -
  - train data - use parametric adjustment
  - test data -  use train data as reference to batch correct test data 

#### Machine Learning
5. Logistic Regression Classification model - Use train data for training LR model and test it again both the test datasets.
    
Hypothesis - The test data made of homogenous dataset (test1) must show greater accuracy than test data made of heterogenous dataset (test2).


