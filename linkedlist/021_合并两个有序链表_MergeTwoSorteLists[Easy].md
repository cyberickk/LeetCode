# 021 合并两个有序链表 Merge Two Sorted Lists [Easy]

解法一：循环遍历，含头节点

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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1==NULL)return l2;
        if(l2==NULL)return l1;
        ListNode dummy = ListNode(0);
        if(l1->val <= l2->val)
        {
            dummy.next = l1;
            l1 = l1->next;
        }
        else
        {
            dummy.next = l2;
            l2 = l2->next;
        }
        ListNode *newnode = dummy.next;
        while(l1 != NULL && l2 != NULL)
        {
            if(l1->val <= l2->val)
            {
                newnode->next = l1;
                l1 = l1->next;
            }
            else
            {
                newnode->next = l2;
                l2 = l2->next;
            }
            newnode = newnode->next;
        }
        newnode->next = (l1 == NULL) ? l2 : l1;
        return dummy.next;
    }
};
```





链表的注意事项：

- 创建新节点 ` ListNode dummy = ListNode(0);` 新节点 val = 0，next 默认为 NULL
- 节点引用成员对象， `dummy.val` 是 int 型，`dummy.next` 是节点指针
- 创建节点指针 `*newnode`  指向 `dummy.next,` 指针的下一个 `newnode->next`  
- 访问指针所指向的节点成员对象 `newnode->val`  `newnode->next` 



解法二：递归

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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1==NULL)return l2;
        if(l2==NULL)return l1;
        if(l1->val <= l2->val)
        {
            l1->next = mergeTwoLists(l1->next, l2);
            return l1;
        }
        else
        {
            l2->next = mergeTwoLists(l1,l2->next);
            return l2;
        }
    }
};
```



