## 1. ArrayList의 특징

- ArrayList는 객체가 추가되어 용량을 초과하면 자동으로 부족한 크기만큼 용량이 늘어난다.
- 표준 배열보다는 느리지만 배열에서 많은 조작이 필요한 경우 유용하게 사용이 가능하다.
<br><br>

## 2. ArrayList 선언하기

### 2.1 타입을 설정하지 않고 설정하는 경우

```java
ArrayList list = new ArrayList();
```

### 2.2 타입을 설정하여 선언하는 경우

```java
ArrayList<String> list = new ArrayList<String>();
```

### 2.3 초기 용량을 세팅하여 선언하는 경우

```java
ArrayList<Integer> list = new ArrayList<Integer>(10);
```

### 2.4 초기값을 세팅하여 선언하는 경우

```java
ArrayList<Integer> list = new ArrayList<Integer>(Arrays.asList(1, 2, 3, 4);
```

`Arrays.asList(배열)`

입력되는 배열을 ArrayList 타입으로 변경시켜줄 수 있는 메서드 입니다.
<br><br>

## 3. ArrayList의 메서드

### 3.1 값 추가하기

`add(Object)`

ArrayList의 마지막에 데이터를 추가할 수 있습니다.

`add(int index, Object)`

ArrayList의 원하는 index에 데이터를 추가할 수 있습니다.

### 3.2 값 변경하기

`set(int index, Object)`

원하는 index에 있는 값을 변경할 수 있습니다. 

### 3.3 값 삭제하기

`remove(Object)`

ArrayList에서 Object와 같은 값을 가지는 데이터를 삭제합니다. 

만약 같은 값이 두 개 있는 경우 첫 번째 같은 값을 삭제합니다.

`remove(int index)`

해당 index를 가지는 데이터를 삭제합니다.

`clear()`

ArrayList에 있는 모든 데이터를 삭제합니다.

### 3.4 크기 구하기

`size()`

ArrayList의 크기를 구할 수 있습니다.

### 3.5 값 출력하기

`get(int index)`

해당 index를 가지는 값을 얻어올 수 있습니다.

### 3.6 iterator 사용하여 출력하기

```java
ArrayList<String> list = new ArrayList<String>();

Iterator iter = list.iterator();

while(iter.hasNext()) {
		System.out.println(iter.next());
}
```

`iterator()`

ArrayList를 Iterator 타입으로 만들 수 있습니다.

`Iterator.hasNext()`

다음 내용이 존재하면 true를 반환합니다. 

`Iterator.next()`

다음 내용을 얻어옵니다. get() 메서드와 비슷하다고 생각하면 됩니다.

### 3.7 값 검색하기

`contains(Object)`

해당 값을 가지는 데이터가 존재하는지 여부를 나타냅니다. 있다면 true를 반환합니다. 

`indexOf(Object)`

해당 값을 가지는 데이터의 index를 찾아서 반환하고, 만약 데이터가 없다면 -1을 출력합니다.