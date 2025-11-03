# A. Мячик на лесенке

![image](./.assets/image-1760362490912.png)

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {

    int n;
    cin >> n;

    if (n <= 0) return 0;
    if (n == 1) return 1;
    if (n == 2)return 1;
    if (n==3)return 2;

    int pr1 = 1;
    int pr2 = 2;
    int pr3 = 4;
    int c = 0;

    for (int i =4; i <= n;i++) {
        c = pr1 + pr2 + pr3;
        pr1 = pr2;
        pr2 = pr3;
        pr3 = c;
    }
    

    cout << c << endl;
    return 0;
}
```