# Practical Deep Learning Competition - Image Classification

This repository contains my submission for the final competition of the **"Practical Deep Learning"** course at **FIT, ČVUT**.  
Course link: [NIE-PDL](https://courses.fit.cvut.cz/NIE-PDL) | Additional course details: [bilakniha (NIE-PDL)](https://bilakniha.cvut.cz/cs/predmet7580706.html#gsc.tab=0)


## Competition Overview

In this competition, the task is to classify images of paintings into six different artistic styles. The styles are represented by the following six artists:

- Vincent van Gogh  
- Salvador Dalí  
- Claude Monet  
- Rembrandt Harmenszoon van Rijn  
- Pablo Picasso  
- Andy Warhol  

The dataset was generated using the Stable Diffusion model.  

## Evaluation

Submissions are evaluated based on **accuracy**, which is calculated as:

`Accuracy = Number of correct predictions / Total number of predictions`


## Submission Format

For each `image_id `in the test set, you must predict the label of the given image (name of the artist). The file should contain a header and have the following format:

```sh
image_id,label
6188.png,Salvador-Dali
4895.png,Pablo-Picasso
7716.png,Andy-Warhol
etc.
```


## Implementation Details

### Model Architecture and Training
- **Backbone Architecture:** The model uses **EVA-02 Large Patch14 (448)** (`"eva02_large_patch14_448.mim_m38m_ft_in22k_in1k"`) as the feature extractor, initialized with pretrained weights.
- **Training Augmentation Pipeline:** To improve generalization, a diverse set of augmentations was applied during training. The pipeline includes:
  - Random Horizontal Flip
  - Color Jitter (adjusting brightness, contrast, saturation, and hue)
  - Random Resized Crop
  - Random Affine Transformations (including rotation and translation)
  - Random Vertical Flip
  - Random Rotation (20 degrees)
  - Random Erasing (with probability 30%)

  Additionally, the training process supports multiple augmentation strategies:
  - **Normal Augmentation:** A random subset (0–3 transforms) is applied from the list above.
  - **CutMix Augmentation:** With a 70% probability, images are combined using CutMix to blend samples.
  - **MixUp Augmentation:** Alternatively, with a 70% probability, images are mixed using MixUp.
  - **Combined Augmentation:** A combination strategy is employed where a random subset (0–2 transforms) is first applied, and then either CutMix or MixUp is applied based on a random threshold.

- **Test Time Augmentation (TTA):** During inference, multiple augmented versions of each test image are processed. Augmentations for TTA include:
  - Horizontal Flip
  - Vertical Flip
  - Random Rotation (15 degrees)
  
  Predictions from these augmented images are averaged to produce the final result.

### Hardware Constraints and Adjustments
- **Batch Size Reduction:** Due to memory limitations on Kaggle’s P100 GPU, the batch size was **decreased** to fit the model in memory.
- **Inference Memory Optimization:** The inference loop was divided into **smaller chunks** to avoid exceeding RAM limits.
- **Training Time:** The full training process took approximately **8 hours**.



## Results

My solution ranked **1st place** on the **Private Leaderboard** with an **accuracy of 0.8826**.

The complete implementation can be found in [`solution.ipynb`](solution.ipynb).
