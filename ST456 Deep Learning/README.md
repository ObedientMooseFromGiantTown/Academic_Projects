# Complete the Look: Scene-based Complementary Product Recommendation

## Overview  

This project replicates and adapts a contextual fashion recommender system that suggests products to complement a given scene image. It builds on the “Complete the Look” setup from Kang et al and uses scene–product triplets to learn visual style compatibility.  

## Project goals  

- Learn embeddings that represent the style of a scene and candidate products.  
- Model both global style and local region information within a scene.  
- Use triplet loss to rank compatible products above incompatible ones.  
- Evaluate performance using accuracy, mean reciprocal rank and visual diagnostics.  

## Data  

- Base dataset: **STL-Fashion** and related “Shop-The-Look” data, processed into a “Complete-The-Look” (CTL) format.  
- The preprocessed dataset includes:  
  - 29,429 scene images.  
  - 38,098 product images.  
  - 72,173 compatible scene–product pairs with bounding boxes and category labels.  
- Triplet construction: for each scene, a positive product from within the scene and a negative product from the same category but a different scene.  
- The compatibility pattern is illustrated on page 1 of the accompanying report with a plot of scene–product compatibility scores, which shows clear separation between positive and negative pairs.  

## Methods  

### Architecture  

- Backbone: ResNet-50 pre-trained on ImageNet, used as a frozen feature extractor for both scene and product images.  
- Global features from the final convolutional block represent overall scene and product style.  
- Local features come from an intermediate convolutional block, reshaped to a grid of regional descriptors to capture spatial detail.  
- All features pass through two-layer feed-forward networks with batch normalisation, ReLU, dropout and L2 normalisation to produce:  
  - Global scene embeddings.  
  - Global product embeddings.  
  - Local scene region embeddings and category-specific bias terms.  

### Compatibility and training  

- Global compatibility is the L2 distance between global scene and product embeddings.  
- Local compatibility uses a category-aware attention mechanism that weights scene regions according to how relevant they are for the product category. Local distances are aggregated with these attention weights.  
- A hybrid compatibility score averages global and local distances.  
- Training uses a triplet hinge loss with a margin, which encourages positive pairs to be closer than negative pairs by at least that margin.  

## How to use this repository  

Suggested workflow.  

1. Set up a Python environment with TensorFlow or Keras and standard imaging libraries.  
2. Download or prepare the CTL triplets, ensuring paths to scene and product images, bounding boxes and categories are correct.  
3. Run the data preparation script or notebook to load triplets and build batches.  
4. Build the Keras model with shared ResNet-50 backbones for scene and product streams.  
5. Train the model using the triplet loss. Monitor training loss, which in the original experiments drops steadily across 50 epochs.  
6. Evaluate binary comparison accuracy and mean reciprocal rank, and generate t-SNE plots and attention maps if desired.  

Adapt any file names and paths to your actual project structure.  

## Results  

- Binary comparison accuracy of about 69 per cent, very close to the 70 per cent reported in Kang et al.  
- Mean reciprocal rank between about 0.47 and 0.52 across product categories such as topwear, footwear and accessories, which means the correct product is usually within the top two suggestions.  
- Training loss falls from roughly 0.18 to 0.09 over 50 epochs, which indicates stable convergence even with CPU-only training.  

## Reproducibility  

To mirror the reported behaviour.  

- Use frozen ResNet-50 backbones and 128-dimensional embeddings with shared parameters for global scene and product streams.  
- Train with Adam, minibatch size 16, a margin of 0.2 in the triplet loss and around 50 epochs.  
- Keep the same triplet construction process, including the requirement that negatives come from the same category but a different scene.  

## Acknowledgements and references  

The project replicates and extends the Complete-The-Look work by Kang et al and draws on earlier Siamese network applications to visual similarity and “Shop-The-Look” recommendation.  



