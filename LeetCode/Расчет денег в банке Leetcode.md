# Расчет денег в банке Leetcode

Херси хочет накопить денег на свою первую машину. Он каждый **день** кладет деньги в банк Leetcode.

Он начинает с того, что кладет деньги в понедельник, в первый день. Каждый день со вторника по воскресенье он будет вкладывать больше, чем накануне. В каждый последующий понедельник он будет вкладывать больше, чем в **предыдущий понедельник**.`$1``$1``$1`

Учитывая , верните *общую сумму денег, которую он будет иметь в банке Leetcode в конце **дня.*`n``nth`

 

**Пример 1:**

**Input:** n = 4
**Output:** 10
**Explanation:** After the 4th day, the total is 1 + 2 + 3 + 4 = 10.
**Пример 2:**

**Input:** n = 10
**Output:** 37
**Explanation:** After the 10th day, the total is (1 + 2 + 3 + 4 + 5 + 6 + 7) + (2 + 3 + 4) = 37. Notice that on the 2nd Monday, Hercy only puts in $2.
**Пример 3:**

**Input:** n = 20
**Output:** 96
**Explanation:** After the 20th day, the total is (1 + 2 + 3 + 4 + 5 + 6 + 7) + (2 + 3 + 4 + 5 + 6 + 7 + 8) + (3 + 4 + 5 + 6 + 7 + 8) = 96.

# Решение

```c++
class Solution {
public:
    int triSum(int n) {
        return (n * (n + 1)) >> 1;
    }

    int totalMoney(int days) {
        int nWeeks = days / 7;
        int rDays = days % 7;

        return triSum(days) - 42 * triSum(nWeeks - 1) - 6 * nWeeks * rDays;
    }
};
```
