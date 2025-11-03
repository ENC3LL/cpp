# K наиболее часто встречающихся элементов

Даны массив целочисленных значений `nums` и целое число `k`, верните `k` *наиболее часто встречающихся элементов*. Вы можете вернуть ответ в **любом порядке**.

**Пример 1:**

**Ввод:** nums = [1,1,1,2,2,3], k = 2
**Вывод:** [1,2]
**Пояснение:** Посчитаем, сколько раз встречается каждое число в массиве:
1 -> 3
2 -> 2
3 -> 1
Так как K равен 2, берем 2 наиболее часто встречающихся числа, это [1,2].

**Пример 2:**

**Ввод:** nums = [1], k = 1
**Вывод:** [1]

# Код

```c++
vector<int> topKFrequent(vector<int>& nums, int k) {
    // 1. Подсчет частот с помощью unordered_map
    unordered_map<int, int> freq;
    for (int num : nums) {
        freq[num]++;
    }
    
    // 2. Создаем вектор из пар (частота, число) и сортируем по убыванию частоты
    vector<pair<int, int>> pairs;
    for (auto& [num, count] : freq) {
        pairs.push_back({count, num});
    }
    
    // Сортируем по убыванию частоты
    sort(pairs.begin(), pairs.end(), [](const pair<int, int>& a, const pair<int, int>& b) {
        return a.first > b.first;
    });
    
    // 3. Берем k самых частых элементов
    vector<int> result;
    for (int i = 0; i < k && i < pairs.size(); i++) {
        result.push_back(pairs[i].second);
    }
    
    return result;
}
```