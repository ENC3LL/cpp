# Префиксные суммы (partial_sum)

Префиксные суммы — мощная техника в олимпиадном программировании. Создаётся новый массив (или изменяется текущий), где `pref[i]` равно сумме всех элементов исходного массива от 0 до `i`. Это позволяет находить сумму на любом отрезке `[L, R]` за константное время O(1) по формуле `pref[R] - pref[L-1]`.

```c++
#include <iostream>
#include <vector>
#include <numeric> // Для partial_sum

using namespace std;

int main() {
    vector<int> vec;
    int n;
    cout << "Введите количество элементов в векторе: ";
    cin >> n;
    cout << "Введите " << n << " элементов: ";
    for(int i = 0; i < n; ++i) {
        int val;
        cin >> val;
        vec.push_back(val);
    }
    
    // Создаем вектор для хранения префиксных сумм
    vector<int> prefix_sums(vec.size());
    partial_sum(vec.begin(), vec.end(), prefix_sums.begin());

    cout << "\nИсходный вектор:     ";
    for (int el : vec) cout << el << "\t";
    cout << endl;

    cout << "Вектор префиксных сумм: ";
    for (int el : prefix_sums) cout << el << "\t";
    cout << endl << endl;

    // Теперь мы можем быстро считать сумму на любом отрезке
    int left, right;
    cout << "Введите левую и правую границу (индексы) для подсчета суммы: ";
    cin >> left >> right;

    if (left >= 0 && right < vec.size() && left <= right) {
        int sum = prefix_sums[right] - (left > 0 ? prefix_sums[left - 1] : 0);
        cout << "Сумма элементов на отрезке [" << left << ", " << right << "] = " << sum << endl;
    } else {
        cout << "Некорректные индексы!" << endl;
    }

    return 0;
}
```