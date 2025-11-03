# E. Табло с инкрементом

![image](./.assets/image-1759401625951.png)

# Ответ

```cpp
#include <iostream>
using namespace std;

int main() {
    long long n, k;
    cin >> n >> k;

    // Обработка чисел, оканчивающихся на 0
    if (n % 10 == 0) {
        cout << n << endl;
        return 0;
    }

    // Обработка чисел, оканчивающихся на 5
    if (n % 10 == 5) {
        if (k == 0) {
            cout << n << endl;
        } else {
            cout << n + 5 << endl;
        }
        return 0;
    }

    // Для остальных чисел выполняем итерации, пока k > 0
    while (k > 0) {
        int last_digit = n % 10;
        
        // Если последняя цифра стала 0, выходим из цикла
        if (last_digit == 0) {
            break;
        }
        
        // Если последняя цифра вошла в цикл [2,4,8,6], останавливаемся
        if (last_digit == 2 || last_digit == 4 || last_digit == 8 || last_digit == 6) {
            break;
        }
        
        n += last_digit;
        k--;
    }

    // Если остались итерации и последняя цифра в цикле [2,4,8,6]
    if (k > 0) {
        int last_digit = n % 10;
        
        // Определяем начальную позицию в цикле
        int cycle_start = last_digit;
        int cycle_sum = 0;
        int cycle_length = 4;
        
        // Вычисляем сумму приростов за полный цикл
        if (cycle_start == 2) {
            cycle_sum = 2 + 4 + 8 + 6;
        } else if (cycle_start == 4) {
            cycle_sum = 4 + 8 + 6 + 2;
        } else if (cycle_start == 8) {
            cycle_sum = 8 + 6 + 2 + 4;
        } else if (cycle_start == 6) {
            cycle_sum = 6 + 2 + 4 + 8;
        }
        
        // Добавляем полные циклы
        long long full_cycles = k / cycle_length;
        n += full_cycles * cycle_sum;
        k %= cycle_length;
        
        // Выполняем оставшиеся итерации
        while (k > 0) {
            n += n % 10;
            k--;
        }
    }

    cout << n << endl;
    return 0;
}
```