# Удаление n-ого узла с конца списка
Вам дан указатель `head` связного списка, удалите `nый` узел с конца списка и верните указатель на голову списка.

**Пример 1:**

![image](./.assets/image-1761601209492.png)

**Ввод:** head = [1,2,3,4,5], n = 2
**Вывод:** [1,2,3,5]**Пример 2:**

**Ввод:** head = [1], n = 1
**Вывод:** []**Пример 3:**

**Ввод:** head = [1,2], n = 1
**Вывод:** [1]

# Решение
```c++
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* res = new ListNode(0, head);
        ListNode* dummy = res;

        for (int i = 0; i < n; i++) {
            head = head->next;
        }

        while (head != nullptr) {
            head = head->next;
            dummy = dummy->next;
        }

        dummy->next = dummy->next->next;

        ListNode* result = res->next;
        delete res;
        return result;
    }
};
```




