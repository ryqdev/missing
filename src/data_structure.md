---
layout: lecture
title: "Data Structure"
date: 2022-08-30
ready: true
---

# Data Structure

#### 线性数据
**静态数组**
```cpp
const int SIZE;
int array[SIZE];
​
memset(array, 0x3f, sizeof array);
```

这是最经典的静态数组，访问元素的时间复杂度是O(1)

缺点是数组长度固定，不可变化。

另外在C中可以使用memset来对数组或者变量进行初始化

**动态数组**

在C++的STL中，vector用来表示动态数组，vector是一个模板类：

```cpp
const int SIZE;
const int VALUE;
vector<int> array(SIZE, VALUE);
```

动态数组的坏处也很明显：

长度的变化是有代价的，因为数据的随机访问特性，所有数据必须是在一块连续的内存地址空间里面，所以当数组的长度超过一定数值之后，需要把整段数组内存迁移到新的内存区域

**栈**

C++中用`stack<T>`来得到栈。

栈是FIFO的线性结构，在算法中一个比较重要的用法是`单调栈`, 常用的结构如下：

```cpp
for(){
  while(){
    //...
  }
}
```

单调栈例题：

* [https://leetcode.com/problems/trapping-rain-water/](https://leetcode.com/problems/trapping-rain-water/)
* [https://leetcode.com/problems/largest-rectangle-in-histogram/](https://leetcode.com/problems/largest-rectangle-in-histogram/)

**队列**

C++中用`queue<T>`来得到队列

**链表**

**单向链表**

```cpp
struct ListNode {
    int val;
    ListNode *next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode *next) : val(x), next(next) {}
};
```

反转单向链表 三部曲:

* [https://leetcode.com/problems/reverse-linked-list/](https://leetcode.com/problems/reverse-linked-list/)
* [https://leetcode.com/problems/reverse-linked-list-ii/](https://leetcode.com/problems/reverse-linked-list-ii/)
* [https://leetcode.com/problems/reverse-nodes-in-k-group/](https://leetcode.com/problems/reverse-nodes-in-k-group/)

**优先队列（堆）Priority queue**

```cpp
auto cmp = [](ListNode* l1, ListNode* l2){
            return l1 -> val > l2 -> val;
        };
priority_queue<ListNode*, vector<ListNode*>, decltype(cmp)>pq(cmp);
```

#### 图结构

**树**

C++版本：

```cpp
class treeNode{
    int value;
    treeNode* left;
    treeNOde* right;
    treeNode():value(-1), left(nullptr), right(nullptr){}
    treeNode(int _value): value(_value), left(nullptr), right(nullptr){}
    treeNode(int _value, treeNode* _left, treeNode* _right): value(_value), left(_left), right(_right){}
};
```

**字典树 Trie**

C++版本

```cpp
struct TrieNode {
    TrieNode(): count(0), isEnd(false), children(vector<TrieNode*>(26, nullptr)){};
    ~TrieNode(){
        for(TrieNode* child : children){
            if(child)
                delete(child);
        }
    }
    int count;
    bool isEnd;
    vector<TrieNode*> children;
};
​
class Trie {
public:
    TrieNode* dummy;
    Trie() {
        dummy = new TrieNode();
    }
​
    ~Trie(){
        delete dummy;
    }
    void insert(string word) {
        TrieNode* cur = dummy;
        for(char &c : word){
            if(cur -> children[c - 'a'] == nullptr){
                cur -> children[c - 'a'] = new TrieNode();
            }
            cur = cur -> children[c - 'a'];
            cur -> count ++;
        }
        cur -> isEnd = true;
    }
​
    bool search(string word) {
        TrieNode* p = find(word);
        return p && p -> isEnd == true;
    }
​
    bool startsWith(string prefix) {
        TrieNode* p = find(prefix);
        return p != dummy;
    }
    TrieNode* find(string &pre){
        TrieNode* cur = dummy;
        for(char &c : pre){
            cur = cur -> children[c - 'a'];
            if(cur == nullptr){
                break;
            }
        }
        return cur;
    }
};
```

**Segment tree**

```cpp
#define ll long long
​
struct segtree {
    int size;
    vector<ll> sums;
    void init(int n) {
        size = 1;
        while (size < n) {
            size *= 2;
        }
        sums.assign(2 * size, 0LL);
    }
    
    void set(int i, int v, int x, int lx, int rx) {
        if (rx - lx == 1) {
            sums[x] = v;
            return;
        }
        int m = (lx + rx) / 2;
        if (i < m) {
            set(i, v, 2 * x + 1, lx, m);
        } else {
            set(i, v, 2 * x + 2, m, rx);
        }
        sums[x] = sums[2 * x + 1] + sums[2 * x + 2];
    }
​
    void set(int i, int v) {
        set(i, v, 0, 0, size);
    }
​
    ll sum(int l, int r, int x, int lx, int rx) {
        if(lx >= r or rx <= l) {
            return 0;
        }
        if(lx >= l and rx <= r) {
            return sums[x];
        }
        int m = (lx + rx) / 2;
        ll s1 = sum(l, r, 2 * x + 1, lx, m);
        ll s2 = sum(l, r, 2 * x + 2, m, rx);
        return s1 + s2;
    }
​
    ll sum(int l, int r){
        return sum(l, r, 0, 0, size);
    }
};
```

**后缀数组 suffix array**

```cpp
#define ll long long
 
vector<int> suffixArray(){
    string s;
    cin >> s;
    s += '$';
    int n = (int)s.size();
    vector<int> p(n), c(n);
    {
        vector<pair<char, int>> a(n);
        for (int i = 0; i < n; ++i) {
            a[i] = {s[i], i};
        }
        sort(a.begin(), a.end());
        for (int i = 0; i < n; ++i) {
            p[i] = a[i].second;
        }
        c[p[0]] = 0;
        for (int i = 1; i < n; ++i) {
            if (a[i].first == a[i-1].first) {
                c[p[i]] = c[p[i - 1]];
            } else {
                c[p[i]] = c[p[i - 1]] + 1;
            }
        }
    }
    int k = 0;
    while ((1 << k) < n) {
        vector<pair<pair<int, int>, int>>a(n);
        // update a according to c
        for (int i = 0; i < n; ++i) {
            a[i].first = {c[i], c[(i + (1 << k)) % n]};
            a[i].second = i;
        }
        sort(a.begin(), a.end());
        for (int i = 0; i < n; ++i) {
            p[i] = a[i].second;
        }
        c[p[0]] = 0;
        for (int i = 1; i < n; ++i) {
            if (a[i].first == a[i-1].first) {
                c[p[i]] = c[p[i - 1]];
            } else {
                c[p[i]] = c[p[i - 1]] + 1;
            }
        }
        k++;
    }
    return p;
}
```

**Dijkstra 算法**

```cpp
vector<int> dis(n, INT_MAX);
priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
pq.emplace(0, startPos);
dis[startPos] = 0;
while (!pq.empty()) {
    auto cur = pq.top();
    pq.pop();
    int curPos = cur.second;
    int curDis = cur.first;
    for (int nextPos: adj[curPos]) {
        if (dis[nextPos] > curDis + edge[curPos][nextPos]) {
            dis[nextPos] = curDis + edge[curPos][nextPos];
            pq.emplace(dis[nextPos], nextPos);
        }
    }
}
```

**Union and find**

path compression，smart union

```cpp
int find(int x) {
	while (x != link[x]){
        x = link[x];
    }
    return x;
}

void union(int a, int b) {
    a = find(a);
    b = find(b);
    link[a] = b;
}

void union_find(){
    vector<int> link(n);
    for (int i = 0; i < n; ++i) {
        link[i] = i;
    }
}
```
