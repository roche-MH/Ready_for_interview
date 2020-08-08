# DataStructure

* Array vs Linked List
* Stack and Queue
* Tree
  * Binary Tree
  * Full Binary Tree
  * Complete Binary Tree
  * BST (Binary Search Tree)
* Binary Heap
* Red Black Tree
  * 정의
  * 특징
  * 삽입
  * 삭제
* Hash Table
  * Hash Function
  * Resolve Collision
    * Open Addressing
    * Separate Chaining
  * Resize
* Graph
  * Graph 용어정리
  * Graph 구현
  * Graph 탐색
  * Minimum Spanning Tree
    * Kruskal algorithm
    * Prim algorihtm



## Array vs Linked List

**Array**

가장 기본적인 자료구조인 `Array` 자료구조는, 논리적 저장 순서와 물리적 저장순서가 일치한다. 따라서 `인덱스`(index)로 해당 원소(element)에 접근할 수 있다. 그렇기 때문에 찾고자 하는 원소의 인덱스 값을 알고 있으면 `Big-O(1)` 에 해당 원소로 접근 할수 있다. 즉 random access가 가능하다는 장점이 있는 것이다.

하지만 삭제 또는 삽입의 과정에서는 해당 원소에 접근하여 작업을 완료한뒤(O(1)), 또 한가지의 작업을 추가적으로 해줘야 하기 때문에, 시간이 더 걸린다. 만약 배열의 원소중 어느 원소를 삭제했다고 했을때, 배열의 연속적인 특징이 깨지게 된다. 즉 빈공간이 생기는 것이다. 따라서 삭제한 원소보다 큰 인덱스를 갖는 원소들을 `shift` 해 줘야 하는 비용이 발생하고 이 경우 시간 복잡도는 O(n)가 된다. 그렇기 때문에 Array 자료구조에서 삭제 기능에 대한 time complexity 의 worst case 는 O(n)이 된다.

삽입의 경우도 마찬가지이다. 만약 첫번째 자리에 새로운 원소를 추가하고자 한다면 모든 원소들의 인덱스를 1씩 shift 해줘야 하므로 이 경우도 O(n)의 시간을 요구하게 된다.



**Linked List**

이 부분에 대한 문제점을 해결하기 위한 자료구조가 Linked list 이다. 각각의 원소들은 자기 자신 다음에 어떤 원소인지만을 기억하고 있다. 따라서 이 부분만 다른 값으로 바꿔주면 삭제와 삽입을 O(1) 만에 해결할 수 있는것이다.

하지만 Linked List 역시 한가지 문제가 있다. 원하는 위치에 삽입을 하고자 하면 원하는 위치를 Search 과정에 있어서 첫번째 원소부터 다 확인해봐야 한다는 것이다.

Array와는 달리 논리적 저장 순서와 물리적 저장 순서가 일치하지 않기 때문이다. 이것은 일단 삽입하고 정렬하는 것과 마찬가지이다. 이 과정 때문에, 어떤한 원소를 삭제 또는 추가하고자 했을 때, 그 원소를 찾기 위해서 O(n)의 시간이 추가적으로 발생하게 된다.

결국 Linked list 자료구조는 Search 에도 O(n)의 time complexity를 갖고, 삽입,삭제에 대해서도 O(n)의 time complexity를 갖는다. 그렇다고 해서 아주 쓸모없는 자료구조는 아니기에, 우리가 학습하는 것이다. 이 Linked List 는 Tree 구조의 근간이 되는 자료구조이며, Tree 에서 사용되었을 때 그 유용성이 드러난다.

**Personal Recommendation**

* Array 를 기반으로 한 Linked List 구현
* ArrayList 를 기반으로 한 Linked List 구현



## Stack and Queue

**Stack**

선형 자료구조의 일종으로 `Last In First Out(LIFO)` 즉, 나중에 들어간 원소가 먼저 나온다. 이것은 Stack 의 가장 큰 특징이다. 차곡차곡 쌓이는 구조로 먼저 Stack 에 들어가게 된 원소는 맨 바닥에 깔리게 된다. 그렇기 때문에 늦게 들어간 녀석들은 그 위에 쌓이게 되고 호출시 가장 위에 있는 녀석이 호출되는 구조이다.

**Queue**

선형 자료구조의 일종으로 `First In First Out(FIFO)` 즉, 먼저 들어간 놈이 먼저 나온다. Stack 과는 반대로 먼저 들어간 놈이 맨 앞에서 대기하고 있다가 먼저 나오게 되는 구조이다. 참고로 JAVA Collection 에서 Queue는 인터페이스이다. 이를 구현하고 있는 `Priority queue` 등을 사용할수 있다.

**Personal Recommendation**

* Stack을 사용하여 미로찾기 구현하기
* Queue를 사용하여 Heap 자료구조 구현하기
* Stack 두개로 Queue 자료구조 구현하기
* Stack 으로 괄호 유효성 체크 코드 구현하기



## Tree

트리는 스택이나 큐와 같은 선형 구조가 아닌 비선형 자료구조이다. 트리는 계층적 관계를 표현하는 자료구조이다. 이 `트리`라는 자료구조는 표현에 집중한다. 무엇인가를 저장하고 꺼내야 한다는 사고에서 벗어나 트리라는 자료 구조를 바라보자

**트리를 구성하고 있는 구성요소들(용어)**

* Node(노드): 트리를 구성하고 있는 각각의 요소를 의미한다.
* Edge(간선): 트리를 구성하기 위해 노드와 노드를 연결하는 선을 의미한다.
* Root Node(루트 노드): 트리 구조에서 최상위에 있는 노드를 의미한다.
* Terminal Node (= leaf Node, 단말 노드): 하위에 다른 노드가 연결되어 있지 않은 노드를 의미한다.
* Internal Node(내부노드, 비단말 노드): 단말 노드를 제외한 모든 노드로 루트노드를 포함한다.



**Binary Tree(이진 트리)**

루트 노드를 중심으로 두 개의 서브트리(큰트리에 속하는 작은 트리)로 나뉘어 진다. 또한 나뉘어진 두 서브 트리도 모두 이진 트리어야 한다. 재귀적인 정의라 맞는듯 하면서도 이해하기 쉽지 않을 듯하다. 한가지 덧붙이자면 공집합도 이진 트리로 포함시켜야 한다. 그래야 재귀적으로 조건을 확인해 갔을때, leaf node 에 다달았을때 정의가 만족되기 때문이다. 자연스럽게 노드가 하나 뿐인 것도 이진 트리 정의에 만족하게 된다.

트리에서는 각`층별로` 숫자를 매겨서 이를 트리의 `Level(레벨)` 이라고 한다. 레벨의 값은 0 부터 시작하고 따라서 루트 노드의 레벨은 0 이다. 그리고 트리의 최고 레벨을 가리쳐 해당 트리의 `height(높이)` 라고 한다.



**Perfect Binary Tree (포화 이진트리), Complete Binary Tree (완전 이진트리), Full Binary Tree (정 이진 트리)**

모든 레벨이 꽉 찬 이진트리를 가리켜 포화 이진 트리라고 한다.

위에서 아래로, 왼쪽에서 오른쪽으로 순서대로 차곡차곡 채워진 이진트리를 가리켜 `완전 이진트리`라고 한다.

 모든 노드가 0개 혹은 2개의 자식 노드만을 갖는 이진 트리를 가리켜 `정 이진트리`라고 한다.

배열로 구성된 `Binary Tree` 는 노드의 개수가 n 개 이고 root 가 0이 아닌 1에서 시작할때, i 번째 노드에 대해서 parent(i) = i/2, left_child(i) = 2i, right_child(i) = 2i+1 의 index 값을 갖는다.



**BST (Binary Search Tree)**

효율적인 탐색을 위해서는 어떻게 찾을까만 고민해서는 안된다. 그보다는 효율적인 탐색을 위한 저장방법이 무엇일까를 고민해야 한다. 이진 탐색 트리는 이진 트리의 일종이다. 단 이진 탐색 트리에는 데이터를 저장하는 규칙이 있다. 그리고 그 규칙은 특정 데이터의 위치를 찾는데 사용할 수 있다.

* 규칙 1. 이진 탐색 트리의 노드에 저장된 키는 유일하다.
* 규칙 2. 부모의 키가 왼쪽 자식 노드의 키보다 크다.
* 규칙 3. 부모의 키가 오른쪽 자식 노드의 키보다 작다
* 규칙 4. 왼쪽과 오른쪽 서브트리도 이진 탐색 트리이다.

이진 탐색 트리의 탐색 연산은 O(log n)의 시간 복잡도를 갖는다. 사실 정확히 말하면 O(h)라고 표현하는 것이 맞다. 트리의 높이를 하나씩 더해갈수록 추가할 수 있는 노드의 수가 두배씩 증가하기 때문이다. 하지만 이러한 이진 탐색 트리는 Skewed Tree(편향 트리)가 될수 있다. 저장 순서에 따라 계속 한쪽으로만 노드가 추가되는 경우가 발생하기 때문이다. 이럴 경우 성능에 영향을 미치게 되며, 탐색의 Worst Case 가 되고 시간 복잡도는 O(n)이 된다.

배열보다 많은 메모리를 사용하며 데이터를 저장했지만 탐색에 필요한 시간 복잡도가 같게 되는 비효율적인 상황이 발생한다. 이를 해결하기 위해 `Rebalancing` 기법이 등장하였다. 균형을 잡기 위한 트리 구조의 재조정을 `Rebalancing` 이라한다. 이 기법을 구현한 트리에는 여러 종류가 존재하는데 그 중에서 하나가 뒤에서 살펴볼 `Red-Black Tree` 이다.



**Personal Recommendation**

* Binary Search Tree 구현하기
* 주어진 트리가 Binary 트리인지 확인하는 알고리즘 구현하기



## Binary Heap

자료구조의 일종으로 Tree 의 형식을 하고 있으며, Tree 중에서도 배열에 기반한 `complete Binary Tree` 이다. 배열에 트리의 값들을 넣어줄때, 0번째는 건너뛰고 1번 index 부터 루트노드가 시작된다. 이는 노드의 고유번호 값과 배열의 index를 일치시켜 혼동을 줄이기 위함이다. `힙(Heap)` 에는 `최대힙(max Heap)`, `최소힙(min heap)` 두 종류가 있다.

`MAX Heap`이란, 각 노드의 값이 해당 children 의 값보다 **크거나 같은**`complete binary tree`를 말한다. (Min Heap 은 그 반대이다.)

`MAX Heap`에서는 Root node 에 있는 값이 제일 크므로, 최대값을 찾는데 소요되는 연산의 time complexity 이 O(1)이다. 그리고 `complete binary tree` 이기 때문에 배열을 사용하여 효율적으로 관리할 수 있다. (즉, random access 가 가능하다. Min heap에서는 최소값을 찾는데 소요되는 연산의 time complexity가 O(1)이다. ) 하지만 heap의 구조를 계속 유지하기 위해서는 제거된 루트 노드를 대체할 다른 노드가 필요하다. 여기서 Heap은 맨 마지막 노드를 루트 노드로 대체시킨후, 다시 heapift 과정을 거쳐 heap 구조를 유지한다. 이런 경우에는 결국 O(log n)의 시간복잡도로 최대값 또는 최소값에 접근할수 있게 된다.

**Personal Recommendation**

* Heapify 구현하기



## Red Black Tree

RBT(Red-Black Tree)는 BST를 기반으로 하는 트리 형식의 자료구조이다. 결론부터 말하자면 Red-Black Tree 에 데이터를 저장하게 되면 Search, Insert, Delete 에 O(log n)의 시간 복잡도가 소요된다. 동일한 노드의 개수일때, depth를 최소화 하여 시간 복잡도를 줄이는 것이 핵심 아이디어이다. 동일한 노드의 개수일 때, depth가 최소가 되는 경우는 tree가 complete binary tree 인 경우이다.

**Red-Black Tree** 의 정의

Red-Black Tree 는 다음의 성질들을 만족하는 BST 이다.

1. 각 노드는 `Red` or `Black` 이라는 색깔을 갖는다.
2. Root node 의 색깔은 `Black` 이다.
3. 각 leaf node 는 `Black`이다.
4. 어떤 노드의 색깔이 `red`라면 두개의 children 의 색깔은 모두 black 이다.
5. 각 노드에 대해서 노드로부터 descendant leaves 까지의 단순 경로는 모두 같은수의 black nodes 들을 포함하고 있다. 이를 해당 노드의 `Black-Height` 라고 한다.