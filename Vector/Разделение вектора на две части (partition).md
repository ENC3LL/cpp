# Разделение вектора на две части (partition)

Алгоритм `partition` переупорядочивает элементы так, что все элементы, удовлетворяющие некоторому условию (предикату), оказываются в начале вектора, а остальные — в конце. Это очень эффективно и работает за линейное время O(N).

```c++
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {
    vector<int> vec = {1, 9, 2, 8, 3, 7, 4, 6, 5};
    cout << "Исходный вектор: ";
    for (int el : vec) cout << el << " ";
    cout << endl;

    int pivot;
    cout << "Введите число-разделитель (например, 5): ";
    cin >> pivot;

    // Переместим все числа, которые < pivot, в начало
    auto partition_point = partition(vec.begin(), vec.end(), [pivot](int num) {
        return num < pivot; // Предикат: возвращает true для элементов первой группы
    });

    cout << "После partition (все, что меньше " << pivot << ", слева):" << endl;
    for (int el : vec) cout << el << " ";
    cout << endl;

    // partition_point - это итератор на первый элемент второй группы
    cout << "Элементы первой группы: ";
    for (auto it = vec.begin(); it != partition_point; ++it) {
        cout << *it << " ";
    }
    cout << endl;

    cout << "Элементы второй группы: ";
    for (auto it = partition_point; it != vec.end(); ++it) {
        cout << *it << " ";
    }
    cout << endl;

    return 0;
}
```