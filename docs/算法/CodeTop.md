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

### 解题思路：

双指针迭代+Hash

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        //使用hash表来存储字符出现的次数
        unordered_map<char, int> hash;

        //记录结果
        int res = 0;

        //双指针迭代，当j遍历到当前字符出现了两次，i指针向前遍历，指向--操作，直到hash值变为1
        for(int i = 0, j = 0; j < s.length(); j ++)
        {
            hash[s[j]] ++;
            while(hash[s[j]] > 1) hash[s[i++]] --;
            res = max(res, j - i + 1);
        }

        return res;
    }
};
```



## 3、LRU缓存机制

[题目链接](https://leetcode.cn/problems/lru-cache/)

### 什么是LRU?

LRU (Least recently used：最近最少使用)算法在缓存写满的时候，会根据所有数据的访问记录，淘汰掉未来被访问几率最低的数据。也就是说该算法认为，最近被访问过的数据，在将来被访问的几率最大。

图示：

![img](CodeTop.assets/653f0ff13dd026a13b7495477ef5b89dd74bed.png)

本题解题思路和上图一样，使用双向链表来存储数据,以Node形式—(key, value)，使用hash表来判断当前节点Node是否存在

```c++
class LRUCache {
public:
    //使用双链表维护key-value
    struct Node{
        int key, val;
        Node *left, *right;
        Node(int _key, int _val): key(_key), val(_val), left(NULL), right(NULL){}
    }*L,*R;

    //哈希表维护key, Node(key, value)
    unordered_map<int, Node*> hash;
    int n;

    //删除节点p
    void remove(Node* p){
        p->right->left = p->left;
        p->left->right = p->right;
    }

    //在双链表最左侧插入节点，代表此节点最近使用了一次，注意双链表中越靠右侧代表使用次数越少
    void insert(Node* p){
        p->right = L->right;
        p->left = L;
        L->right->left = p;
        L->right = p;
    }

    LRUCache(int capacity) {
        n = capacity;
        //定义的双链表左右节点
        L = new Node(-1, -1), R = new Node(-1, -1);
        L->right = R, R->left = L;
    }
    
    int get(int key) {
        //不存在key,则返回-1
        if(hash.count(key) == 0) return -1;
        //key存在，则取出双链表中的点，先删除此点，再将此点插入到双链表最左侧，代表最近更新了一次
        auto p = hash[key];
        remove(p);
        insert(p);
        return p->val;
    }
    
    void put(int key, int value) {
        //如果key已经存在
        if(hash.count(key)){
            auto p = hash[key];
            //更新val并且更新节点位置
            p->val = value;
            remove(p);
            insert(p);
        }else{
            //如果容量已满
            if(hash.size() == n){
                auto p = R->left;
                //从双链表中删除
                remove(p);
                //从哈希表中删除
                hash.erase(p->key);
                //从内存溢出的角度删除p点
                delete p;
            }
            auto p = new Node(key, value);
            hash[key] = p;
            insert(p);
        }
    }
};

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache* obj = new LRUCache(capacity);
 * int param_1 = obj->get(key);
 * obj->put(key,value);
 */
```





## 4、数组中的第K个最大的数

[题目链接](https://leetcode.cn/problems/kth-largest-element-in-an-array/)

快速选择算法 或者 堆排序（手写）

### 快选：

```c++
class Solution {
public:
    int quick_select(vector<int>& nums, int l, int r, int k)
    {
        if(l >= r) return nums[l];
        int x = nums[l + r >> 1], i = l - 1, j = r + 1;
        while(i < j)
        {
            do i++; while(nums[i] > x);
            do j--; while(nums[j] < x);
            if(i < j){
                swap(nums[i], nums[j]);
            }
        }

        if(j - l + 1 >= k) return quick_select(nums, l, j, k);
        else return quick_select(nums, j + 1, r, k - (j - l + 1));

    }

    int findKthLargest(vector<int>& nums, int k) {
        return quick_select(nums, 0, nums.size() - 1, k);
    }
};
```

### 堆排序：

```c++
class Solution {
public:
    
    //down操作-将较小的值down下去
    void down(vector<int>& nums, int u, int len)
    {

        int t = u;
        if(u*2<= len && nums[u*2] > nums[t]) t = u*2;
        if(u*2 + 1 <= len && nums[u*2 + 1] > nums[t]) t = u*2 + 1;
        if(t != u)
        {
            //交换数据
            swap(nums[t], nums[u]);
            down(nums, t, len);
        }
    }

    //使用堆排序
    int findKthLargest(vector<int>& nums, int k) {
        int len = nums.size();
        vector<int> tmp(len + 1);
        for(int i = 1; i <= len; i++)
        {
            tmp[i] = nums[i - 1];
        }
        //堆排 构建大根堆 时间复杂度O(n)
        for(int i = len / 2; i; i--)
        {
            down(tmp, i, len);
        }

        while(k-- - 1)
        {
            tmp[1] = tmp[len];
            len--;
            down(tmp, 1, len);
        }
        return tmp[1];

    }
};
```



## 5、K个一组翻转链表

[题目链接](https://leetcode.cn/problems/reverse-nodes-in-k-group/)

### 解题思路：

1、反转之前先判断未反转的链表元素是否有k个

2、对接下来k个元素进行反转操作

3、改变反转后的链表头节点和尾节点的指向

4、依次循环执行

### 代码实现：

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
    ListNode* reverseKGroup(ListNode* head, int k) {
        auto dummy = new ListNode(-1);
        dummy->next = head;
        for(auto p = dummy;;)
        {
            auto q = p;
            //先判断当前节点后面是否有足量的k个元素
            for(int i = 0; i < k && q; i ++) q = q->next;
            //如果元素数量不足，直接break
            if(!q) break;
            auto a = p->next, b = a->next;
            //反转链表
            for(int i = 0; i < k - 1; i ++)
            {
                auto c = b->next;
                b->next = a;
                a = b;
                b = c;
            }
            //改变节点指向
            auto c = p->next;
            p->next = a;
            c->next = b;
            //更新p节点
            p = c;

        }

        return dummy->next;
    }
};
```





# 11-20



# 21-30



# 31-40



# 41-50

