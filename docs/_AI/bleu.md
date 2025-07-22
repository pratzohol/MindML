---
title: BLEU Score
---

# BLEU Score

- BLEU stands for "Bilingual Evaluation Understudy".  
- It evaluates the quality of **text generation** by comparing n-grams of generated text, i.e., candidate with the reference text, i.e., ground truth.  
- Usually, BLEU score decreases as the length of generated text increases. This is because, in higher order n-grams, it's much more likely to be non-overlapping with the reference text.

## 1. Formula

$$\text{BLEU} = \text{BP} \cdot \exp \left(\sum_{i=1}^{N} w_i \ln p_i\right)$$

Where:

- $\text{BP}$ is **Brevity Penalty**. It is defined as 
    $\quad \text{BP} = 
    \begin{cases}
    1 & \text{if } c > r \\
    \exp\left(1 - \frac{r}{c} \right) & \text{if } c \leq r
    \end{cases}$  
    where

    $$
    \begin{aligned}
    r &= \text{length of reference text} \\
    c &= \text{length of candidate text}
    \end{aligned}
    $$

    We see $\text{BP} < 1$ for candidate text shorter than reference text. It penalizes very short outputs, but also, does not exceed 1 even if candidate text is much longer than reference text.

- $p_i$ is **clipped precision** of n-gram with length $i$. 

    $$
    p_i = \dfrac{\text{CountClip}(\text{matching-n-grams}_i, \text{max-ref-count}_i)}{\text{candidate-n-grams}_i}
    $$

- $w_i$ is weight given to n-grams with length $i$. Usually $N$ is taken upto 4. Then, in this case we can assign $w_1, w_2, w_3, w_4$ each to be $0.25$.

## 2. Smoothed-BLEU

When a candidate is short and no bigrams or trigrams match, BLEU can be zero, even if the output is reasonably close. Smoothed BLEU modifies the precision terms $p_i$ to avoid zero values when there are no matches.

This can be done using methods like adding 1 to both numerator and denominator, or backoff smoothing.