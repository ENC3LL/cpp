# A. Делёж грибов



Вася и Маша ходили в лес и собрали nn грибов, для каждого гриба известен его вес aiai​. Они выложили их в один ряд и решили делить следующим образом: первый гриб берёт Вася, второй — Маша, третий — Вася, четвёртый — Маша и т.д.

Вася очень любит грибы и не очень любит Машу. Количество радости Васи равно разности суммарного веса грибов, доставшихся Васе, и суммарного веса грибов, доставшихся Маше. 

Маша отвлеклась на минутку, и за это время Вася может выбрать любые два гриба и поменять их местами (а может и не менять). Определите максимальную радость Васи, которую можно достичь не более чем одним обменом.

## Формат ввода
В первой строке содержится одно натуральное число n — количество грибов
Во второй строке содержится n чисел ai​ — вес грибов

### Пример 1
Ввод      Вывод
1 2                  2
1
### Пример 2
Ввод       Вывод
3                      2
2 2 2
### Пример 3
Ввод                             Вывод
11                                         10
4 10 7 5 4 5 3 8 3 2 5


# Ответ
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <sstream>
#include <algorithm>
#include <numeric>

using namespace std;

int main() {
    int n;
    cin >> n;
    cin.ignore(); // игнорируем остаток строки после n

    vector<int> v1;
    v1.reserve(n); // опционально: резервируем память

    string line;
    getline(cin, line);
    stringstream ss(line);

    int vint;
    while (v1.size() < static_cast<size_t>(n) && ss >> vint) {
        v1.push_back(vint);
    }

    vector<int> vas;
    vector<int> mash;

    // Теперь вектор содержит не более n элементов

    if (!v1.empty()) {
    }
    else {
        cout << "Вектор пуст" << endl;
        return 0;
    }

    for (size_t i = 0; i < v1.size(); ++i) {
        if ((i + 1) % 2 == 1) { // нечётная позиция (1-based)
            vas.push_back(v1[i]);
        }
        else {                // чётная позиция (1-based)
            mash.push_back(v1[i]);
        }
    }

    auto min_odd_it = min_element(vas.begin(), vas.end());
    auto max_even_it = max_element(mash.begin(), mash.end());

    if (*min_odd_it < *max_even_it){ swap(*min_odd_it, *max_even_it); }

    int dif;

    dif = accumulate(vas.begin(), vas.end(),0) - accumulate(mash.begin(), mash.end(),0);

    cout << dif << endl;

    return 0;
}
```












