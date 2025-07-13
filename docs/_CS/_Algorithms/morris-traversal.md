---
title: Morris Traversal of Tree
---

## Problem 

Print _in-order_, _pre-order_ and _post-order_ traversal of tree in $O(N)$ time and $O(1)$ space constraints without using any data structures such as stacks or queues.

## Algorithm

### In-order

- If there is no left subtree, then we just push `root->val` to result and move to right (`root = root->right`)
- Otherwise, we find the _inorder predecessor_, let's say `prev` of `root` (This is the value which will pe pushed just before `root->val`)
- We notice that this value will be the rightmost child of left subtree
- Now, we need to maintain a link from _inorder predecessor_ to the `root` node
- So, we assign `root` as right child of _inorder predecessor_ (`prev->right = root`)
- Now, when we have processed the left subtree, we will find that the `prev->right != nullptr`. 
- In that case, we need to push `root->val` to result and remove the connection, i.e., `prev->right = nullptr` and move the `root` to right subtree.

### Pre-order

- If there is no left subtree, then we just push `root->val` to result and move to right (`root = root->right`)
- Otherwise, we find the _inorder predecessor_, let's say `prev` of `root` (This is the value after which right subtree will pe printed)
- We notice that this value will be the rightmost child of left subtree
- Now, we need to maintain a link from _inorder predecessor_ to the `root` node
- So, we assign `root` as right child of _inorder predecessor_ (`prev->right = root`) and push `root->val` to result.
- Now, when we have processed the left subtree, we will find that the `prev->right != nullptr`. 
- In that case, we need to remove the connection, i.e., `prev->right = nullptr` and move the `root` to right subtree.

### Post-order

- Post-order is `Left -> Right -> Root` which is reverse of Pre-order and switching left and right links.
- So, algorithm is same as Pre-order, instead we find leftmost chuld of right subtree as predecessor.
- And, instead of assigning right child, we assign left child.

## Code

### In-order

```Cpp
vector<int> preOrder(Node* root) { 
    vector<int> res;

    while (root)  { 
      	// If left child is null, print the prev node val. Move to right child. 
        if (root->left == nullptr)  { 
            res.push_back(root->val);
            root = root->right; 
        } 
        else { 
          	// Find inorder predecessor 
            Node* prev = root->left; 
            while (prev->right && prev->right != root) 
                prev = prev->right; 

            // If the right child of inorder predecessor already points to this node then print this node
            if (prev->right == root)  { 
                prev->right = nullptr; 
                res.push_back(root->val);
                root = root->right; 
            } 

            // If right child doesn't point to this node, make right child point to this node 
            else { 
                prev->right = root; 
                root = root->left; 
            } 
        } 
    } 

    return res;
}
```

### Pre-order

```Cpp
vector<int> preOrder(Node* root) { 
    vector<int> res;

    while (root)  { 
      	// If left child is null, print the prev node val. Move to  right child. 
        if (root->left == nullptr)  { 
            res.push_back(root->val);
            root = root->right; 
        } 
        else { 
          	// Find inorder predecessor 
            Node* prev = root->left; 
            while (prev->right && prev->right != root) 
                prev = prev->right; 

            // If the right child of inorder predecessor already points to this node 
            if (prev->right == root)  { 
                prev->right = nullptr; 
                root = root->right; 
            } 

            // If right child doesn't point to this node, then print this node and make right child point to this node 
            else { 
                res.push_back(root->val);
                prev->right = root; 
                root = root->left; 
            } 
        } 
    } 

    return res;
}
```

### Post-order

```Cpp
vector<int> postOrder(Node* root) { 
    vector<int> res;

    while (root)  { 
      	// If left child is null, print the prev node val. Move to left child. 
        if (root->right == nullptr)  { 
            res.push_back(root->val);
            root = root->left; 
        } 
        else { 
          	// Find predecessor 
            Node* prev = root->right; 
            while (prev->left && prev->left != root) 
                prev = prev->left; 

            // If the left child of predecessor already points to this node 
            if (prev->left == root)  { 
                prev->left = nullptr; 
                root = root->left; 
            } 

            // If left child doesn't point to this node, then print this node and make left child point to this node 
            else { 
                res.push_back(root->val);
                prev->left = root; 
                root = root->right; 
            } 
        } 
    } 

    // reversing the list to get correct post-order nodes
    reverse(res.begin(), res.end());
    return res;
}
```

## Complexity

Each node will be visited maximum of two times, once to find the _inorder predecessor_, and next time when the connection between `prev` and `root` is already established. So, T = $O(2N)$