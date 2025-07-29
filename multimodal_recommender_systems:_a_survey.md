# _Multimodal Recommender Systems: A Survey_ notes

Paper: [https://arxiv.org/abs/2302.03883](https://arxiv.org/abs/2302.03883)

## Definitions
  * **Modality**: form of media _describing_ the content, the user, or the interactions between them. e.g. (text): user reviews, product descriptions, (video): game/movie trailers, product demo clips
  * **Semantic space**: a dimensionality or format that allows for meaningful combinations of features that came from different types of multimedia.

----------

## Example Given: Movie Recommendations

  Assume a movie recommendation system, like Netflix or Amazon Video. The multimodal features are things like posters (image), PR blurbs (text), and trailers (video). There are also traditional numeric features like year released and rating. Working with the interactions or combinations of these features is complicated since they cannot share an embedding layer, at least not easily. Even if you create embedding models that project each feature into a vector space with the same dimensionality, they each live in different semantic spaces. So there are two challenges identified: (1) feature engineering/data representation, and (2) converting the features into a common "semantic space".

  An additional problem is sparsity. Even with good representations of multimodal features, user-item interactions in recommendation systems are still very sparse.

  In other words:

### Challenges in Multimodal Recommender Systems:

1. Feature representation
1. Creating meaningful feature interactions
1. Sparsity
1. Performance

## Modality Encoding

  Getting good representations of the multimedia features is key. Some common model architectures for creating them are listed in the table below:

### Embeddings by Media Type

| Type                      | Technique                                                                                       |
| ------------------------  | ----------------------------------------------------------------------------------------------- |
| Text                      | Word2Vec, recurrent neural networks, convolutional neural networks, sentence transformers, BERT |
| Image                     | Convolutional neural networks, residual neural networks, transformers                           |
| Other (e.g. sound, video) | Conversion to other media type or prepublished feature vectors                                  |

## Feature Interaction

  The problem of representing text, image, audio, and visual features has many known solutions that were listed immediately above. However the representations listed above are typically sparse and also live in different semantic spaces.

  There are three types of interactions the paper identifies:

### 1. Bridge

  **Objective:** Create a common semantic space for all modaities.

  One problem (or area for improvement) for traditional, older recsys, is that interactions between users and multimedia features have not been sufficiently explored, but rather, those features are used to enhance the representation of the items to recommend (? not sure this is correct).

  They suggest three ways to use this information to produce more meaningful interactions, and through that, better models.

1. **User-item graphs**: Understanding users' preferences for different modalities is something that can clearly improve recommendations; if all are equally weighted, the recommendation system is suboptimal. A model called MMGCN creates a user-item bipartite graph for each modality, and modifies those graphs' structure during training to remove links between incorrect data (e.g. user clicks "not interested" on a video). There are other models that use attention, and/or can modify the weights of each modality based on user preference, which MMGCN and GRCN don't.
1. **Item-item graphs**: Item-item graphs are valuable because they can be used to create better item representations. LATTICE constructs an item-item graph for each modality, based on the user-item graph, and then aggregates those to obtain latent item-item graphs for each modality.
1. **Knowledge graphs**: Knowledge graphs are useful because they can provide auxiliary information for recommender systems.

### 2. Fusion

  **Objective:** Create a single feature vector containing all the data for the items that are recommended to users.

  Techniques used include:

1. **Coarse-grained attention**
1. **Fine-grained attention:** Multimodal data contains both global and fine-grained features. Fine-grained attention fuses fine-grained information between different modalities, which is used especially in fashion.
1. **Combined attention**

  Other alternatives the authors discuss in passing include gating and concatenating features. These fusion techniques are usually combined with others like the attention methods mentioned above and graph representations.

### 3. Filtration

  **Objective:** Remove noise, which is a bigger problem in more information-rich modalities (e.g. video).

  Techniques used include image segmentation (VECF, UVCAN) and margin identification (MM-Rec).

  Graph neural networks are also used here, like FREEDOM, GRCN, and PMGRCN.

## Feature Enhancement

  One thing that makes multimodal features so complex is that different modality representations of the same items (i.e. a movie's poster vs. its' PR blurb) have an overlap, but not a complete one, in what information they carry about the item. "Therefore, the recommendation performance and generalization of multimodal recommender systems can be significantly improved if the unique and common characteristics can be distinguished."

### 1. Disentangled Representation Learning

  Decomposition of multimodal features in order to extract helpful information that is entangled between the various modalities. Models include DICER, MacridVAE, CDR, MDR, DMRL, PAMD, and SEM-MacridVAE.

### 2. Contrastive Learning

  Figure out the relationship between positive and negative examples. Uses data augmentation to enhance the representation, and optimizes based on contrastive loss. Techniques include GHMFC, Cross-CRB, MICRO, and CMCKG.

## Model Optimization

  Recsyses which use multimodal encoding require significantly more resources to train than traditional recsys models do, because of the greater volume and complexity of their data.

  The paper's authors suggest two approaches, end-to-end training and two-step training. End-to-end training seeks to be more efficient (faster/cheaper/smaller), while two-step training aims to perform better.

### 1. End-to-end training

  **Objective:** Minimize training time and resources required by using pretrained encoders and only optimize based on to "an end-to-end pattern."

  AN example of how large these models get is Vit-Base, which has 86 million parameters. Example models for this include NOVA and VLSNR have pretrained encoders for image and text features. An alternative is fine-tuning using a small number of epochs ("only 100") and using recommendation and contrastive loss.

  Yet another method used is reducing the number of parameters that get updated while training:

1. **MKGformer:** shares many attention layer parameters.
2. **FREEDOM:** freezes some parameters of the graph structure, which also has a denoising effect.

### 2. Two-step training

  **Objective:**

## Tools

1. **MMRec**: Multimodal recommendation toolbox based on PyTorch.
1. **Cornac**:

## Challenges and the future
