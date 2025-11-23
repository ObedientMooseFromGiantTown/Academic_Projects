# Comparison of Binary Classification and Feature Selection Methods for Bio-medical Data

## Overview  

This project compares several binary classification and feature selection methods across two biomedical case studies. The first involves classifying immune cells from RNA expression data. The second focuses on feature selection and classification for high-dimensional molecular properties.  

## Project goals  

Case study 1, immune cell classification.  

- Compare a set of baseline classifiers on both full features and principal components.  
- Identify models that give strong F1 scores.  
- Build improved ensemble models such as L2-regularised logistic regression, stacking and weighted voting.  

Case study 2, molecular property prediction.  

- Apply multiple feature selection methods to a high-dimensional, imbalanced dataset.  
- Combine selected features with several classifiers.  
- Find the combination that maximises balanced accuracy.  

## Data  

### Case study 1: cell classification  

- Dataset: subset of data from Suo et al.  
- 5,471 observations and 4,124 gene expression features.  
- Two classes: CD4+T, the negative class, and TREG, the positive class. The dataset is only mildly imbalanced.  
- Features are standardised, then principal component analysis, PCA, is applied to obtain low-dimensional representations.  
- The UMAP plot on page 3 of the accompanying report shows substantial overlap between the two cell types, which makes the classification problem non-trivial.  

### Case study 2: molecule properties  

- Dataset: DOROTHEA from the NIPS 2003 challenge.  
- 800 observations and 100,000 binary features.  
- Strong class imbalance, with 78 positives and 722 negatives.  
- The count plot on page 3 shows that most features are zero very often, which highlights sparsity and the need for careful feature selection.  

## Methods  

### Case study 1: classifiers and ensembles  

Baseline classifiers.  

- LDA.  
- Logistic regression.  
- QDA.  
- k-NN.  
- Gradient boosting decision trees, GBDT.  
- Random forest.  
- Support vector classifiers, SVC.  

Each model is trained on both the full feature set and the first ten principal components, using a split into 80 per cent training and 20 per cent testing.  

Improved models.  

- L2 logistic classifier with a regularisation term to control coefficient size.  
- Stacking that combines random forest and logistic regression as base learners with a logistic regression meta-learner, trained on 50 principal components.  
- Weighted voting classifier with soft voting from SVC, logistic regression and GBDT, with weights reflecting their baseline performance.  

### Case study 2: feature selection and classification  

Feature selection methods.  

- Forward selection with logistic regression, after first narrowing features using random forest importance.  
- Elastic net logistic regression with a cross-validated mixing parameter.  
- Recursive feature elimination, RFE, with random forest and logistic regression base models.  
- Mutual information based selection.  
- SelectFromModel with a random forest classifier.  

After selection, several classifiers, QDA, k-NN, logistic regression, random forest, LDA and SVC, are trained on the reduced feature sets. Balanced accuracy is used to compare them under class imbalance.  

## How to use this repository  

Suggested workflow.  

1. Set up a Python environment with scikit-learn and standard numerical libraries.  
2. For case study 1, load the gene expression data, perform standardisation and PCA and split into train and test sets.  
3. Train baseline classifiers on both the raw features and principal components, then log accuracy, balanced accuracy, AUC and F1 score.  
4. Train the L2 logistic, stacking and weighted voting models on the chosen representation, using cross-validation to tune hyperparameters and PCA dimension where needed.  
5. For case study 2, load the DOROTHEA dataset, then run each feature selection method and train the chosen classifier on the resulting features.  
6. Record balanced accuracy and compare across all method combinations.  

Update any paths, file names and model settings to match your codebase.  

## Results  

### Case study 1  

- Among baseline models, LDA, GBDT and SVC perform best on the gene expression data.  
- All three improved models raise the F1 score relative to individual baselines.  
- The weighted voting classifier that combines SVC, logistic regression and GBDT on 200 principal components achieves the highest F1 score and is selected as the final model.  

### Case study 2  

- Applying different feature selection methods yields several competitive pipelines.  
- The best balanced accuracy comes from a QDA classifier using 50 features selected by forward selection with logistic regression.  

## Reproducibility  

To reproduce the reported findings.  

- Keep the same train–test split proportions and random seeds.  
- Use identical preprocessing steps, especially standardisation and PCA for the cell data.  
- Match the number of selected features in each feature selection method, for example 50 features for forward selection.  

## Acknowledgements and references  

This work was carried out for ST443 at the London School of Economics and Political Science and is based on publicly available data, including the DOROTHEA dataset from the NIPS 2003 feature selection challenge.  
