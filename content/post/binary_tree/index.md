---
title: 二叉树
subtitle: 二叉树。

# Summary for listings and search engines
summary: Welcome 👋 We know that first impressions are important, so we've populated your new site with some initial content to help you get familiar with everything in no time.

# Link this post with a project
projects: []

# Date published
date: "2020-12-13T00:00:00Z"

# Date updated
lastmod: "2020-12-13T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

toc: true

pager: true

show_related: true

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: "Image credit: [**Unsplash**](https://unsplash.com/photos/CpkOjOcXdUY)"
  focal_point: ""
  placement: 2
  preview_only: false

authors:
  - admin

tags:
  - Go
  - 开源

categories:
  - 教程
# Book page type (do not modify).
# type: book
---

```cpp
#include <iostream>
#include <stack>
#include <queue>
/** 㐂◨⮳᪟ᢝ */
typedef int tree_node_elem_t;
  /*
  *@struct
  *@brief λࣸᵀ㐂◨
  */
  struct binary_tree_node_t {
  binary_tree_node_t *left; /* ጕ႘ၿ */
  binary_tree_node_t *right; /* ढ႘ၿ */
  tree_node_elem_t elem; /* 㐂◨⮳᪟ᢝ */
};
/**
* @brief ۇٴᎾ䕼ࢵ喌䕁ᒁ.
* @param[in] root ᵨ㐂◨
* @param[in] visit 䃮䬝᪟ᢝٲ㉏⮳ܬ᪟ᠶ䦷
* @return ᬏ
*/
void pre_order_r(const binary_tree_node_t *root,
int (*visit)(const binary_tree_node_t*)) {
if (root == nullptr) return;
visit(root);
pre_order_r(root->left, visit);
pre_order_r(root->right, visit);
```
