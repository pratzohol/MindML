---
title: "Number of Trainable Params"
tags:
    - Method
---

# Number of Trainable Parameters of Model

## 1. Method-1

```py
def print_num_trainable_params(torch_module):
    model_parameters = filter(lambda p: p.requires_grad, torch_module.parameters())
    params = int(sum([np.prod(p.size()) for p in model_parameters]))
    print("Number of trainable parameters of the model:", params)
    return params
```
