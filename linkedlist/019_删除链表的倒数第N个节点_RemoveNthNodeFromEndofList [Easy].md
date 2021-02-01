# 019 删除链表的倒数第N个节点 Remove Nth Node From End of List [Easy] 

给定一个链表，删除链表的倒数第 *n* 个节点，并且返回链表的头结点。

**示例：**

```
给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.
```

**说明：**

给定的 *n* 保证是有效的。

**进阶：**

你能尝试使用一趟扫描实现吗？



快慢指针，快指针先后移 n 次，然后快慢指针同时后移，快指针移动到末尾时慢指针指向的就是倒数第 n 个节点，删除该节点即可。难点是边界的处理。

时间复杂度 O(n)，空间复杂度  O(1)

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
    ListNode* removeNthFromEnd(ListNode* head, int n) {       
        if(head == NULL || head->next == NULL)
            return NULL;
        ListNode *n1 = head, *n2 = head;
        for(int i = 0; i < n; ++i)
            n2 = n2->next;
        if(n2 == NULL)
        {
            head = head->next;
            return head;
        }
        while(n2->next != NULL)
        {
            n1 = n1->next;
            n2 = n2->next;
        }
        n1->next = n1->next->next;
        return head;
    }
};
```



为了避免边界判定，新建一个空的头结点 dummy，再指向原来的 head,  fast 和 slow 都从 dummy 开始遍历，fast 向后移动 n+1 次

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
    ListNode* removeNthFromEnd(ListNode* head, int n) {       
        ListNode *dummy = new ListNode(0);
        ListNode *fast = dummy, *slow = dummy;
        dummy->next = head;
        for(int i = 0; i < n+1; ++i)
            fast = fast->next;
        while(fast) {
            fast = fast->next;
            slow = slow->next;
        }
        slow->next = slow->next->next;
        return dummy->next;
    }
};
```

