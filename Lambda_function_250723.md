# Lmabda 함수
---
- 람다 함수는 익명 함수 라고도 부른다.
- 람다 함수는 함수명이 없는 함수로 일반적으로는 일회성으로 사용하거나 함수를 인자로 전달하거나 함수로 정의하기에는 매우 간단한 리턴값을 가지는 경우 유용하게 사용한다.
- 람다 함수는 다음과 같이 사용한다.
```python
lambda arguments: expression

add = lambda x, y: x + y
add(4, 6)
>> 10
```
- 위의 람다 함수는 아래의 `def` 함수와 완전히 같다.
```python
def add(x, y): 
    return x + y
```
- 람다 함수는 위와같은 함수를 한줄로 간단하게 표현할 수 있기 때문에 map()과 같은 함수와 함께 활용하기 좋다. 
```python
my_list = [1, 2, 3, 4, 5]
my_list2 = list(map(lambda x: x * 2, my_list))
print(my_list2)
>> [2, 4, 6, 8, 10]
```
- map의 함수 부분에 람다 함수를 작성하면 따로 함수를 선언할 필요 없이 한 라인 안에서 연산을 할 수 있다. 
- 또한 filter()나 sorted()등의 함수와 조합하여 다양하게 응용 할 수 있다. 
```python
my_list = [1, 2, 3, 4, 5]
my_list2 = list(filter(lambda x: x % 2 == 1, my_list))
print(my_list2)
>> [1, 3, 5]
```
- filter를 통해 조건에 맞는 값만 선택할 수도 있다.
```python
my_list = ['coconut', 'apple', 'banana']
my_list2 = sorted(my_list, key=lambda x: len(x))
print(my_list2)
>> ['apple', 'banana', 'coconut']
```
- sorted에 키값을 람다 함수로 정의된 문자열의 길이를 기준으로 정렬할 수도 있다.
```python
my_dict = [
    {'name': 'aaa', 'age': 15, 'gender': 'male'}, 
    {'name': 'bbb', 'age': 23, 'gender': 'female'}, 
    {'name': 'ccc', 'age': 30, 'gender': 'male'}
    ]
my_dict2 = list(map(lambda dict: dict(name = dict['name'], age = dict['age'], my_dict)))
print(my_dict2)
>> [{'name': 'aaa', 'age': 15}, {'name': 'bbb', 'age': 23}, {'name': 'ccc', 'age': 30}]
```
- 기존 딕셔너리 리스트의 일부 key값만을 갖는 딕셔너리 리스트를 map()함수와 람다 함수를 통해 쉽게 만들 수도 있다.
- 람다 함수는 한줄로 간편하게 함수를 선언할 수 있다는 장점이 있지만 함수의 로직이 조금이라도 복잡해지면 람다 함수로는 선언하는것이 더 힘들어지기 때문에 간단한 연산이나 get동작 같은 상황에만 사용하는 것이 좋다.