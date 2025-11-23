# Comparative Analysis of Graph Neural Networks and Kernel Methods for Molecular HIV Inhibition Prediction

## Overview  

This project compares graph neural networks and graph kernel methods for predicting whether a molecule inhibits HIV replication. Molecules are modelled as graphs, with atoms as nodes and bonds as edges, and the task is a binary classification problem on the OGBG-MolHIV benchmark dataset.  

## Project goals  

- Predict HIV inhibition from molecular graphs.  
- Compare several graph neural network (GNN) architectures with graph kernel approaches.  
- Study the effect of pooling and normalisation choices on GNN performance.  
- Assess trade-offs between predictive performance, interpretability and computation.  

## Data  

- Dataset: **OGBG-MolHIV** from the Open Graph Benchmark.  
- Size: 41,127 molecular graphs with standard train, validation and test splits.  
- Each molecule is an undirected graph with atom and bond features. AtomEncoder and BondEncoder turn these categorical features into continuous embeddings for the GNNs.  
- The table on page 2 of the accompanying report summarises node, edge, degree and clustering statistics for each split and highlights the modest graph sizes used in training.  
- There is a marked class imbalance, with about 3.5% positive (toxic or inhibiting) molecules, as shown in the histogram on page 2.  

## Methods  

### Graph neural networks  

The following GNN architectures are implemented.  

- GCN with bond embeddings and a root embedding term.  
- GIN with learnable ε, bond features and batch normalisation in the MLPs.  
- Gated GCN using GRU-based message passing for deeper architectures.  
- Virtual node variants that add a synthetic node connected to all others to improve long-range information flow.  

Pooling options include simple sum or mean pooling, attention-based pooling and more advanced readout layers. Normalisation options include BatchNorm, LayerNorm, InstanceNorm and GraphNorm after each convolutional layer. Dropout after ReLU activations improves generalisation.  

### Kernel methods  

Graph kernel models are built by pairing precomputed kernels with an SVM classifier.  

- Shortest path kernel.  
- Weisfeiler–Lehman (WL) kernel.  
- Neighbourhood hashing.  
- WL-OA and a core-based framework.  

For these methods, edge attributes are ignored and only the atomic number is used as a node label. To keep computation manageable, the training set is subsampled to 5,000 graphs, while validation and test sets remain intact. The SVM decision scores are calibrated with Platt scaling to obtain reliable probabilities and ROC-AUC scores.  

## How to use this repository  

Typical workflow.  

1. Set up a Python environment with PyTorch, PyTorch Geometric or DGL, OGB and standard scientific libraries.  
2. Download the OGBG-MolHIV dataset using the OGB loader.  
3. Run the data preprocessing script or notebook to prepare graph objects and train–validation–test splits.  
4. Train a baseline GNN such as GIN with default pooling and normalisation.  
5. Experiment with different GNN architectures and pooling setups.  
6. Compute graph kernel matrices on the subsampled training set and fit SVM models.  
7. Compare ROC-AUC, training time and memory use across all models.  

Update any script names or commands to match your own code layout.  

## Results  

- Best GNN: GIN with a virtual node, reaching a test ROC-AUC around 0.785.  
- Graph kernels perform slightly below the best GNNs yet remain competitive, with simple shortest path kernels matching or exceeding more complex variants such as WL-OA.  
- The analysis indicates that GNNs and graph kernels have complementary strengths. GNNs scale better and can integrate rich features, while kernels give more transparent similarity measures.  

## Reproducibility  

To reproduce the reported results.  

- Fix random seeds across PyTorch, NumPy and Python.  
- Use the same OGB splits and training hyperparameters as described in the report, such as number of layers, hidden dimension, dropout rate and learning schedule.  
- For kernel methods, keep the same subsampling scheme, including all positives and a random subset of negatives, and use the same SVM settings.  

## Acknowledgements and references  

This project is based on work carried out for the Department of Statistics at the London School of Economics and Political Science and uses the OGBG-MolHIV dataset and related open-source tools.  
