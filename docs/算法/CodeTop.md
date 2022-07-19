# 1-10

## 1、反转链表 

[题目链接](https://leetcode.cn/problems/reverse-linked-list/)

### 解题思路：

递归或者双指针迭代



### 递归解法：

```cpp
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
    ListNode* reverseList(ListNode* head) {
        //头节点不存在或者第二个节点不存在，直接返回head
        if(!head || !head->next) return head;
        //递归调用
        auto tail = reverseList(head->next);
        //更新head节点与head->next节点之间的指针
        head->next->next = head;
        head->next = nullptr;
        //返回反转后的节点
        return tail;
    }
};
```



### 双指针迭代解法：

```cpp
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
    ListNode* reverseList(ListNode* head) {
        if(!head) return head;
        //从最前面两个节点开始迭代
        auto a = head, b = head->next;
        //当指针b依然存在
        while(b)
        {
            auto c = b->next;
            //改变指针指向
            b->next = a;
            //移动a指针到b指针的位置
            a = b;
            //移动b指针到c指针的位置
            b = c;
        }

        head->next = nullptr;
        //双指针迭代结束时a指针指向最后一个节点，b指针指向null
        return a;

    }
};
```



## 2、无重复字符的最长子串

[题目链接](https://leetcode.cn/problems/longest-substring-without-repeating-characters/)





## 3、LRU缓存机制

[题目链接](https://leetcode.cn/problems/lru-cache/)



## 4、数组中的第K个最大的数

[题目链接](https://leetcode.cn/problems/kth-largest-element-in-an-array/)



## 5、K个一组翻转链表

[题目链接](https://leetcode.cn/problems/reverse-nodes-in-k-group/)



# 11-20



# 21-30



# 31-40



# 41-50

