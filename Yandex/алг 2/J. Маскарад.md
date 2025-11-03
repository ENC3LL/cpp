# J. Маскарад


![image](./.assets/image-1760362712566.png)

![image](./.assets/image-1760362718021.png)

```c++
#include <iostream>
#include <vector>
#include <algorithm>
#include <climits>

using namespace std;

const long long INF = 1e18;

int main() {
    int N, L;
    cin >> N >> L;
    vector<int> P(N), R(N), Q(N), F(N);
    int total_max = 0;
    for (int i = 0; i < N; i++) {
        cin >> P[i] >> R[i] >> Q[i] >> F[i];
        total_max += F[i];
    }

    if (total_max < L) {
        cout << -1 << endl;
        return 0;
    }

    vector<vector<long long>> dp(N+1, vector<long long>(total_max+1, INF));
    vector<vector<int>> prev(N+1, vector<int>(total_max+1, -1));
    dp[0][0] = 0;

    int current_max = 0;
    for (int i = 0; i < N; i++) {
        for (int j = 0; j <= current_max; j++) {
            if (dp[i][j] == INF) continue;
            for (int k = 0; k <= F[i]; k++) {
                int new_j = j + k;
                if (new_j > total_max) continue;
                long long cost = (k < R[i]) ? (long long)k * P[i] : (long long)k * Q[i];
                if (dp[i][j] + cost < dp[i+1][new_j]) {
                    dp[i+1][new_j] = dp[i][j] + cost;
                    prev[i+1][new_j] = k;
                }
            }
        }
        current_max += F[i];
        if (current_max > total_max) current_max = total_max;
    }

    long long best_cost = INF;
    int best_j = -1;
    for (int j = L; j <= total_max; j++) {
        if (dp[N][j] < best_cost) {
            best_cost = dp[N][j];
            best_j = j;
        }
    }

    if (best_cost == INF) {
        cout << -1 << endl;
    } else {
        cout << best_cost << endl;
        vector<int> ans(N);
        int j = best_j;
        for (int i = N; i >= 1; i--) {
            ans[i-1] = prev[i][j];
            j -= prev[i][j];
        }
        for (int i = 0; i < N; i++) {
            cout << ans[i];
            if (i < N-1) cout << " ";
        }
        cout << endl;
    }

    return 0;
}
```