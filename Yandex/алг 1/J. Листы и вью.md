# J. Листы и вью


![image](./.assets/image-1759700129179.png)

![image](./.assets/image-1759700141024.png)

# Ответ

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <sstream>
#include <map>
#include <memory>
#include <algorithm>

// Структура FigonList логически корректна и остается без изменений.
struct FigonList {
    std::shared_ptr<std::vector<int>> data;  // Общие данные списка
    size_t start_offset;                     // Смещение начала подсписка
    size_t list_size;                        // Размер этого списка
    bool is_owner;                           // Является ли владельцем данных

    FigonList() : data(nullptr), start_offset(0), list_size(0), is_owner(false) {}

    // Конструктор для создания нового списка с начальными элементами
    explicit FigonList(const std::vector<int>& initial_elements) {
        data = std::make_shared<std::vector<int>>(initial_elements);
        start_offset = 0;
        list_size = initial_elements.size();
        is_owner = true;
    }

    // Получить элемент по пользовательскому индексу (начинается с 1)
    int get(int user_index) const {
        size_t internal_index = start_offset + (user_index - 1);
        return (*data)[internal_index];
    }

    // Установить значение элемента по пользовательскому индексу
    void set(int user_index, int value) {
        size_t internal_index = start_offset + (user_index - 1);
        (*data)[internal_index] = value;
    }

    // Добавить элемент в конец списка (только если владелец)
    void add(int value) {
        if (is_owner) {
            data->push_back(value);
            list_size++;
        }
    }

    // Создать подсписок из диапазона элементов
    FigonList subList(int from, int to) const {
        FigonList new_sublist;
        new_sublist.data = this->data;  // Разделяем данные с родительским списком
        new_sublist.start_offset = this->start_offset + (from - 1);
        new_sublist.list_size = (to - from) + 1;
        new_sublist.is_owner = false;  // Подсписок не владеет данными
        return new_sublist;
    }
};

// Глобальная карта для хранения всех именованных списков.
std::map<std::string, FigonList> lists;

/**
 * @brief Надежный парсер, использующий stringstream для обработки команд.
 * * Эта функция заменяет оригинальный хрупкий парсер. Она токенизирует входную
 * строку после замены всех разделителей пробелами, что делает ее нечувствительной
 * к вариациям форматирования.
 */
void parseAndExecute(std::string line) {
    // Заменяем все разделители пробелами для легкой токенизации.
    for (char &c : line) {
        if (c == '(' || c == ')' || c == '=' || c == ',' || c == '.' || c == ';') {
            c = ' ';
        }
    }

    std::stringstream ss(line);
    std::string token1;
    ss >> token1;

    if (token1 == "List") {
        // Объявление: например, "List a = new List(...)" или "List b = a subList(...)"
        std::string new_list_name, token3, command;
        ss >> new_list_name >> token3; // token3 - либо исходный список, либо "new"

        if (token3 == "new") { // Случай: new List(...)
            ss >> command; // Потребляем ключевое слово "List"
            std::vector<int> values;
            int val;
            while(ss >> val) {
                values.push_back(val);
            }
            lists[new_list_name] = FigonList(values);
        } else { // Случай: subList(...)
            std::string source_list_name = token3;
            ss >> command; // "subList"
            int from, to;
            ss >> from >> to;
            // .at() может вызвать сбой, если source_list_name не существует,
            // но это вряд ли будет проблемой по сравнению с ошибкой парсинга.
            lists[new_list_name] = lists.at(source_list_name).subList(from, to);
        }
    } else {
        // Вызов метода: например, "a get 1"
        std::string list_name = token1;
        std::string command;
        ss >> command;

        if (command == "get") {
            int idx;
            ss >> idx;
            std::cout << lists.at(list_name).get(idx) << "\n";
        } else if (command == "set") {
            int idx, val;
            ss >> idx >> val;
            lists.at(list_name).set(idx, val);
        } else if (command == "add") {
            int val;
            ss >> val;
            lists.at(list_name).add(val);
        }
    }
}

int main() {
    // Быстрый ввод/вывод для производительности.
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    int n;
    std::cin >> n;
    std::string line;
    std::getline(std::cin, line); // Потребляем символ новой строки после чтения n.

    for (int i = 0; i < n; ++i) {
        std::getline(std::cin, line);
        if (!line.empty()) {
            parseAndExecute(line);
        }
    }

    return 0;
}
```