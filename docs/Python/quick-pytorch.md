---
title: "Pytorch Nuggets"
tags:
    - pytorch
---

# Pytorch Nuggets : A collection of short notes

## 1. Torch and Numpy

- Default `dtype` of numpy is `float64` whereas for pytorch, it is `float32`. 
- Thus, use `ndarray.from_numpy().type(torch.float32)` to convert numpy array to pytorch tensor.
- `torch.Tensor.numpy()` converts pytorch tensor to numpy array. Data type will be `float32`. 

## 2. Reshape, View, squeeze, unsqueeze

- **View** just changes the shape but addresses the same memory. Thus, if you change any value after view operation, it will change the original tensor as well.
- **Reshape** creates a copy of the tensor and thus, changes in reshaped tensor will not affect the original tensor.
- **Squeeze** removes all the dimensions with size 1. For example, `A x 1 x B x 1 X C` will return `A x B x C`.
- **Unsqueeze** adds a dimension of `1` at specified `dim`.

## 3. Evaluation mode

- Instead of using `torch.no_grad`, its better to use `torch.inference_mode` as it is more efficient.

## 4. Random Seed

- Use `torch.manual_seed( <int> )` to set the random seed for all the modules.

## 5. Mean 

- `dtype` of the tensor can only be `float` or `complex` for `torch.mean()`.