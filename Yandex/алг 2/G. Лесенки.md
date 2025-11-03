# G. Лесенки


![image](./.assets/image-1760362623367.png)

```c++
#include <iostream>
#include <vector>

using namespace std;

int main() {
    int N;
    cin >> N;
    vector<long long> dp(N + 1, 0);
    dp[0] = 1;
    for (int k = 1; k <= N; k++) {
        for (int i = N; i >= k; i--) {
            dp[i] += dp[i - k];
        }
    }
    cout << dp[N] << endl;
    return 0;
}
```