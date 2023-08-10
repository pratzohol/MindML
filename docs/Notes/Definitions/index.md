---
tags:
    - Basics
---

# Definitions

## 1. Overview

This post will contain definition of various terms that I come across while reading papers and articles. I will try to keep it updated as I learn more about new terms.

These terms are not that complex and time consuming to understand and hence, does not deserve separate posts. So, I will keep on adding them here.

## 2. Glossary

### # CCS Concepts
"CCS Concepts" typically refers to the concepts or topics within the field of computer science that are relevant to the research presented in the paper. CCS stands for "ACM Computing Classification System," which is a standardized classification system used in the computer science community to categorize research papers and topics.

### # CI.yml
CI.yml is a configuration file used in continuous integration (CI) workflows. It is commonly used in conjunction with tools like GitHub Actions, GitLab CI/CD, or other CI/CD platforms. The "ci.yml" file contains instructions and settings for automating the build, test, and deployment processes of a software project. It defines the steps, dependencies, environment variables, and other parameters required to perform automated testing and integration tasks.

### # Pre-train, Fine-tune
The pre-train, fine-tune paradigm is a common approach used in transfer learning, particularly in the context of deep learning models. It involves two main stages:

1. _Pre-training_ : In the pre-training stage, a neural network model is trained on a large and diverse dataset, typically on a related but different task. This initial training is called "pre-training" because the model is not yet specialized for the specific downstream task of interest. Instead, it learns general features and representations from the data in an unsupervised or supervised manner.
2. _Fine-tune_ :  In this stage, the pre-trained model is further trained on a smaller, task-specific dataset. During fine-tuning, the earlier layers of the model, which capture more generic features, are usually frozen or updated with a lower learning rate to preserve the general knowledge learned during pre-training. The later layers, which capture more task-specific information, are updated with a higher learning rate to allow the model to specialize for the specific task.

CONS : There might be a large training gap between the pre-trained model and the downstream task. This can lead to a phenomenon called "catastrophic forgetting," where the model forgets the general knowledge learned during pre-training as it learns the task-specific information during fine-tuning. This also leads to large fine-tuning time which might become comparable to the training time and hence, becomes computationally expensive.

### # Secure Multiparty Computation (SMC)

SMC allows a number of mutually distrustful parties to carry out a joint computation of a function of their inputs, while preserving the privacy of the inputs.