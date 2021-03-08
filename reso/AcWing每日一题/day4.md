# Day 4---红与黑(1113)

## 关键点

洪水灌溉算法：

BFS（最短距离）

DFS（更方便）

## AC代码（BFS)

```c++
#include<iostream>
#include<algorithm>
#include<queue>
using namespace std;

#define x first
#define y second

typedef pair<int, int>PII;

const int N = 25;
char map[N][N];

int n, m;

int bfs(int orix, int oriy) {
    queue<PII>q;
    q.push({orix, oriy});
    int res = 0;

    int dx[] = {-1, 0, 1, 0}, dy[] = {0, 1, 0, -1};

    while(q.size()){
        auto t = q.front();
        q.pop();
        res ++;
        
        for(int i = 0; i < 4; i ++){
            int x = t.x + dx[i], y = t.y + dy[i];
            if(x < 0 || y < 0 || x >= n || y >= m || map[x][y] != '.') continue;
            map[x][y] = '#';
            q.push({x, y});
            
        }
    }
    
    return res;
}

int main(){
    
    while(cin >> m >> n, n || m){
        for(int i = 0;i < n; i++) cin >> map[i];
        int x, y;
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(map[i][j] == '@'){
                    x = i, y = j;
                }
            }
        }
        cout << bfs(x, y) <<endl;
    }    
    return 0;
}

```

