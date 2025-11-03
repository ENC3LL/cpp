# D. Отборочный контест
![image](./.assets/image-1759343963327.png)

# Ответ

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <sstream>
#include <algorithm>

using namespace std;

int main() {
    int n, k;
    cin >> n >> k;
    cin.ignore();

    vector<int> v1;
    v1.reserve(n);
    vector<int> v2;

    string line;
    getline(cin, line);
    stringstream ss(line);

    int num;
    while (v1.size() < static_cast<size_t>(n) && ss >> num) {
        v1.push_back(num);
    }

    if (v1.empty()) {
        cout << "Вектор пуст" << endl;
        return 0;
    }

    // Сортируем вектор
    sort(v1.begin(), v1.end());

    // Удаляем дубликаты и сохраняем их в v2
    vector<int> unique_v1;
    for (size_t i = 0; i < v1.size(); ++i) {
        if (i == 0 || v1[i] != v1[i - 1]) {
            unique_v1.push_back(v1[i]);
        }
        else {
            v2.push_back(v1[i]); // Дубликаты перемещаются в v2
        }
    }
    v1 = move(unique_v1);

    // Если в v1 меньше элементов чем k, добавляем из v2
    while (v1.size() < static_cast<size_t>(k) && !v2.empty()) {
        v1.push_back(v2[0]);
        v2.erase(v2.begin());
    }

    // Выводим ровно k элементов (или меньше, если не хватает)
    for (size_t i = 0; i < static_cast<size_t>(k) && i < v1.size(); ++i) {
        cout << v1[i];
        if (i < static_cast<size_t>(k) - 1 && i < v1.size() - 1) {
            cout << " ";
        }
    }
    cout << endl;

    return 0;
}
```