# Идиома erase-remove

Это стандартный и эффективный способ удаления всех вхождений определённого элемента из вектора. Прямое удаление в цикле неэффективно, так как каждый `erase` сдвигает все последующие элементы.

* `std::remove`: Перемещает все элементы, которые **не** равны заданному значению, в начало вектора. Возвращает итератор на "новую" позицию конца. Он не изменяет размер вектора.
* `vec.erase`: Удаляет элементы в диапазоне, изменяя размер вектора.

```c++
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> vec = {10, 20, 30, 20, 40, 50, 20};

    std::cout << "Исходный вектор: ";
    for (int el : vec) std::cout << el << " ";
    std::cout << std::endl;

    int value_to_remove;
    std::cout << "Введите значение для удаления: ";
    std::cin >> value_to_remove;

    // 1. Шаг 'remove': перемещаем все '20' в конец
    auto new_end = std::remove(vec.begin(), vec.end(), value_to_remove);
    // Вектор теперь может выглядеть так: {10, 30, 40, 50, ?, ?, ?}, new_end указывает на первый '?'

    // 2. Шаг 'erase': удаляем "мусор" с конца
    vec.erase(new_end, vec.end());

    std::cout << "Вектор после удаления: ";
    for (int el : vec) std::cout << el << " ";
    std::cout << std::endl;

    return 0;
}
```

