## 후기

원래 골드 두 문제 풀려고 했었다. 
골드5랑 골드3 두 문제만 풀어야지~ 싶었는데 오랜만에 토요라운드에 참가하니 난이도가 바뀌어있었다. 
골드5는 없고 골드3, 골드2가 있길래 실버2와 골드3을 잡기로 했다. 
다음 토요라운드에는 골드3, 골드2를 잡아봐야지.


## D 16493 최대 페이지 수 10:09

엇 그냥 비트마스크로 모든 경우의 수를 구하면 되지 않을까 싶었다. 
m이 20이니깐 2^20만큼 걸릴 것이다. 
그런데 바로 시간 복잡도 계산이 안 돼서 음 2^10이 대략 1,000이고 천 * 천 = 10^6이라 10^9보다 작으니 되겠다 싶었다.
빠르게 풀고 통과했다. 굿굿.


## E 14621 나만 안되는 연애 11:04

엇 MST...? 
MST 일년 전에 한번 풀어봤는데 기억이 안 났다.
블로그를 뒤졌다. 
블로그에 정리도 안 해놨다. 
이전에 내가 푼 코드 + 검색으로 MST 개념부터 다시 공부하고 풀었다. 

1. 그리디하게 edge의 길이를 저장해놓는다. 
2. 저장할 때 여-여, 남-남은 필요없으니 걸러서 저장한다
3. 오름차순 정렬을 한다
4. 짧은 것부터 뽑아서 계산한다
5. 뽑을 때 Union find를 활용해서 같은 집합에 속했는지 안 속했는지 확인한다
6. 같은 집합이라면 사이클이므로 패스한다
7. 뽑은 edge의 개수가 n - 1인지 확인한다
8. 끝~

그래도 풀어서 다행이다. 
재밌었다! 
나는 다익스트라, 넵섹, 등등 이런 알고리즘 개념들이 두렵고 외면만 하고 있었는데 어쩔 수 없이 마주해버렸다. 
MST는 다시 나와도 이제는 편하게 풀 수 있을 것 같다. 

## 이후

한 시간 정도 시간이 남아서 코드 정리도 하고 또 뭐 하지 고민하다가 현욱님 코드를 참고했다. 
잘하는 사람 코드 읽는 건 도움이 된다..
MST 코드는 비슷했고 람다를 사용했길래 C++에서 람다를 어떻게 사용하는지 배웠다. 

## D번 넵섹으로 풀기

넵섹을 공부했다. dp로 푸는구나.. 

**넵섹**

- 물건의 무게와 가치가 주어지고, 담을 수 있는 배낭의 최대 용량이 주어진다
- 배낭에 넣을 수 있는 물건들의 가치 합의 최댓값 구하기
- dp[i][j] 처음부터 i까지 물건을 살펴보고, 배낭의 용량이 j였을 때 배낭에 들어간 물건 가치 합의 최댓값

-> 결국 배낭에 물건을 넣은 경우 / 넣지 않았을 경우 중 가치가 더 큰 걸 고르는 것 같다. 

코드는 현욱님 코드 염탐했다. 

```
#include <iostream>
#include <algorithm>
#include <vector>
#include <string>
#include <functional>
#include <string>
#include <queue>
#include <deque>
#include <stack>
#include <set>
#include <map>
#include <cmath>
#include <cstring>
#include <bitset>
#include <stdio.h>
#include <math.h>
#include <sstream>

#define xx first
#define yy second
#define all(x) (x).begin(), (x).end()

using namespace std;
using i64 = long long int;
using ii = pair<int, int>;
using iis = pair<int, string>;
using ii64 = pair<i64, i64>;
using iii = tuple<int, int, int>;

int table[205][25];
vector<ii> book;

// day: 남은 일 수, idx: 인덱스
int solve(int day, int idx) {
    // book 사이즈 만큼만 확인
    if (idx == book.size())
        return 0;
    
    auto& res = table[day][idx];
    
    if (res != -1)
        return res;
    
    // 책을 안 읽는 경우
    res = solve(day, idx + 1);
    
    // 책을 읽는 경우
    // 소요되는 일 수가 현재 일 수보다 작다면
    if (book[idx].xx <= day)
        // 남은 일 수에서 소요되는 일 수를 뺸다
        // 그리고 챕터의 수는 더한다
        res = max(res, solve(day - book[idx].xx, idx + 1) + book[idx].yy);
    
    // 책을 읽는 경우 / 안 읽는 경우 중 큰 값 리턴
    return res;
}

int main() {
    int n, m;
    scanf("%d %d", &n, &m);
    
    // dp 초기화를 합니다
    memset(table, -1, sizeof(table));
    
    book.resize(m);
    
    for (int i = 0; i < m; i++)
        scanf("%d %d", &book[i].xx, &book[i].yy);
    
    printf("%d\n", solve(n, 0));
    
    return 0;
}
```

