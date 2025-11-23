# Academic_Projects

A collection of projects completed during my time at the London School of Economics (LSE). The work here spans coursework, research projects and independent studies, with a focus on data science, statistics and applied machine learning.

## About this repository  

Each project sits in its own folder and includes a dedicated README that explains the motivation, data, methods and results in more detail. This top level file gives a quick overview so you can see how everything fits together.

## Project overview  

### Comparative Analysis of Graph Neural Networks and Kernel Methods for Molecular HIV Inhibition Prediction  

A machine learning project that compares graph neural networks with graph kernel methods on the OGBG-MolHIV dataset. Molecules are represented as graphs and the task is to predict whether each one inhibits HIV replication. The work examines different GNN architectures, pooling strategies and normalisation schemes, and evaluates how they perform against kernel based SVMs in terms of accuracy, efficiency and interpretability.

### Complete the Look: Scene-based Complementary Product Recommendation  

A computer vision project that rebuilds a scene based fashion recommender system. Given a scene image, the model suggests products that complement the outfit or context. It uses a ResNet backbone, global and local visual embeddings, and a triplet loss to learn compatibility between scenes and products. Results are reported using accuracy and mean reciprocal rank, along with visual diagnostics.

### Comparison of Driving Test Results for a Given Profile between Two Centres  

An applied statistics project that compares driving test outcomes at the Burgess Hill and Wood Green test centres for a specific candidate profile, a 21 year old woman. The analysis uses official driving test statistics, graphical exploration, normality checks, t tests and logistic regression to estimate pass rates and recommend the test centre that offers the higher chance of success.

### Comparison of Binary Classification and Feature Selection Methods for Bio-medical Data  

A two part study on high dimensional biomedical data. The first case focuses on classifying immune cells from RNA expression data and compares several classifiers and ensembles. The second case studies molecular property prediction with a very high dimensional and imbalanced dataset and evaluates different feature selection strategies. Performance is compared using measures such as F1 score and balanced accuracy.

### Estimating Missing Trade Data  

An applied econometrics and data science project linked to work with the World Trade Organization. It looks at gaps in international trade statistics and tests methods for estimating missing bilateral trade flows. The project combines economic structure, such as gravity models and mirror statistics, with modern machine learning approaches, including tree based models and graph neural networks, to improve the completeness and quality of trade data.

## Working with this repository  

To explore a project, open its folder and start with the local `README.md`. That file will usually cover:

- The aim of the project  
- Details of the dataset and any preprocessing  
- The main models or methods used  
- How to run the code and reproduce key results  
