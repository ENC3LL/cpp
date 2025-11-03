# I. Цепочка в таблице


![image](./.assets/image-1760362680842.png)

```c++
#include <iostream>
#include <vector>
#include <algorithm>
#include <tuple>

using namespace std;

int main() {
    int n, m;
    cin >> n >> m;
    vector<vector<int>> matrix(n, vector<int>(m));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            cin >> matrix[i][j];
        }
    }

    vector<tuple<int, int, int>> points;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            points.push_back({matrix[i][j], i, j});
        }
    }

    sort(points.begin(), points.end());

    vector<vector<int>> dp(n, vector<int>(m, 1));
    int ans = 1;

    int dx[] = {-1, 1, 0, 0};
    int dy[] = {0, 0, -1, 1};

    for (auto& point : points) {
        int val = get<0>(point);
        int i = get<1>(point);
        int j = get<2>(point);

        for (int d = 0; d < 4; d++) {
            int ni = i + dx[d];
            int nj = j + dy[d];
            if (ni >= 0 && ni < n && nj >= 0 && nj < m) {
                if (matrix[ni][nj] == val - 1) {
                    dp[i][j] = max(dp[i][j], dp[ni][nj] + 1);
                }
            }
        }
        ans = max(ans, dp[i][j]);
    }

    cout << ans << endl;

    return 0;
}
```