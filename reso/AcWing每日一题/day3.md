---
title:Day 3---蛇形矩阵(756)
time:2021-01-22 21:07:00
categories:算法
tags:算法,ACWing,蛇形矩阵
summary:ACWing寒假题目 Day03
---
# Day 3---蛇形矩阵(756)

## 关键点

预设方向数组

`const int dx[] = {0, 1, 0, -1};`
`const int dy[] = {1, 0, -1, 0};`

## AC代码

```c++
#include<iostream>
using namespace std;

const int N = 110;
int res[N][N];

const int dx[] = {0, 1, 0, -1};
const int dy[] = {1, 0, -1, 0};
int main(){
    int n, m;
    cin>>n>>m;
    int cnt = 1;
    int i = 0, j = -1;
    int dir = 0;
    while(1){
        int xx = i + dx[dir];
        int yy = j + dy[dir];
        if(!res[xx][yy] && xx >= 0 && xx < n && yy >= 0 && yy < m){
            res[xx][yy] = cnt++;
            i = xx, j = yy;
        }
        else{
            dir++;dir%=4;
        }
        if(cnt == n*m+1) break;
    }
    for(int i = 0;i < n; i++){
        for(int j = 0; j < m; j++){
            cout<<res[i][j]<<" ";
        }
        cout<<endl;
    }
    return 0;
}
```

