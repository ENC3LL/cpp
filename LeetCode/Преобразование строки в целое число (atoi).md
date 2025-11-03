# Преобразование строки в целое число (atoi)

Реализуйте функцию, которая преобразует строку в 32-битное целое число со знаком.`myAtoi(string s)`

Алгоритм выполнения этого задачи следующий:`myAtoi(string s)`

1. **Пробелы**: Игнорируйте все начальные пробелы ().`" "`
2. **Знаковость**: Определите знак, проверив, является ли следующий символ или , предполагая позитивность, если ни один из них не присутствует.`'-'``'+'`
3. **Преобразование**: Чтение целого числа, пропуская ведущие нули до тех пор, пока не будет найден символ, не состоящий из цифр, или не будет достигнут конец строки. Если цифры не были прочитаны, то результат равен 0.
4. **Округление**: Если целое число выходит за пределы 32-разрядного целого диапазона со знаком , то округлите целое число, чтобы остаться в диапазоне. В частности, целые числа меньше должны округляться до , а целые числа больше должны округляться до .`[-231, 231 - 1]``-231``-231``231 - 1``231 - 1`

Возвращает целое число в качестве конечного результата.

 

**Пример 1:**

**Входные данные:** s = "42"

**Выход:** 42

**Объяснение:**

The underlined characters are what is read in and the caret is the current reader position.
Step 1: "42" (no characters read because there is no leading whitespace)
         ^
Step 2: "42" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "__42__" ("42" is read in)
           ^
**Пример 2:**

**Входные данные:** s = "-042"

**Выход:** -42

**Объяснение:**

Step 1: "__   __-042" (leading whitespace is read and ignored)
            ^
Step 2: "   __-__042" ('-' is read, so the result should be negative)
             ^
Step 3: "   -__042__" ("042" is read in, leading zeros ignored in the result)
               ^
**Пример 3:**

**Входные данные:** s = "1337c0d3"

**Выход:** 1337

**Объяснение:**

Step 1: "1337c0d3" (no characters read because there is no leading whitespace)
         ^
Step 2: "1337c0d3" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "__1337__c0d3" ("1337" is read in; reading stops because the next character is a non-digit)
             ^
**Пример 4:**

**Входные данные:** s = "0-1"

**Выход:** 0

**Объяснение:**

Step 1: "0-1" (no characters read because there is no leading whitespace)
         ^
Step 2: "0-1" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "__0__-1" ("0" is read in; reading stops because the next character is a non-digit)
          ^
**Пример 5:**

**Входные данные:** s = "слова и 987"

**Выход:** 0

**Объяснение:**

Чтение останавливается на первом нецифровом символе 'w'.

# Решение

```c++
class Solution {
public:
    int myAtoi(string s) {
        if (s.empty()) {
            return 0;
        }

        // Use standard library constants
        const long long MAX_INT = INT_MAX;
        const long long MIN_INT = INT_MIN;

        int i = 0;
        int n = s.length();

        // Step 1: Skip leading whitespace
        while (i < n && s[i] == ' ') {
            i++;
        }

        // Check if we've reached the end
        if (i == n) {
            return 0;
        }

        // Step 2: Check for sign
        int sign = 1;
        if (s[i] == '+') {
            i++;
        }
        else if (s[i] == '-') {
            sign = -1;
            i++;
        }

        // Step 3: Read digits and convert
        long long res = 0;
        while (i < n && isdigit(s[i])) {
            int digit = s[i] - '0';
            res = res * 10 + digit;

            if (sign * res <= INT_MIN) {
                return INT_MIN;
            }
            if (sign * res >= INT_MAX) {
                return INT_MAX;
            }

            i++;
        }

        // Step 4: Apply sign and return
        return static_cast<int>(res * sign);
    }
};
```

