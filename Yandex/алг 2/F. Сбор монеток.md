# F. Сбор монеток


![image](./.assets/image-1760362592213.png)

```c++
#include <iostream>
#include <vector>
#include <algorithm>
#include <climits>

using namespace std;

int main() {
    int n;
    cin >> n;
    vector<vector<char>> matrix(n, vector<char>(3));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < 3; j++) {
            cin >> matrix[i][j];
        }
    }

    vector<vector<int>> dp(n, vector<int>(3, INT_MIN));
    
    for (int j = 0; j < 3; j++) {
        if (matrix[0][j] != 'W') {
            dp[0][j] = (matrix[0][j] == 'C') ? 1 : 0;
        }
    }

    for (int i = 1; i < n; i++) {
        for (int j = 0; j < 3; j++) {
            if (matrix[i][j] == 'W') continue;
            int coin = (matrix[i][j] == 'C') ? 1 : 0;
            int max_prev = INT_MIN;
            for (int k = -1; k <= 1; k++) {
                int prev_j = j + k;
                if (prev_j >= 0 && prev_j < 3) {
                    if (dp[i-1][prev_j] > max_prev) {
                        max_prev = dp[i-1][prev_j];
                    }
                }
            }
            if (max_prev != INT_MIN) {
                dp[i][j] = coin + max_prev;
            }
        }
    }

    int result = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < 3; j++) {
            if (dp[i][j] > result) {
                result = dp[i][j];
            }
        }
    }
    cout << result << endl;

    return 0;
}
```