# H. Разрезанная строка


![image](./.assets/image-1759699909423.png)

# Ответ

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <map>
#include <queue>

using namespace std;

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(0);
    
    // Чтение входных данных
    int n, m;           // n - длина строки s, m - количество кусков
    cin >> n >> m;
    string s;           // Исходная строка, которую нужно получить
    cin >> s;
    int L = n / m;      // Длина каждого куска
    
    // Создаем словарь, где ключ - строка куска, значение - очередь позиций
    // Это нужно для отслеживания, какие куски и на каких позициях должны быть
    map<string, queue<int>> segments_map;
    
    // Разбиваем исходную строку s на m кусков длиной L
    // и запоминаем, какой кусок на какой позиции должен стоять
    for (int i = 0; i < m; i++) {
        string segment = s.substr(i * L, L);  // Вырезаем кусок длины L
        segments_map[segment].push(i);        // Запоминаем позицию этого куска
    }
    
    // Вектор для хранения результата - порядок склеивания кусков
    // res[i] = номер куска, который должен стоять на i-й позиции
    vector<int> res(m);
    
    // Читаем перемешанные куски и определяем их правильные позиции
    for (int i = 0; i < m; i++) {
        string t;  // Очередной кусок из входных данных
        cin >> t;
        
        // Ищем этот кусок в нашем словаре
        auto it = segments_map.find(t);
        if (it != segments_map.end()) {
            queue<int>& q = it->second;  // Очередь позиций для этого куска
            int pos = q.front();         // Берем первую доступную позицию
            q.pop();                     // Удаляем ее из очереди
            res[pos] = i + 1;            // Записываем, что кусок (i+1) должен быть на позиции pos
            if (q.empty()) {
                segments_map.erase(it);  // Если позиций больше нет, удаляем запись
            }
        }
    }
    
    // Выводим результат - порядок склеивания кусков
    for (int i = 0; i < m; i++) {
        cout << res[i] << " ";
    }
    cout << endl;
    
    return 0;
}
```