# Linked List (연결 리스트)
> 연결리스트는 다른 추상 자료형을 구현할 때 기반이 되는 기초 선형 자료구조이다. 각 노드가 데이터와 다음노드의 주소를 갖고 한줄로 연결되어 있는 방식으로 데이터를 저장한다.\
`Head`-->`Data, next` --> `Data, next`--> . . . `Data, None` \
의 형식으로 데이터를 저장한다.

- 배열(array)과 연결리스트의 차이점
    ---
    >- 배열은 물리적으로 연결된 메모리에 동일한 자료형을 연속적으로 저장한다.
    >- 배열은 인덱스로 값에 접근하기 때문에 임의 접근이 가능하다. 따라서 특정 값을 탐색하는데 걸리는 시간복잡도는 **O(1)** 이다.
    >- 하지만 배열은 처음 선언한 크기를 변경할 수 없고 값을 추가하거나 삭제하려면 후행 데이터들을 옮겨야 하므로 추가, 삭제 작업 시 시간복잡도는 **O(n)** 이다. 
    ---
    >- 연결리스트는 메모리는 임의의 위치에 존재하고 각각의 노드가 다음 노드의 주소 정보를 통해 연결되어있다.
    >- 연결리스트는 순서는 존재하지만 인덱스가 없기 때문에 앞에서부터 순차적으로 탐색해야한다. 따라서 특정 값을 탐색하는데 걸리는 시간 복잡도는 **O(n)** 이다. 
    >- 하지만 연결리스트는 크기를 동적으로 할당할 수 있고 값을 추가하거나 삭제할때 작업 위치에 관계가 없기 때문에 추가, 삭제 작업 시 시간복잡도는 **O(1)** 이다. 

## 그러나 파이썬에서는 배열이 아닌 리스트 자료형이 따로 존재한다.
- 그렇다면 List자료형과 연결리스트는 어떤 차이가 있을까
    ---
    >- Python에서 List자료형은 동적으로 크기를 할당한다. 하지만 연결리스트처럼 노드단위로 저장하는것이 아니라 배열처럼 연속된 메모리 주소를 갖는다. 
    >- List는 인덱스를 갖는 시퀀스 자료형이므로 데이터에 임의 접근 할 수 있다. 따라서 탐색하는데 걸리는 시간복잡도는 **O(1)** 이다.
    >- 하지만 배열과 같은 메모리 구조를 갖고있기 때문에 추가, 삭제 시에는 배열과 같은 이유로 시간복잡도는 **O(n)** 이 된다.
    >- 추가로 List는 공간이 부족하면 이전 공간의 두배 크기의 새로운 배열에 할당하는데 내부 동작에서 이전 배열에서 새로운 배열로 값을 복사해야 하기 때문에 **O(n)** 의 시간이 걸리게 된다.
    >- 접근이 적고 값의 추가와 삭제가 빈번한 자료를 저장할 때는 배열이나 리스트 보다는 연결리스트를 사용하는것이 좋다.

## 연결리스트의 구현
> Node Class
```python
Class Node: 
    def __init__(self, data): 
        self.data = data
        self.next = None
```
- data에 노드에 저장할 데이터가 들어가고 Node 객체가 처음 생성되면 다음 노드 주소가 저장될 next에는 None으로 초기화 된다.
> Insert의 구현
```python
def insert(head, data, index): 
    new_node = Node(data)
    if index == 0: 
        new_node.next = head
        head = new_node
        return head
    current_node = head
    for _ in range(index - 1): 
        current_node = current_node.next
    new_node.next = current_node.next
    current_node.next = new_node
    return head
```
- 데이터를 담은 새로운 노드를 생성하고 만약 삽입할 위치가 맨 앞(head)이라면 현재 head를 새로운 노드의 next에 넣고 새로운 노드를 head에 할당한 뒤 head를 반환한다.
- 맨 앞이 아니라면 index-1 번 만큼 후행 노드로 간 뒤 그 뒤에 새로운 노드를 삽입한다.
- 이 경우 가장 마지막 노드(next가 None인) 뒤쪽으로 삽입되더라도 새로운 노드의 next가 None이 되고 마지막이였던 노드의 next가 새로운 노드를 가르키면서 자연스럽게 새로운 노드가 tail이 된다.
> Delete의 구현
```python
def delete(head, data) # data로 삭제할 시
    current_node = head
    pre_node = None
    try: 
        while current_node.data != data: 
            pre_node = current_node
            current_node = current_node.next
    except:
        priint("can't find data!!")
        return head
    if current_node is head: 
        head = current_node.next
        return head
    pre_node.next = current_node.next
    return head
```
- 해당 노드의 앞과 뒤의 노드를 이어주어야 하기 때문에 현재 노드와 이전 노드의 정보 모두 필요하다.
- while로 해당하는 데이터가 있는 노드까지 순회한뒤 만약 삭제할 노드가 head라면 head다음 노드를 head로 만들어주면 간단하게 삭제가 가능하다. 만약 삭제할 값을 찾지 못하였다면 None에서 .next를 참조하려 할때 exception이 발생하는데 이때 try문으로 예외처리를 하면 된다.
- 삭제할 노드의 이전 노드의 next를 다음노드에 이어주면 삭제할 노드는 자연스럽게 참조가 불가능하게 바뀐다. 
- 파이썬의 경우 Garbege Collection을 통해 자동으로 메모리 관리를 하기 때문에 삭제한 노드를 임의로 메모리 할당을 해제시킬 필요는 없다.
