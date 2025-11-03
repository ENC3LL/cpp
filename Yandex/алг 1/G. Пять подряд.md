# G. Пять подряд


![image](./.assets/image-1759699861975.png)
# Ответ

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    int n, m;
    cin >> n >> m;
    vector<string> field(n);
    for (int i = 0; i < n; i++) {
        cin >> field[i];
    }

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (field[i][j] == '.') {
                continue;
            }
            char current = field[i][j];
            
            // Проверка горизонтали вправо
            if (j + 4 < m) {
                bool found = true;
                for (int k = 1; k < 5; k++) {
                    if (field[i][j + k] != current) {
                        found = false;
                        break;
                    }
                }
                if (found) {
                    cout << "Yes" << endl;
                    return 0;
                }
            }
            
            // Проверка вертикали вниз
            if (i + 4 < n) {
                bool found = true;
                for (int k = 1; k < 5; k++) {
                    if (field[i + k][j] != current) {
                        found = false;
                        break;
                    }
                }
                if (found) {
                    cout << "Yes" << endl;
                    return 0;
                }
            }
            
            // Проверка диагонали вниз-вправо
            if (i + 4 < n && j + 4 < m) {
                bool found = true;
                for (int k = 1; k < 5; k++) {
                    if (field[i + k][j + k] != current) {
                        found = false;
                        break;
                    }
                }
                if (found) {
                    cout << "Yes" << endl;
                    return 0;
                }
            }
            
            // Проверка диагонали вниз-влево
            if (i + 4 < n && j - 4 >= 0) {
                bool found = true;
                for (int k = 1; k < 5; k++) {
                    if (field[i + k][j - k] != current) {
                        found = false;
                        break;
                    }
                }
                if (found) {
                    cout << "Yes" << endl;
                    return 0;
                }
            }
        }
    }
    
    cout << "No" << endl;
    return 0;
}
```