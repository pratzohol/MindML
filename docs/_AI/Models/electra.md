---
title: ELECTRA
---

# ELECTRA

## 1. Introduction

This paper introduced the pre-training objective of [**Replaced Token Detection (RTD)**](./codebert.md#32-rtd) which is sample-efficient compared to traditional MLM which utilizes only 15% of tokens for pre-training. Using very less compute, it outperforms lot of models by a significant margin.

## 2. Pre-training Objective

Two neural networks are trained, namely, generator $G$ and discriminator $D$. Both works as encoders. The generator $G$ is trained with $\text{MLE}$ loss instead of training it adversarially as earlier works show it is difficult to apply GANs to text.


For $\boldsymbol{x} = [x_1, x_2, .., x_n]$ as input, we get contextualized embeddings $h(\boldsymbol{x}) = [h_1, h_2, .., h_n]$.  

- First, select positions to mask-out tokens, replace them with $[MASK]$.  
- Generator then predicts the masked tokens.  
- Masked tokens are replaced by generator samples.  
- Discriminar predicts if the token is "real".

$$
\begin{array}{ll}
m_i \sim \text{unif}\{1, n\} \quad \text{for } i = 1 \text{ to } k 
& \quad \boldsymbol{x}^{\text{masked}} = \text{REPLACE}(x, \boldsymbol{m}, [\text{MASK}]) \\
\hat{x}_i \sim p_G(x_i \mid \boldsymbol{x}^{\text{masked}}) \quad \text{for } i \in \boldsymbol{m}
& \quad \boldsymbol{x}^{\text{corrupt}} = \text{REPLACE}(x, \boldsymbol{m}, \hat{\boldsymbol{x}})
\end{array}
$$

### 2.1 Generator

For position $t$, where $x_t = [MASK]$, we first get probability distribution over the vocabulary $V$ by taking softmax after calculating dot product with embedding matrix $E$. The probability of generating token $x_t$ is given by,

$$
p_G(x_t \mid \boldsymbol{x}) = 
    \dfrac{\exp (E{x_t}^T \cdot h_G(\boldsymbol{x})_t)}{\sum_{x'} \exp (E{x'}^T \cdot h_G(\boldsymbol{x})_t)}
$$

The generator $G$ is trained using this $\text{MLE}$ loss function: 

$$
\mathcal{L}_{MLM}(\boldsymbol{x}, \theta_G) = 
\mathbb{E} \left(
    - \sum_{i \in \boldsymbol{m}} \log p_G(x_i \mid \boldsymbol{x}^{\text{masked}})
\right)
$$

### 2.2 Discriminator

For the discrimintor, it outputs a probability whether $x_t$ is "real". 

$$
D(\boldsymbol{x}, t) = sigmoid(w^T h_D(\boldsymbol{x}_t))
$$

The loss function for Discriminator $D$ is given by,

$$
\mathcal{L}_{\text{Disc}}(\boldsymbol{x}, \theta_D) = 
\mathbb{E} \left( 
\sum_{t = 1}^{n} 
- \mathbb{1}(x_t^{\text{corrupt}} = x_t) \log D(\boldsymbol{x}^{\text{corrupt}}, t)
- \mathbb{1}(x_t^{\text{corrupt}} \ne x_t) \log (1 - D(\boldsymbol{x}^{\text{corrupt}}, t))
\right)
$$

---

The combined pre-training objective to minimize then becomes :

$$
\min\limits_{\theta_G, \theta_D} \sum_{\boldsymbol{x} \in \mathcal{X}} 
\mathcal{L}_{MLM}(\boldsymbol{x}, \theta_G) + \lambda \mathcal{L}_{\text{Disc}}(\boldsymbol{x}, \theta_D)
$$

$\lambda$ is taken 50 since the loss of discriminator is very small compared to generator. After pre-training is done, we discard the generator model and use the discriminator. 

## 3. Pre-training Data

- 3.3 Billion tokens from **Wikipedia** and **BookCorpus**.
- For ELECTRA-Large model, it's trained on 33B tokens by including data from **ClueWeb**, **CommonCrawl**, and **Gigaword**.

## 4. Pre-training Setup for G-D 

- **Weight Sharing**: We use common $E$ for both $G$ and $D$. Hidden dimension is taken to be same as $D$'s hidden state. This is because, $D$ only updates tokens tht are present in input or sampled by generator. Whereas $G$ updates every token because of the $softmax$.
- **Smaller Generator**: If smaller $G$ is taken, first we add linear layer to project $E$ into $G$'s hidden state. Model works best with $G$ that are 1/2 or 1/4 of size of $D$. We don't want a weak $G$ but also don't want a very strong $G$ which correctly detects the token most of the time.
- **Training Algorithm**: If we first separately train $G$, it becomes too good at prediction and $D$ can cheat the system by predicting "real" everytime. Thus, both are trained jointly.

## 5. ELECTRA 