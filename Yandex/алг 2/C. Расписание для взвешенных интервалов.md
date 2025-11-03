# C. Расписание для взвешенных интервалов


![image](./.assets/image-1760362418622.png)

```c++
#include <iostream>
#include <vector>
#include <algorithm>
#include <iomanip>

using namespace std;

struct Interval {
    double start;
    double end;
    double weight;
};

bool compareByEnd(const Interval& a, const Interval& b) {
    return a.end < b.end;
}

int main() {
    int n;
    cin >> n;
    vector<Interval> intervals(n);
    for (int i = 0; i < n; i++) {
        cin >> intervals[i].start >> intervals[i].end >> intervals[i].weight;
    }

    if (n == 0) {
        cout << 0 << endl;
        return 0;
    }

    sort(intervals.begin(), intervals.end(), compareByEnd);

    vector<double> dp(n + 1, 0.0);
    dp[0] = 0.0;

    for (int i = 1; i <= n; i++) {
        double current_start = intervals[i - 1].start;
        double current_weight = intervals[i - 1].weight;

        int left = 0;
        int right = i - 2;
        int found_index = -1;

        while (left <= right) {
            int mid = (left + right) / 2;
            if (intervals[mid].end <= current_start) {
                found_index = mid;
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }

        double candidate = dp[found_index + 1] + current_weight;
        dp[i] = max(dp[i - 1], candidate);
    }

    cout << fixed << setprecision(10) << dp[n] << endl;

    return 0;
}
```