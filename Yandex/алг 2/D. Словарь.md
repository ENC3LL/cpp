# D. Словарь


![image](./.assets/image-1760362509541.png)

```c++
#include <iostream>
#include <vector>
#include <string>
using namespace std;

bool in(string, vector<string>);
bool intin(int, vector<int>);

int main() {
    string sentence;
    getline(cin,sentence);
    int N;
    cin >> N;
    cin.ignore();
    vector<string> dict;
    vector<string> result;
    vector<int> ex;
        for (int i=0;i<N;i++) {
        string word;
        getline(cin,word);
        dict.push_back(word);
    }
    int flag=0;
    string w;
    
    while(true) {
    for(int i=0;i<sentence.length();i++) {
        w+=sentence[i];
        if (in(w, dict)==true and intin(i,ex)==false) {
            result.push_back(w);
            flag=i;
            w="";
        } 
    }
    if (w!="") {
        ex.push_back(flag);
        flag=0;
        w="";
        result.clear();
    }
    else {
        break;
    }
}
   string resultstr;
   for (int j=0; j<result.size();j++) {
    if (j > 0) {
        resultstr += " ";
    }
    resultstr += result[j];
}
   cout << resultstr << w;
   return 0;
}


bool in(string p, vector<string> dictionary) {
    for (int i=0; i<dictionary.size();i++) {
        if (dictionary[i]==p) {
            return true;
        }
    }
    return false;
}

bool intin (int num, vector<int> except) {
    for (int i=0; i<except.size();i++) {
        if (except[i]==num) {
            return true;
        }
    }
    return false;
}
```