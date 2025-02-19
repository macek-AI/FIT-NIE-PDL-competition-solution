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

## Results

My solution ranked **1st place** on the **Private Leaderboard** with an **accuracy of 0.8826**.

The complete implementation can be found in [`solution.ipynb`](solution.ipynb).
