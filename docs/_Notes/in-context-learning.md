# In-context Learning (ICL)

## 1. Definition

In-context Learning or ICL was defined in ["Language Models are few-shot learners"](https://arxiv.org/abs/2005.14165) by Brown et al., the paper that introduced GPT-3. The authors define ICL as:

> _During unsupervised pre-training, a language model develops a broad set of skills and pattern recognition abilities. It then uses these abilities at inference time to rapidly adapt to or recognize the desired task. We use the term “in-context learning” to describe the inner loop of this process, which occurs within the forward-pass upon each sequence._

## 2. ICL vs Size of the Model

[Akyürek et al.](https://arxiv.org/abs/2211.15661) make another observation that ICL exhibits _algorithmic phase transitions_ as model depth increases:

* One-layer transformers’ ICL behavior approximates a single step of gradient descent, while wider and deeper transformers match ordinary least squares or ridge regression solutions.
* It is possible to imagine that if small models implement simple learning algorithms in-context, larger models might implement more sophisticated functions during ICL.
* Smaller models do not seem to learn from in-context examples, and larger ones do.

## 3. Related Discussion

1. In [[2-icl-over-graphs-PRODIGY|ICL over Graphs : PRODIGY]], I covered the paper ["PRODIGY : Enabling in-context learning over graphs"](https://arxiv.org/abs/2305.12600) which extends the concept of ICL to graphs.


