# Contrastive Learning

## Definition

> Contrastive learning aims at learning low-dimensional representations of data by contrasting between similar and dissimilar samples.

What this means is that it tries to bring similar samples close to each other in the representation space and push dissimilar samples away from each other.

Let's suppose we have 3 images, $I_1$, $I_2$ and $I_3$, where $I_1$ and $I_2$ belongs to same class (e.x. dog) and $I_3$ belongs to different class (e.x. cat). The representation space will look something like this:

![svg-1](../../assets/Notes/Miscellaneous/contrastive-learning-1.drawio.svg)

We see that the distance $d(x_1, x_2)$ is small compared to $d(x_1, x_3)$ and $d(x_2, x_3)$ where $d()$ is a metric function like euclidean.

[//]: # (comment in markdown looks like this)

## Loss Functions

### Contrastive Loss 

We suppose that we have a pair ($I_i$, $I_j$) and a label $Y$ that is equal to 0 if the samples are similar and 1 otherwise. To extract a low-dimensional representation of each sample, we use a Convolutional Neural Network $f$ that encodes the input images $I_i$ and $I_j$ into an embedding space where $x_i = f(I_i)$ and $x_j = f(I_j)$. The contrastive loss is defined as:  


### Triplet Loss
