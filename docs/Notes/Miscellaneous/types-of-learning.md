---
tags:
    - Basics
---

# Types of Learning

There are broadly 3 different types of learning in Machine Learning paradigm:

* Supervised Learning
* Unsupervised Learning
* Semi-supervised Learning

## 1. Supervised Learning

When we have lots of labeled samples and we want to train our model to learn from these samples, we use Supervised Learning. Model's performance is measure against a test set which is not seen during training. (We have true labels of the test set)

## 2. Unsupervised Learning

When we don't have any labeled data and instead model tries to discover patterns and insights without any explicit guidance or instruction. For example, clustering is an unsupervised learning task.

### 2.1. Self-supervised Learning

- This is kinda unsupervised but with an additional supervisory signal.
-  For example, one perform augmentations on the same images and label them as a positive pair, different images as negative pair, and attempts to push the learnt features of negative pairs away while dragging positive features close.
-  Constrastive learning is a type of self-supervised learning.
-  This enables the network to learn to group images of similar classes, which allows model to perform classification / segmentation tasks without having ground truths.

## 3. Semi-supervised Learning

When we have a few labeled samples and a lot of unlabeled samples, we want to be able to use both of them to optimize the performance and learning capability of our model. This is the definition of Semi-supervised Learning.