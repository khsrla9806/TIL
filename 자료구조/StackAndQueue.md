## 📘 스택과 큐 (Stack / Queue)

### 📖 Stack (스택)

스택 자료구조는 마지막에 들어간 데이터가 제일 먼저 나오는 LIFO(Last In First Out) 구조입니다. 자바에서는 스택을 Stack class로 구현하여 제공하고 있어서 아래와 같이 사용할 수 있습니다.

```java
Stack<Integer> stack = new Stack<>();
```

스택 활용의 간단한 예시로는 홈페이지의 뒤로가기, 앞으로가기 버튼의 기능과 같습니다.

```java
초기 상태 (현재 있는 페이지는 "구글")
BackStack ["네이버", "다음", "구글"]
ForwardStack []

뒤로가기 버튼을 눌렀을 때 (현재 있는 페이지는 "다음")
BackStack ["네이버", "다음"]
ForwardStack ["구글"]

뒤로가기 버튼을 다시 한번 눌렀을 때 (현재 있는 페이지는 "네이버")
BackStack ["네이버"]
ForwardStack ["구글", "다음"]
```

### 📖 Stack Method

1. `empty()`
    
    Stack이 비어있는 상태인지를 알려줍니다. 비어있다면 true를 반환합니다. 주로 while문을 사용하여 스택을 다룰 때 사용합니다.
    
2. `peek()`
    
    Stack의 가장 마지막에 있는 객체를 반환합니다. peek()는 객체를 보여주기만 할 뿐 스택에서 제거하지 않습니다. 만약 Stack이 비어있다면 EmptyStackException을 발생시킵니다.
    
3. `pop()`
    
    peek()와 유사하게 가장 마지막에 있는 객체를 반환합니다. 하지만 pop()의 경우 꺼내서 보여준 객체를 Stack에서 제거합니다.
    
4. `push(Object object)`
    
    Stack에 객체를 저장합니다.
    
5. `search(Object object)`
    
    Stackd에서 객체 object를 찾아서 위치(int)를 반환합니다. 배열과는 다르게 위치는 0이 아닌 1부터 시작합니다. 만약 찾고자하는 객체가 없다면 -1을 반환합니다.
    

### 📖 Queue(큐)

큐 자료구조는 처음에 들어간 데이터가 가장 먼저 나오는 FIFO(First In First Out) 형태의 자료구조 입니다. 자바에서는 Queue를 인터페이스로 정의만 해놓았기 때문에 Queue 인터페이스를 구현한 구현체들 중에서 하나를 골라서 사용해야 합니다.

자주 사용되는 구현체로는 LinkedList와 PriorityQueue가 있습니다. 사용법은 다음과 같습니다.

```java
Queue<Integer> queue1 = new LinkedList<>();
Queue<Integer> queue2 = new PriorityQueue<>();
```

### 📖 Queue Method

1. `add(Object object)`
    
    객체를 Queue에 추가합니다. 추가하는데 성공하면 true를 반환하고, 저장공간이 부족할 경우에는 illegalStateException을 발생시킵니다.
    
2. `peek()`
    
    스택에서와 비슷하게 Queue에서 객체를 읽어서 반환합니다. 이때 Queue에서 객체를 삭제하지는 않습니다. 
    
3. `poll()`
    
    peek()와는 다르게 Queue에서 객체를 꺼내서 반환합니다. 이때 Queue에서 꺼낸 객체는 삭제됩니다. 만약 Queue가 비어있다면 null을 반환합니다.
    
4. `offer(Object object)`
    
    Queue에 객체를 저장합니다. 저장에 성공하면 true, 저장에 실패하면 false를 반환합니다.
    
5. `remove()`
    
    Queue에서 객체를 꺼내서 반환합니다. 만약 비어있다면 NoSuchElementException을 발생시킵니다. 
    
6. `element()`
    
    peek()와 기능이 동일합니다. 하지만 만약 Queue가 비어있을 경우에는 NoSuchElementException을 발생시킵니다.
    

### 📖 PriorityQueue

Queue 인터페이스의 구현체 중 하나입니다. 저장하는 순서에 상관없이 우선순위가 높은 것부터 꺼내는 특징을 가지고 있습니다. null은 저장할 수 없습니다.

PriorityQueue는 가장 큰 값이나 가장 작은 값을 빠르게 찾을 수 있다는 특징을 가지고 있습니다.

예를 들어 보면 데이터를 3, 4, 1, 7, 8 순서대로 저장했을 때, 우선순위로는 숫자가 가장 작은 1이 제일 먼저 나옵니다. 데이터를 하나씩 뽑아서 확인했을 때 1 → 3 → 4 → 7 → 8 순서대로 나오는 것을 확인할 수 있습니다.

### 📖 Deque

Queue와 Stack을 합쳐놓은 형태와 유사한 자료구조이다. 즉, 양쪽에서 추가/삭제가 가능하다. 

1. `offerLast()`
    
    Queue의 offer(), Stack의 push()와 같은 기능을 가집니다. 객체를 Deque에 저장합니다.
    
2. `pollLast()`
    
    마지막 데이터를 꺼내서 가져오기 때문에 Stack의 pop()과 같은 기능을 가집니다. 
    
3. `pollFirst()`
    
    첫 번째로 들어간 데이터를 꺼내서 가져오기 때문에 Queue의 poll()과 같은 기능을 가집니다.
    
4. `peekFirst()`
    
    첫 번째로 들어간 데이터를 반환합니다. 데이터는 사라지지 않기때문에 Queue의 peek()와 같은 기능을 가집니다.
    
5. `peekLast()`
    
    마지막으로 들어간 데이터를 반환합니다. 데이터는 사라지지 않기 때문에 Stack의 peek()와 같은 기능을 가집니다.
