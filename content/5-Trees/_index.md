---
title : "Trees"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---
***Binary search trees*** are another data structure that can be used to store data more efficiently such that it can be searched and retrieved.

We can imagine a sorted sequence of numbers.

![trees](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/5.trees/trees1.png)

Imagine then that the center value becomes the top of a tree. Those that are less than this value are placed to the left. Those values that are more than this value are to the right.

![trees](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/5.trees/trees2.png)

Pointers can then be used to point to the correct location of each area of memory such that each of these nodes can be connected.

![trees](https://raw.githubusercontent.com/baobaoupcloud/cs-w5/main/static/images/5.trees/trees3.png)

In code, this can be implemented as follows.

```c
// Implements a list of numbers as a binary search tree

#include <stdio.h>
#include <stdlib.h>

// Represents a node
typedef struct node
{
    int number;
    struct node *left;
    struct node *right;
}
node;

void free_tree(node *root);
void print_tree(node *root);

int main(void)
{
    // Tree of size 0
    node *tree = NULL;

    // Add number to list
    node *n = malloc(sizeof(node));
    if (n == NULL)
    {
        return 1;
    }
    n->number = 2;
    n->left = NULL;
    n->right = NULL;
    tree = n;

    // Add number to list
    n = malloc(sizeof(node));
    if (n == NULL)
    {
        free_tree(tree);
        return 1;
    }
    n->number = 1;
    n->left = NULL;
    n->right = NULL;
    tree->left = n;

    // Add number to list
    n = malloc(sizeof(node));
    if (n == NULL)
    {
        free_tree(tree);
        return 1;
    }
    n->number = 3;
    n->left = NULL;
    n->right = NULL;
    tree->right = n;

    // Print tree
    print_tree(tree);

    // Free tree
    free_tree(tree);
    return 0;
}

void free_tree(node *root)
{
    if (root == NULL)
    {
        return;
    }
    free_tree(root->left);
    free_tree(root->right);
    free(root);
}

void print_tree(node *root)
{
    if (root == NULL)
    {
        return;
    }
    print_tree(root->left);
    printf("%i\n", root->number);
    print_tree(root->right);
}
```

Notice this search function begins by going to the location of `tree`. Then, it uses recursion to search for `number`. The `free_tree` function recursively frees the tree. `print_tree` recursively prints the tree.

A tree like the above offers dynamism that an array does not offer. It can grow and shrink as we wish.

Further, this structure offers a quick search time.