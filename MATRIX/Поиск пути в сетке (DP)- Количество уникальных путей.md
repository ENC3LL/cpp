# Поиск пути в сетке (DP): Количество уникальных путей

Это классическая задача на динамическое программирование. Дана сетка (матрица), нужно найти количество способов добраться из левого верхнего угла в правый нижний, двигаясь только вправо или вниз.

**Логика DP:** Количество путей в ячейку `dp[i][j]` равно сумме путей в ячейку сверху `dp[i-1][j]` и ячейку слева `dp[i][j-1]`.

```c++
#include <iostream>
#include <vector>
#include <iomanip>

void printMatrix(const std::vector<std::vector<int>>& matrix) {
    if (matrix.empty()) return;
    for (const auto& row : matrix) {
        for (int element : row) std::cout << std::setw(4) << element << " ";
        std::cout << std::endl;
    }
}

int main() {
    int rows, cols;
    std::cout << "Введите размеры сетки (строки столбцы): ";
    std::cin >> rows >> cols;

    // dp[i][j] будет хранить количество путей в ячейку (i, j)
    std::vector<std::vector<int>> dp(rows, std::vector<int>(cols));

    // Инициализация: в любую ячейку первого столбца есть только 1 путь (вниз)
    for (int i = 0; i < rows; ++i) {
        dp[i][0] = 1;
    }

    // Инициализация: в любую ячейку первой строки есть только 1 путь (вправо)
    for (int j = 0; j < cols; ++j) {
        dp[0][j] = 1;
    }

    // Заполняем остальную часть dp-таблицы
    for (int i = 1; i < rows; ++i) {
        for (int j = 1; j < cols; ++j) {
            // Формула перехода
            dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
        }
    }

    std::cout << "\nDP-таблица (количество путей до каждой ячейки):" << std::endl;
    printMatrix(dp);

    std::cout << "\nВсего уникальных путей из (0,0) в (" << rows - 1 << "," << cols - 1 << "): "
              << dp[rows - 1][cols - 1] << std::endl;

    return 0;
}
```

