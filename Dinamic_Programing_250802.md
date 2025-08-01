# Dinamic Programing (DP)
## 다이나믹 프로그래밍?
- 최적화 이론의 한 기술이며 전체에 대한 최적해를 구하기 위해 일부에서의 최적해를 사용해서 효율적으로 구하는 알고리즘 기법이다.
- 이전 최적해를 구하려면 이전의 최적해를 기억하고 있어야 하는데 이를 `메모이제이션(Memoization)`이라고 한다. 또는 (주로 개발현장에서는) `캐싱(caching)`이라고 한다.
- 쉽게 말하자면 어떤 문제를 풀기위해 그 문제를 작은 문제의 연장으로 생각하고 과거에 구한 해를 이용하는 방식의 알고리즘을 총칭한다.
- 사실 이름처럼 다이나믹 하거나 하진 않다. 오히려 번역한 `기억하며 풀기`가 DP의 본질에 더 가깝다.
- DP를 이용하는 알고리즘 문제를 하나 소개하자면 
> 플랫폼: `백준` 문제번호: `14501` 문제제목: `퇴사` 사용 알고리즘: `DP, 브루탈 포스` \
> 링크: https://www.acmicpc.net/problem/14501

문제
-
상담원으로 일하고 있는 백준이는 퇴사를 하려고 한다.

오늘부터 N+1일째 되는 날 퇴사를 하기 위해서, 남은 N일 동안 최대한 많은 상담을 하려고 한다.

백준이는 비서에게 최대한 많은 상담을 잡으라고 부탁을 했고, 비서는 하루에 하나씩 서로 다른 사람의 상담을 잡아놓았다.

각각의 상담은 상담을 완료하는데 걸리는 기간 Ti와 상담을 했을 때 받을 수 있는 금액 Pi로 이루어져 있다.

N = 7인 경우에 다음과 같은 상담 일정표를 보자.

|   |1일|2일|3일|4일|5일|6일|7일 |
|---|---|---|---|---|---|---|---|
|Ti |3  |5  |1  |1  |2  |4  |2  |
|Pi |10 |20 |10 |20 |15 |40 |200|

1일에 잡혀있는 상담은 총 3일이 걸리며, 상담했을 때 받을 수 있는 금액은 10이다. 5일에 잡혀있는 상담은 총 2일이 걸리며, 받을 수 있는 금액은 15이다.

상담을 하는데 필요한 기간은 1일보다 클 수 있기 때문에, 모든 상담을 할 수는 없다. 예를 들어서 1일에 상담을 하게 되면, 2일, 3일에 있는 상담은 할 수 없게 된다. 2일에 있는 상담을 하게 되면, 3, 4, 5, 6일에 잡혀있는 상담은 할 수 없다.

또한, N+1일째에는 회사에 없기 때문에, 6, 7일에 있는 상담을 할 수 없다.

퇴사 전에 할 수 있는 상담의 최대 이익은 1일, 4일, 5일에 있는 상담을 하는 것이며, 이때의 이익은 10+20+15=45이다.

상담을 적절히 했을 때, 백준이가 얻을 수 있는 최대 수익을 구하는 프로그램을 작성하시오.

입력
-
첫째 줄에 N (1 ≤ N ≤ 15)이 주어진다.

둘째 줄부터 N개의 줄에 Ti와 Pi가 공백으로 구분되어서 주어지며, 1일부터 N일까지 순서대로 주어진다. (1 ≤ Ti ≤ 5, 1 ≤ Pi ≤ 1,000)

출력
-
첫째 줄에 백준이가 얻을 수 있는 최대 이익을 출력한다.

---

>- 위의 문제에서는 퇴사하기 전까지 기간에 대한 최대 수익을 구해야 한다. DP는 전체에 대한 최대 수익을 일부의 최대수익을 먼저 구하고 구간이 증가할 때 마다 이전에 구해놓은 최대 수익을 이용해 새로운 최대 수익을 구한다. 

>- 또는 상담일정의 최대 일수가 15일 이므로 가능한 모든 경우의 수를 계산하는 브루트 포스 알고리즘으로도 해결이 가능하다. 

- 먼저 일부 구간의 최대 수익을 결정하는 방식을 생각해보자. \
만약 구간이 1이라면 해당 상담을 선택하는 것이 반드시 최대 수익이 될 것이므로 무조건 선택해야 한다.\
그리고 구간을 1만큼 늘려 2라면 어떻게 해야할까\
먼저 새로 추가된 2일 째 상담을 선택한다. 그 다음 선택이 가능다면 1일째 상담을 선택한다. 이후 기억해 두었던 이전 구간인 1일의 최대 수익과 2일 째의 최대 수익을 비교해서 더 큰 최대 수익을 선택한다.

- 다음 N구간에서 N+1구간의 최대 수익을 구하려면 어떻게 해야 할까\
먼저 N+1일 째 상담을 선택한 다음 선택이 가능한 가장 가까운 일자의 최대 수익을 더한다. 이후 N일 째의 최대 수익과 N+1일 째의 최대 수익을 비교하여 더 큰 최대 수익을 선택한다.

- 이러한 아이디어에서 전체에 대한 최대 수익을 구하기 위해 일부 구간의 최대 수익을 기억해 두었다가 조금씩 구간을 확장 해 나갈 때 이전 최대 수익을 사용해 새로운 최대 수익을 계산하고 이러한 구간에 대한 동작을 반복해 나가면서 결국에는 전체에 대한 최대 수익을 구하는 방식이 바로 동적 계획법(DP)이다. 

- 위의 아이디어 대로 풀이한 결과를 살펴보자

소스코드
- 
```python
n = int(input())

schedule = list(list(0 for _ in range(n)) for _ in range(2))
max_gains = list(0 for _ in range(n))

def find_best(idx): 
    """ schedule[idx]의 상담을 추가해서 이전 최대 이득과 비교해서
    더 큰 값을 max_gains[idx]에 넣는다.
    """
    try: 
        new_max = schedule[1][idx] + max_gains[idx+schedule[0][idx]] # N일을 선택할 때의 새로운 최대 수익
        max_gains[idx] = max(max_gains[idx+1], new_max)# 이전 최대 수익과 비교해서 더 큰쪽을 선택
    except: # IndexError 발생하는 경우는 확인하는 상담만으로 가득 채울때 이다.
        if idx+1 < n: 
            max_gains[idx] = max(max_gains[idx+1], schedule[1][idx]) # 확인하는 상담이 끝까지 다 채울때
        else: 
            max_gains[idx] = schedule[1][idx] # 마지막 1일 경우

for i in range(n): 
    day, cost = map(int, input().split())
    schedule[0][i] = day
    schedule[1][i] = cost
    
for i in range(n): # 퇴사로 인해 상담 못하는 날짜 제외
    if schedule[0][i] > n - i: 
        schedule[0][i] = 0
        schedule[1][i] = 0

for i in range(len(schedule[0])-1, -1, -1): 
    if schedule[0][i] == 0: 
        try: 
            max_gains[i] = max_gains[i+1]
        except: 
            max_gains[i] = 0
        finally: 
            continue
    find_best(i) 

print(max_gains[0]) # 1일째 최대 수익이 전체 구간에 대한 최대 수익이다.
```

- 먼저 1일차에서 시작하기보다 끝 날짜에서 거꾸로 구간을 늘려왔다. 왜냐하면 순방향으로 늘려나가면 N일을 선택했을 때 그 이전 구간에 대해 선택을 못하게 되는 경우를 최소 5일 까지 계산을 해야 하는데 끝에서 부터 선택하면 단순히 이전 최대 수익에서 N일째 상담의 상담 일수만큼 전의 최대수익을 바로 가져오면 되기 때문이다. 
> 순방향
> |N-5|N-4|N-3|N-2          |N-1|N   |        |
> |---|---|---|-------------|---|----|--------|
> |?  |2  |4  |2            |2  |3   |상담일수|
> |?  |O  |X  |O            |X  |선택|선택가능|
> |   |   |   |^이전 최대수익|   |    |        |
>
> N일째의 최소 5일 이전을 체크해야 N일째의 최대 수익이 `N-2의 최대 수익 + N 수익`으로 결정됨

> 역방향
> |N   |N+1|N+2|N+3          |N+4|N+5|       |
> |----|---|---|-------------|---|---|-------|
> |3   |2  |4  |2            |2  |?  |상담일수|
> |선택|X  |X  |O            |O  |O  |선택가능|
> |    |   |   |^이전 최대수익|   |   |        |
>
> 역방향으로 구간을 늘릴 경우 N일째 상담기간 만큼 뒤의 최대수익을 더하면 즉시 최대 수익이 `N+(N의 상담일수-1)의 최대 수익 + N 수익`으로 결정됨

- 끝 날짜에서부터 하루씩 구간을 늘려가다보면 결국에는 첫째날의 최대 수익이 전체 구간에 대한 최대 수익이 될것이다. 
---
- 이런 문제 이외의 다른 예시로 피보나치 수열이 있다. 피보나치의 경우도 N번째 수를 구할 때 처음부터 더해 가면서 구하는 것이 아니라 N-1과 N-2를 기억해 두었다가 N번째 수를 찾을 때에는 N-1과 N-2를 더해서 간단하게 구하는 것이다.