# 142 Linked List Cycle II 

[https://leetcode.com/problems/linked-list-cycle-ii/](https://leetcode.com/problems/linked-list-cycle-ii/)

Given a linked list, return the node where the cycle begins. If there is no cycle, return `null`.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to. **Note that `pos` is not passed as a parameter**.

**Notice** that you **should not modify** the linked list.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

```
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png)

```
Input: head = [1,2], pos = 0
Output: tail connects to node index 0
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```

**Example 3:**

![img](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png)

```
Input: head = [1], pos = -1
Output: no cycle
Explanation: There is no cycle in the linked list.
```

 

**Constraints:**

- The number of the nodes in the list is in the range `[0, 104]`.
- `-105 <= Node.val <= 105`
- `pos` is `-1` or a **valid index** in the linked-list.



## Two Pointers

采用 Floyd Cycle Detection 算法，龟兔赛跑双指针的思想，龟走一步兔走两步，相遇时停下；一方从 head 重新出发，同时一步一步前进，再次相遇时即为环的起始点。

因为链表涉及到空指针，所以需要先提前判断是否为空，防止运行报错。

时间复杂度 O(n)，空间复杂度 O(1)

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode *pos = NULL, *tortoise = head, *hare = head;
        if(head == NULL || head->next == NULL)
            return NULL;
        while(tortoise->next && hare->next){
            tortoise = tortoise->next;
            hare = hare->next;
            if(tortoise == NULL || hare == NULL)
                return NULL;
            hare = hare->next;
            if(hare == NULL)
                return NULL;
            if(hare && tortoise && hare == tortoise)
                break;
        }
        
        tortoise = head;
        while(tortoise != hare){
            if(tortoise == NULL || hare == NULL)
                return NULL;
            tortoise = tortoise->next;
            hare = hare->next;
        }
        
        return hare;
    }
};
```

Runtime: 8 ms, faster than 81.59% of C++ online submissions for Linked List Cycle II.

Memory Usage: 7.5 MB, less than 88.27% of C++ online submissions for Linked List Cycle II.



<br>

代码简化后如下

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        if(!head)   return NULL;
        ListNode *hare = head, *tortoise = head;
        while(hare->next && hare->next->next){
            tortoise = tortoise->next;
            hare = hare->next->next;
            if(hare == tortoise){
                tortoise = head;
                while(tortoise != hare){
                    tortoise = tortoise->next;
                    hare = hare->next;
                }
                return hare;
            }
        }
        return NULL;
    }
};
```

Runtime: 8 ms, faster than 81.59% of C++ online submissions for Linked List Cycle II.

Memory Usage: 7.6 MB, less than 69.29% of C++ online submissions for Linked List Cycle II.