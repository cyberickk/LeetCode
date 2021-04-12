# 1302 Deepest Leaves Sum

[https://leetcode.com/problems/deepest-leaves-sum/](https://leetcode.com/problems/deepest-leaves-sum/)

Given the `root` of a binary tree, return *the sum of values of its deepest leaves*.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2019/07/31/1483_ex1.png)

```
Input: root = [1,2,3,4,5,null,6,7,null,null,null,null,8]
Output: 15
```

**Example 2:**

```
Input: root = [6,7,8,2,7,1,3,9,null,1,4,null,null,null,5]
Output: 19
```

 

**Constraints:**

- The number of nodes in the tree is in the range `[1, 104]`.
- `1 <= Node.val <= 100`



## Iterative Solution

层次遍历找最底层的叶子结点，遍历到每一层时，存储当前所有叶子结点的值，如果遍历到下一层就把之前的和清零，重新计算。

时间复杂度 O(n)，空间复杂度 O(logn)

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int deepestLeavesSum(TreeNode* root) {
        int sum = 0;
        queue<TreeNode*> que;
        que.push(root);
        while(!que.empty()){
            sum = 0;
            int size = que.size();
            while(size--){
                TreeNode* tp = que.front();
                que.pop();
                if(tp->left)    que.push(tp->left);
                if(tp->right)   que.push(tp->right);
                if(tp->left == NULL && tp->right == NULL)  
                    sum += tp->val;
            }
        }
        return sum;
    }
};
```

Runtime: 28 ms, faster than 98.37% of C++ online submissions for Deepest Leaves Sum.

Memory Usage: 38.7 MB, less than 36.59% of C++ online submissions for Deepest Leaves Sum.





## Recursive Solution

递归解法，首先得到树的高度，其次遍历结点并对比高度，当结点的高度和树高相等时进行求和。

时间复杂度 O(n)，空间复杂度 O(1)

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int deepestLeavesSum(TreeNode* root) {
        int d = getDepth(root);        
        return getSum(root, d, 1);
    }
private:
    int getDepth(TreeNode* root){
        if(root == NULL)
            return 0;
        return 1 + max(getDepth(root->left), getDepth(root->right));
    }
    int getSum(TreeNode* root, int d, int cur){
        if(root == NULL)
            return 0;
        if(cur == d)
            return root->val;
        return getSum(root->left, d, cur+1) + getSum(root->right, d, cur+1);
    }
};
```

Runtime: 40 ms, faster than 60.20% of C++ online submissions forDeepest Leaves Sum.

Memory Usage: 38.1 MB, less than 88.69% of C++ online submissions for Deepest Leaves Sum.