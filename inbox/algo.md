
https://www.hello-algo.com/chapter_array_and_linkedlist/array/

## Data Structure

### Two Pointers

```cpp

class Solution {

public:
  bool hasCycle(ListNode *head) {
    ListNode *fastPtr = head;

ListNode *slowPtr = head;

while (fastPtr != nullptr && fastPtr -> next != nullptr) {

fastPtr = fastPtr -> next -> next;

slowPtr = slowPtr -> next;

if (fastPtr == slowPtr) {

return true;

}

}

return false;

}

}

```


[142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)

```cpp

class Solution {

public:

ListNode *detectCycle(ListNode *head) {

ListNode *fastPtr = head;

ListNode *slowPtr = head;

bool isCycle = false;

while (fastPtr != nullptr && fastPtr -> next != nullptr) {

fastPtr = fastPtr -> next -> next;

slowPtr = slowPtr -> next;

if (fastPtr == slowPtr) {

isCycle = true;

break;

}

}

if (!isCycle) {

return nullptr;

}

slowPtr = head;

while (slowPtr != fastPtr) {

slowPtr = slowPtr -> next;

fastPtr = fastPtr -> next;

}

return slowPtr;

}

};

```

  


[160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/)

  


```cpp

class Solution {

public:

ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {

ListNode *ptrA = headA;

ListNode *ptrB = headB;

while (ptrA != ptrB) {

ptrA = (ptrA ? ptrA->next : headB);

ptrB = (ptrB ? ptrB->next : headA);

}

return ptrA; // or ptrB

}

};

```

  

  


[19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

  


```cpp

class Solution {

public:

ListNode* removeNthFromEnd(ListNode* head, int n) {

ListNode* fastPtr = head;

ListNode* slowPtr = head;

for (int i = 0; i < n; ++i) {

fastPtr = fastPtr -> next;

}

if (!fastPtr) {

return head -> next;

}

while(fastPtr -> next) {

fastPtr = fastPtr -> next;

slowPtr = slowPtr -> next;

}

slowPtr -> next = slowPtr -> next -> next;

return head;

}

};

```

  

  


## [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)

  


```cpp

class Solution {

public:

ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {

ListNode* dummy = new ListNode();

ListNode* cur = dummy;

while (list1 && list2) {

if (list1 -> val < list2 -> val) {

cur -> next = list1;

list1 = list1 -> next;

} else {

cur -> next = list2;

list2 = list2 -> next;

}

cur = cur -> next;

}

if (list1) {

cur -> next = list1;

} else {

cur -> next = list2;

}

return dummy -> next;

}

}

```

  

  


## [23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)

  


```cpp

class Solution {

public:

ListNode* mergeKLists(vector<ListNode*>& lists) {

auto cmp = [](ListNode* l1, ListNode* l2) { return l1 -> val > l2 -> val; };

priority_queue<ListNode*, vector<ListNode*>, decltype(cmp)> pq;

for (ListNode* list: lists) {

if (list) {

pq.push(list);

}

}

  


ListNode* dummy = new ListNode();

ListNode* cur = dummy;

// like BFS

while (!pq.empty()) {

// get the top element

ListNode* curNode = pq.top();

pq.pop();

// update the list

cur -> next = curNode;

cur = cur -> next;

// update

if (curNode -> next) {

pq.push(curNode -> next);

}

}

return dummy -> next;

}

};

```

  

  


## [86. Partition List](https://leetcode.com/problems/partition-list/)

  


```cpp

class Solution {

public:

ListNode* partition(ListNode* head, int x) {

ListNode* dummy1 = new ListNode();

ListNode* cur1 = dummy1;

  


ListNode* dummy2 = new ListNode();

ListNode* cur2 = dummy2;

while (head) {

if (head -> val < x) {

cur1 -> next = head;

cur1 = cur1 -> next;

} else {

cur2 -> next = head;

cur2 = cur2 -> next;

}

head = head -> next;

}

cur2 -> next = nullptr;

cur1 -> next = dummy2 -> next;

return dummy1 -> next;

}

};

```

  


### Reverse Linked List

  


[Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/description/)

  


[Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/description/)

  



### Graph Structure

  


## Dynamic Programming

  


## Reference

https://labuladong.github.io/algo/



## Knapsack Problem

### 0-1 BackPack

```cpp
// n: the number of goods
// v: the volumn of backpack

for (int i = 0; i < n; ++i){
    for (int j = v; j >= volume[i]; --j) {
        dp[j] = max(dp[j], dp[j - volume[i]] + value[i]);
    }
}
```

tree结构：https://blog.csdn.net/weixin_44279771/article/details/106602482





### 完全背包问题

```cpp
 for (int i = 0; i < n; ++i){
    for (int j = volume[i]; j <= v; ++j) {
        dp[j] = max(dp[j], dp[j - volume[i]] + value[i]);
    }
}
```



### 多重背包问题 I

https://www.acwing.com/problem/content/submission/code_detail/17269300/



## Rod Cutting

 https://www.geeksforgeeks.org/cutting-a-rod-dp-13/
