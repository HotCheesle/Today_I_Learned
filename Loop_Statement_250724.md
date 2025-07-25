# 반복문 (Loop Statement)
> ## 반복문이란 주어진 코드블록을 여러번 반복해서 실행하는 구문이다.
- for문 
    ---
    - for문은 반복가능한(Iterable) 객체의 요소들을 반복하는데 사용하고 반복 가능한 객체의 요소 개수 만큼 반복한다. 즉 객체를 순회한다.
    ```python
    for 변수 in (itrable): 
        반복할 코드블럭
    ```
    - Iterable한 객체는 `list, tuple, str, dict, set, generator로 생성된 객체` 등이 있다. 
    - 주로 for문과 함께 사용되는 Itrable은 range()이다. range()는 `range object`라는 iterable한 객체를 반환한다.
    - 딕셔너리의 경우 기본적으로 key값만 출력한다. 
    - 중첩리스트의 경우 중첩 for문으로 다음과 같이 쉽게 순회할 수 있다.
    ```python
    elements = [['A', 'B'], ['C', 'D']]

    for element in elements: # element = ['A', 'B']
        for elem in element: # elem = 'A'
            print(elem)
            
    >> A
    >> B
    >> C
    >> D
    ```
    > 리스트 컴프리헨션
    ---
    - for문을 통하여 리스트를 아주 간단하게 만들 수 있는데 리스트를 생성할 때 대괄호 내부에 for문을 사용하여 리스트를 만드는 것으로 다음과 같이 사용할 수 있다.
    ```python
    my_list = [i for i in range(10)]
    print(my_list)
    
    >> [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    # 아래의 코드와 같다.
    my_list = []
    for i in range(10): 
        my_list[i] = i
    # 또는 
    for i in range(10): 
        my_list.append(i)
    ```
    - 위의 코드를 보면 여러줄 걸쳐 작성해야할 내용을 리스트 내부에 for문을 사용함으로 써 간편하게 리스트를 작성할 수 있다. 
    - 또 다른 예로 파이썬 공식문서에 있는 예시를 가져오면 제곱수가 들어있는 리스트를 만들고 싶을 때
    ```python
    squares = [x**2 for x in range(10)]
    >> [0, 1, 4, 9, 16, 25, 36, 42, 64, 81]
    ```
    - 위와 같이 한줄에 선언할 수 있다. 또한 컴프리헨션은 여러개의 for문과 if문을 이용하여 조합을 출력하도록 할 수도 있다.
    ```python
    [(x, y) for x in [1, 2, 3] for y in [3, 4, 5] if x != y]
    >> [(1, 3), (1, 4), (1, 5), (2, 3), (2, 4), (2, 5), 
        (3, 4), (3, 5)]
    ```
    - 위의 예시는 각각 [1, 2, 3]과 [3, 4, 5]를 순회하면서 동시에 if문으로 x와 y가 같지 않아야 한다는 조건을 걸고 있다. 그 결과 (3, 3)을 제외한 모든 조합이 리스트에 포함되었다. 
    - 심지어 함수를 반복시킬 수도 있다.
    ```python
    from math import pi
    [str(round(pi, i)) i for in range(1, 6)]
    >> ['3.1', '3.14', '3.142', '3.1416', '3.14159']
    ```
    - 위에서는 round함수 내에 들어갈 인자를 컴프리헨션으로 집어넣고 있다. 이처럼 수식뿐만 아니라 다른 함수도 반복시킬 수 있다.
    - 단, 너무 복잡하거나 중첩된 컴프리헨션은 zip()이나 map()같은 다른 내장함수를 이용하는것이 더 편하고 코드도 간결해질 수 있다.
- for else문
    ---
    - for else문은 for 루프가 break로 중단되지 않고 iterable객체를 모두 순회했을 때 (끝까지 실행되었을 때) 아래의 else문이 실행된다.
    ```python
    for 변수 in iterable: 
        반복코드
        if 조건: 
            break
    else: 
        iterable을 모두 소비할시 처리문
    ```
    ```python
    for i in range(5): 
        print(i)
        if i == 3: 
            print("반복이 중단되었습니다.")
            break
    else: 
        print("이 메세지는 출력되지 않습니다.")
        
    >> 0
    >> 1
    >> 2
    >> 반복이 중단되었습니다.
    ```
    - 위의 경우 i == 3 조건문에서 break가 걸리므로 else문이 실행되지 않는다. 
    - 만약 break가 걸리지 않는다면 else문이 실행된다
    ```python
    lst = [4, 6, 1, 7, 2, 9, 3, 0, 5]

    for l in lst: 
        if l == 8: 
            print('8을 찾았습니다.')
            break
    else: 
        print('8을 찾지 못했습니다.')
        
    >> 8을 찾지 못했습니다.
    ```
    - 위와 같이 특정 값을 찾기위해 리스트 순회를 할 때 만약 찾는 값이 없다면 for문을 모두 돌고 빠져나올 것이므로 별도의 Flag를 만들지 않고도 else로 예외 처리를 할 수 있다.
- while문
    ---
    - while문은 주어진 조건식이 `True`인 동안 코드를 반복해서 실행한다. 조건식은 매 반복 코드를 완료할때 마다 검사하며 이때 검사결과가 `False`라면 반복을 멈추고 while문을 빠져나온다.
    - 위처럼 `True`인 동안 계속해서 실행이 되므로 조건식이 `False`에 도달하지 못하거나 `break`가 없다면 무한루프에 빠질 위험이 존재한다. 따라서 while문을 작성할 때는 조건식이 `False`로 수렴하거나 `break`가 있어야 한다.
    ```python
    while 조건식: 
        반복할 코드블럭
    ```
    ```python
    a = 0

    while a < 3: 
        print(a)
        a += 1
        
    >> 0
    >> 1
    >> 2
    ```
    - 위의 코드에서는 a 가 매 반복마다 1씩 늘어나다가 3이 되는 순간 조건문 검사에서 `False`가 되어서 while문을 종료한다.
    - for문과의 차이는 종료시점이 명확하지 않다는 것이다. for문의 경우 반복횟수가 정해져 있는 반면 while문은 조건문에 의해 제어될 뿐 정확한 종료시점은 input데이터에 따라 달라질 수 있다는 점에서 가장 큰차이를 보인다. 또한 while문은 종료 되었을 때의 상태를 보장한다는 점이 특징이다.
    ```python
    c, r = 7, 6
    x, y = 1, 1
    while True: 
        seat_num += ((c+r)*2) - 4
        if seat_num > n or (c < 3 or r < 3): 
            seat_num -= ((c+r)*2) - 4
            break
        c -= 2
        r -= 2
        x += 1
        y += 1
    ```
    - 위의 코드는 알고리즘 문제 풀이의 일부분인데 if문과 break를 통해 while을 빠져나오고 있다. 위의 코드에서는 seat_num에 숫자가 더해지면서 n을 넘으면 롤백하고 종료되게 하고 있으므로 while문이 종료되었을 때 seat_num은 항상 n 보다는 작다는 결과를 보장한다.
    - while문은 위와같은 특징 때문에 가변 데이터를 받아서 처리를 하거나 특정 값이 입력될때 까지 또는 특정 조건이 만족 할때 까지 반복해야 하는 상황에서 주로 많이 사용한다.
    - while문을 제어하는 방법은 여러가지가 있는데
        - 위의 코드 예시처럼 for문처럼 매 반복마다 flag변수를 하나 만들어서 일정 횟수가 반복되게 되면 반복이 종료되게 하거나
        - 조건문을 `False`로 수렴하게 잘 작성하여 원하는 상태까지 반복하도록 만들거나
        - while 내부에서 if문으로 조건을 검사하여 break문으로 강제로 빠져나오도록 만들수도 있다.
- while else문
    ---
    - while문도 마찬가지로 else문을 넣을 수 있다. 동작은 for else와 동일하다. break로 강제종료 되지 않으면 else문이 실행된다.
    - while문의 첫번째 예시의 경우 break문이 없으므로 else가 있다면 무조건 동작한다.
    - 두번째 예시의 경우 반드시 break문으로 멈추므로 else를 작성한다면 그 코드에는 도달할 수 없다. 
    ```python
    while 조건문: 
        반복 코드
        break
    else: 
        조건문이 False가 되어 종료될 시 실행될 코드
    ```
    - for else와 마찬가지로 특정 조건까지 반복하다가 다른 특수조건(if)에 의해 break되지 않는다면 예외처리 목적으로 else문을 사용할 수 있겠다.