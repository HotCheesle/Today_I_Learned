# Map() 함수와 Iterator, Generator
> ## map()
- map함수는 function과 반복가능한 객체(string, list, tuple, range, set, dict)를 받아서 map 객체를 반환한다.
  
```python
map(function, iterable, *iterable)
return map object
```
  
- 이제 내부 동작을 살펴보면
  
```python
def starmap(function, iterable):
  # starmap(pow, [(2,5), (3,2), (10,3)]) --> 32 9 1000
  for args in iterable:
    yield function(*args) # yield?
    # yield는 return이랑 비슷하나 함수를 종료하지 않고 일시정지 상태로 두고 값만 호출자에게 반환한 후 함수의 실행을 진행한다.
    # 추가정보 검색 키워드 '제너레이터, 이터레이터'
```
- iterable한 인자를 받아서 for 문으로 iterable을 순회하면서 function에 하나씩 넣어가면서 그 결과값을 뱉고 있다.
- 하지만 결과값은 map object에 담겨있으므로 map을 바로 출력하게되면 다음과 같이 map object가 그대로 출력이 된다.
```python
result = map(int, ['1', '45', '25', '34', '99'])

print(result)
>> <map object at 0x0000...>
```
- 위와 같이 print를 해보니 map object와 메모리상에 어디에 위치해 있는지 출력한다.
```python
def print_a(i): 
    print('aa', end=' ')

result = map(print_a, ['1', '45', '25', '34', '99'])

print(result)
>> <map object at 0x0000...>
```
- 이번엔 함수내에 print함수를 넣었는데 여전히 map object만 출력이 된다. 
- 여기에 list()같은 iterable한 자료형으로 형변환을 해주면 비로소 함수가 실행된 결과를 반환하는것을 볼 수 있다.
```python
def print_a(i): 
    print('aa', end=' ')

result = list(map(print_a, ['1', '45', '25', '34', '99']))

print(result)
>> aa aa aa aa aa [None, None, None, None, None]
```
- 함수 내부의 print문도 동작을 하고 이 함수의 리턴값이 없었으므로 자동으로 result리스트에는 None이 할당되어 길이가 5인 None을 가진 리스트가 출력이 되었다.

> yield와 return
>---
> 두 키워드 모두 함수 내에서 값을 반환하는 함수이다. 하지만 작동방식은 서로 다르다.
>- return
>   - return은 함수에서 값을 반환하고 함수의 실행을 종료하는 역할을 한다. 함수가 호출되면 return 문에 있던 값을 호출자에게 반환한 다음 함수를 즉시 종료한다.
>- yield
>   - 반면 yield는 함수를 전부 실행시키지 않고 중단 시켜놓은 상태에서 호출자에게 값을 반환한 후, 함수의 실행을 재개한다. 이를 통해 함수는 이전 상태를 기억하고 다음 호출 시 정지한 지점에서 다시 이어서 실행할 수 있다. 
>   - yield는 주로 반복 가능한 객체를 생성하는데 사용된다.

```python
def yield_test(): 
  yield 1
  yield 2
  yield 45

yi = yield_test()
print(yi)
for i in yi: 
    print(i)

>> <generator object yield_test at 0x0000...>
>> 1
>> 2
>> 3
``` 
- yield로 일시 정지 되어있는 포함된 함수 자체를 변수에 할당하면 generator object가 할당된다. 그리고 generator 객체는 for문같은 iterable을 필요로 하는 함수로 순회할 수 있다. 
- 엄밀히 따지자면 generator를 for로 순회하는것이 아니라 generator는 iterator를 생성해주는 함수 즉 함수 내부에 yield 키워드가 있는 함수를 generator이라고 할 수 있고 이 generator로 생성된 iterator를 for를 통해 순회하는 것이다.
>### generator는 다음과 같은 특징을 가지고 있다.
>- iterable한 순서가 지정된다.
>- 느슨하게 평가가 된다. (함수가 한번에 모두 실행되지 않고 다음 값이 필요하면 그때 실행한다.)
>- 함수의 로컬 변수를 통해 이전 상태가 유지된다.
>- 무한한 순서가 있는 객체를 모델링 할 수 있다. (ex) 명확한 끝이 없는 데이터 스트림)
>- 자연스러운 스트림 처리를 위 파이프라인으로 구성할 수 있다. 
>- `__next__` 내부함수를 통해 다음 값을 반환 받을 수 있다. 

- 이외에도 만약 generator를 동시에 여러개 생성한다면, 서로가 다른 객체이며 각각 독립적으로 동작한다.
```python
h = test_generator() # 1, 2, 3...
i = test_generator()
next(h) # h -> 1
next(h) # h -> 2
next(i) # i -> 1
next(h) # h -> 3
next(i) # i -> 2
next(i) # i -> 3
>> 1 2 1 3 2 3
```

>### Iterator와 Iterable
>- Iterable
>   - 반복가능한 객체로 대표적인 iterable한 타입에는 list, dict, set, str, bytes, tuple, range가 있다.
>- Iterator
>   - 값을 차례대로 꺼낼 수 있는 객체로 generator나 내장함수, iterable객체의 메소드로 객체를 생성할 수 있다.
>   - 내장함수 `iter()`를 사용하면 iterator 객체를 생성할 수 있다. 
>   - iterator는 클래스 내부에 `__iter__` 함수와 `__next__`를 직접 구현하여 만들 수 있다.
```python
class IterableAndIterator:
    def __init__(self, stop_number):
        self.stop_number = stop_number # 종료 값 지정
        self.current_number = 0 # 현재 값 지정

    def __iter__(self):
        return self # 자기 자신 객체를 리턴

    def __next__(self):
        if self.current_number < self.stop_number:
            self.current_number += 1
            return self.current_number
        else:
            raise StopIteration
```