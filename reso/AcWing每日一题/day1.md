# Day 1---货舱选址(104)

## 数学原理

|x - a| + |x - b| >= |a - b|

当 x 取在 a和b中间的任意点，左式取到最小值。

那么目标函数|a1 - x| + |a2 - x| + ... + | an - x| 若要取得最小值，将a1-an一组，a2-a(n-1)一组，两两一组，那么当x取到所有数的中位数，就满足条件，取得最小值|an - a1|+|a(n-1) - a2 | + .......

## AC代码

```cpp
#include<iostream>
#include<algorithm>
using namespace std;

int a[100050];
int main(){
    int n;
    cin>>n;
    for(int i = 0;i < n; i++){
        cin >> a[i];
    }
    sort(a, a+n);
    int res = 0;
    for(int i = 0; i < n; i++){
        res += abs(a[i] - a[n/2]);
    }
    cout<<res;
    return 0;
}
```

