# 1721 Swapping Nodes in a Linked List

[https://leetcode.com/problems/swapping-nodes-in-a-linked-list/](https://leetcode.com/problems/swapping-nodes-in-a-linked-list/)

You are given the `head` of a linked list, and an integer `k`.

Return *the head of the linked list after **swapping** the values of the* `kth` *node from the beginning and the* `kth` *node from the end (the list is **1-indexed**).*

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/09/21/linked1.jpg)

```
Input: head = [1,2,3,4,5], k = 2
Output: [1,4,3,2,5]
```

**Example 2:**

```
Input: head = [7,9,6,6,7,8,3,0,9,5], k = 5
Output: [7,9,6,6,8,7,3,0,9,5]
```

**Example 3:**

```
Input: head = [1], k = 1
Output: [1]
```

**Example 4:**

```
Input: head = [1,2], k = 1
Output: [2,1]
```

**Example 5:**

```
Input: head = [1,2,3], k = 2
Output: [1,2,3]
```

 

**Constraints:**

- The number of nodes in the list is `n`.
- `1 <= k <= n <= 105`
- `0 <= Node.val <= 100`



# solution

重点是找到倒数第 `k` 个节点，用两个相距 `k` 的指针同时移动，后者移动到最后一个节点时前者就是倒数第 `k` 个。注意计数的边界问题，找第 `k` 个需要从 ` i = 0`  到  `i = k-1`

时间复杂度 O(n)，空间复杂度 O(1)

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* swapNodes(ListNode* head, int k) {
        ListNode *p1 = head, *pk = head, *pe = head;
        for(int i = 0; i < k - 1; ++i){
            p1 = p1->next;
            pe = pe->next;
        }
        while(pe -> next != NULL){
            pk = pk->next;
            pe = pe->next;
        }
        swap(p1->val, pk->val);
        return head;
    }
};
```

Runtime: 588 ms, faster than 83.34% of C++ online submissions for Swapping Nodes in a Linked List.

Memory Usage: 180.1 MB, less than 92.26% of C++ online submissions forSwapping Nodes in a Linked List.