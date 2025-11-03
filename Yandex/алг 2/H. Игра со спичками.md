# H. Игра со спичками


![image](./.assets/image-1760362652306.png)

```c++
#include <iostream>
#include <vector>
using namespace std;

bool isPrime(int);
bool intin(int,vector<int>);

int main() {
    int N;
    cin >> N;
    vector<bool> win(N+1,false);
    win[0]=false;

    for (int i=1; i<=N;i++) {
        bool result = false;
        for (int k=1; k<=3;k++) {
            int pos= i-k;
            if (pos>=0) {
                if (!isPrime(pos)) {
                    if (!win[pos]) {
                        result=true;
                        break;
                    }
                }
            }
        }
        win[i]=result;
    }
    if (win[N]) {
        cout<<1;
    }
    else {
        cout<<2;
    }
    return 0;
}
bool isPrime(int num) {
    if (num < 2) {
        return false;
    }
    for (int i = 2; i * i <= num; i++) {
        if (num % i == 0) {
            return false;
        }
    }
    return true;
}
```
