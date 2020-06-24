## 1. 问题
给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

示例：
```
给定一个链表: 1->2->3->4->5, 和 n = 2.
当删除了倒数第二个节点后，链表变为 1->2->3->5.
```
说明：
给定的 n 保证是有效的。
## 2. 分析
需要了解**链表的遍历和删除其末尾的第 n 个元素**。
### 2.1. 两次遍历算法
思路：删除从列表开头数起的第 (L - n + 1)个结点，其中 L 是列表的长度。只要我们找到列表的长度 L，这个问题就很容易解决。

首先我们将添加一个哑结点作为辅助，该结点位于列表头部。哑结点用来简化某些极端情况，例如列表中只含有一个结点，或需要删除列表的头部。在**第一次遍历中，我们找出列表的长度 L**。然后设置一个指向哑结点的指针，并移动它遍历列表，直至它到达第 (L−n) 个结点那里。我们把第 (L−n) 个结点的 next 指针重新链接至第 (L−n+2) 个结点，完成这个算法。

如图1删除列表中的第L-n+1个元素

![t1](../_image_/a476f4e932fa4499e22902dcb18edba41feaf9cfe4f17869a90874fbb1fd17f5-file_1555694537876.png)

### 2.2. 一次遍历算法
设想假设设定了双指针 first 和 second 的话，当 first 指向末尾的 NULL，first 与 second 之间相隔的元素个数为 n 时，那么删除掉 second 的下一个指针就完成了要求。
* 设置虚拟节点 dummyHead 指向 head
* 设定双指针 first 和 second，初始都指向虚拟节点 dummyHead
* 移动 first，直到 first 与  second 之间相隔的元素个数为 n
* 同时移动 first 与 second，直到 first 指向的为 NULL
* 将 second 的下一个节点指向下下个节点

![t2](../_image_/del_N_node.png)

## 3. 题解
### 3.1. 两次遍历
```C++
/**
 * Definition for singly-linked list.
 */
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};
class Solution{
public: 
    ListNode* removeNthFormEnd(ListNode* head, int n){
        ListNode* dummyHead = new ListNode(0);
        dummyHead->next = head;
        int length = 0;
        ListNode* first = head;
        while(first != NULL){
            length++;
            first = first->next;
        }
        length -= n;
        first = dummyHead;
        while(length > 0){
            length--;
            first = first->next;
        }
        first->next = first->next->next;
        return dummyHead->next;
    }
}
```
### 3.2. 一次遍历
```C++
/**
 * Definition for singly-linked list.
 */
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution{
public: 
    ListNode* removeNthFormEnd(ListNode* head, int n){
        //设置虚拟节点 dummyHead 指向 head
        ListNode* dummyHead = new ListNode(0);
        dummyHead->next = head;
        //设定双指针 first 和 second，初始都指向虚拟节点 dummyHead
        ListNode* first = dummyHead;
        ListNode* second = dummyHead;
        //移动 first，直到 first 与  second 之间相隔的元素个数为 n
        for(int i = 0; i < n+1; i++){
            first = first->next;
        }
        //同时移动 first 与 second，直到 first 指向的为 NULL
        while(first){
            first = first->next;
            second = second->next;
        }
        //将 second 的下一个节点指向下下个节点,删除指定节点。
        ListNode* delNode = second->next;
        second->next = delNode->next;
        delete delNode;
        //指向头节点
        ListNode* retNode = dummyHead->next;
        delete dummyHead;

        return retNode;
    }
}
```