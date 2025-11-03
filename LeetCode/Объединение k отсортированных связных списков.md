# Объединение k отсортированных связных списков

Вам дан массив `lists` с `k` связными списками, каждый связный список отсортирован по возрастанию.

*Объедините все связные списки в один связный список и верните его*.

**Пример 1:**

**Ввод:** lists = [[1,4,5],[1,3,4],[2,6]]
**Вывод:** [1,1,2,3,4,4,5,6]
**Пояснение:** Связные списки:
[
  1->4->5,
  1->3->4,
  2->6
]
объединяем их в один связный список:
1->1->2->3->4->4->5->6**Пример 2:**

**Ввод:** lists = []
**Вывод:** []

# Решение

```c++
class Solution {
public:
    struct Compare {
        bool operator()(ListNode* a, ListNode* b) {
            return a->val > b->val;
        }
    };
    
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        priority_queue<ListNode*, vector<ListNode*>, Compare> minHeap;
        
        // Add all list heads to min heap
        for(ListNode* head : lists) {
            if(head != nullptr) {
                minHeap.push(head);
            }
        }
        
        ListNode* dummy = new ListNode(0);
        ListNode* current = dummy;
        
        while(!minHeap.empty()) {
            ListNode* smallest = minHeap.top();
            minHeap.pop();
            
            current->next = smallest;
            current = current->next;
            
            if(smallest->next != nullptr) {
                minHeap.push(smallest->next);
            }
        }
        
        ListNode* mergedList = dummy->next;
        delete dummy;
        return mergedList;
    }
};
```
