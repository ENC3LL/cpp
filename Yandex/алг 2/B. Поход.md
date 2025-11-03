# B. Поход


![image](./.assets/image-1760362457170.png)

![image](./.assets/image-1760362462544.png)

```c++
#include <iostream>
#include <vector>
#include <string>
using namespace std;

int main() {
    string s;
    getline(cin,s);
    int N=s.length();
    vector<std::vector<int>> matrix(2, std::vector<int>(N+1));
    matrix[0][0]=0; matrix[1][0]=1;
    for (int n=0;n<N;n++) {
        if (s[n]=='L') {
            matrix[0][n+1]=min(matrix[0][n],matrix[1][n])+1;
            matrix[1][n+1]=matrix[1][n];
        }
        else if (s[n]=='R') {
            matrix[0][n+1]=matrix[0][n];
            matrix[1][n+1]=min(matrix[1][n],matrix[0][n])+1;
        }
        else {
            matrix[0][n+1]=matrix[0][n]+1;
            matrix[1][n+1]=matrix[1][n]+1;
        }
    }
    cout << matrix[1][N];   
    return 0;
}
```