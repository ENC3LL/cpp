# E. Башня


![image](./.assets/image-1760362540854.png)

![image](./.assets/image-1760362548491.png)

```c++
#include <iostream>
#include <vector>
#include <algorithm>
#include <climits>

using namespace std;

int main() {
    int N, K;
    cin >> N >> K;
    vector<int> A(N);
    for (int i = 0; i < N; i++) {
        cin >> A[i];
    }

    vector<int> prefix(N + 1, 0);
    for (int i = 1; i <= N; i++) {
        prefix[i] = prefix[i - 1] + A[i - 1];
    }

    vector<double> value(N - K + 1, 0.0);
    for (int i = 0; i <= N - K; i++) {
        int sum = prefix[i + K] - prefix[i];
        int min_val = INT_MAX;
        for (int j = i; j < i + K; j++) {
            if (A[j] < min_val) min_val = A[j];
        }
        value[i] = (double)sum * min_val;
    }

    vector<double> dp(N + 1, 0.0);
    vector<bool> take(N + 1, false);

    for (int i = 1; i <= N; i++) {
        dp[i] = dp[i - 1];
        if (i >= K) {
            double candidate = dp[i - K] + value[i - K];
            if (candidate > dp[i]) {
                dp[i] = candidate;
                take[i] = true;
            }
        }
    }

    vector<int> towers;
    int cur = N;
    while (cur > 0) {
        if (take[cur]) {
            towers.push_back(cur - K + 1);
            cur -= K;
        } else {
            cur--;
        }
    }
    reverse(towers.begin(), towers.end());

    cout << towers.size() << endl;
    for (size_t i = 0; i < towers.size(); i++) {
        cout << towers[i];
        if (i < towers.size() - 1) cout << " ";
    }
    cout << endl;

    return 0;
}
```