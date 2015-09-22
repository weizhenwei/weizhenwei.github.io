---
layout: post
title: "On Recursion and iteration in algorithm"
date: 2015-09-22 22:59:40 +0800
comments: true
categories: algorithm
---

&emsp;&emsp;本文是刷leetcode的一点心得。  

###1 算法设计领域的迭代和递归

&emsp;&emsp;在计算机程序设计或者算法设计领域，迭代和递归在本质上是一致的：
每次递归或迭代是为了解决原问题的子问题，然后根据子问题的结果和当前问题的状态
综合求解当前问题。所不同的是：在递归方法中，先求得子问题的解，然后接合当前
状态求得问题结果。而在迭代方法中，使用栈保存当前问题的求解状态，然后把当前问题
分解为子问题，并把当前状态和子问题入栈；接下来对栈中的元素迭代求解，并记录最终
结果的中间状态，直到栈为空，此时返回最终的求解结果。  
&emsp;&emsp;对于很多问题，用递归的方法很容易就容易解决，而用迭代的方法则不那么
直观，甚至感觉难以下手。这是因为在递归方法中，保存中间结果和栈的操作都交由函数
调用去实现了，而在迭代方法中，这些都需要在算法中手动处理。不过，只要能认识到递归
和函数其实是一样的，那么就可以很自信的说：能用递归解决的问题就一定能用迭代解决。  
&emsp;&emsp;下面以一些leetcode中的题目为例进行分析。  

###2 例题
&emsp;&emsp;[Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)  
Recursive Version:  
```c++
    TreeNode* invertTreeRecursive(TreeNode* root) {  
        if (root == NULL || (root->left == NULL && root->right == NULL)) {  
            return root;  
        }  
  
        if (root->left) {  
            root->left = invertTreeRecursive(root->left);  
        }  
        if (root->right) {  
            root->right = invertTreeRecursive(root->right);  
        }  
        TreeNode *tmpNode = root->left;  
        root->left = root->right;  
        root->right = tmpNode;  
        return root;  
    }  
  
```

Iterative Version:  
```c++
    TreeNode* invertTreeIterative(TreeNode* root) {  
        if (root == NULL || (root->left == NULL && root->right == NULL)) {  
            return root;  
        }  
  
        stack<TreeNode*> theStack;  
        theStack.push(root);  
        while (!theStack.empty()) {  
            TreeNode *topNode = theStack.top();  
            if (topNode->left == NULL && topNode->right == NULL) {  
                theStack.pop();  
            } else {  
                TreeNode *tmpNode = topNode->left;  
                topNode->left = topNode->right;  
                topNode->right = tmpNode;  
  
                theStack.pop();  
                if (topNode->left) {  
                    theStack.push(topNode->left);  
                }  
                if (topNode->right) {  
                    theStack.push(topNode->right);  
                }  
            }  
        }  // while  
  
        return root;  
    }  
```

###3 结论
&emsp;&emsp;能用递归解决的问题，就一定能用迭代解决。  

