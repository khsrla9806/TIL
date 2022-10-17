## 1. Set의 특징

- 객체(데이터)를 중복해서 저장할 수 없다.
- 데이터를 인덱스로 관리하지 않아서 저장 순서가 보장되지 않는다.
<br><br>
## 2. HashSet

### 2.1 HashSet의 특징

- HashSet는 Set을 구현하는 대표적인 클래스이다.
- 데이터를 중복 저장할 수 없고 순서를 보장하지 않는다.

### 2.2 HashSet 사용

```java
import java.util.HashSet;
import java.util.Set;
```

```java
Set<String> set = new HashSet<String>();
set.add("one");
set.add("two");
set.add("three");
set.add("one");

// set-> "one", "two", "three"
```

위 처럼 add() 메서드를 사용해서 데이터를 Set에 입력하면 중복을 제거하기 때문에 “one”은 하나만 들어가게 됩니다. 

### 2.3 HashSet 메서드

`Set.add(Object)`

데이터를 Set에 넣을 수 있습니다. 단 입력되는 데이터는 중복을 허용하지 않습니다. 

```java
Set<String> set = new HashSet<String>();
set.add("김씨");
set.add("이씨");
set.add("박씨");
set.add("정씨");
```

`Set.iterator()`

Set을 반복자(Iterator) 객체로 만들 수 있습니다. Iterator 객체로 만들면 hasNext()와 next() 메서드를 사용할 수 있습니다. 

```java
import java.util.Iterator;

Iterator iter = set.iterator();

while(iter.hasNext()) {
		System.out.print(iter.next() + " ");
}

// 출력
// 김씨 이씨 박씨 정씨
```

`Set.size()`

Set의 크기를 얻을 수 있습니다. Set에 저장된 데이터의 개수를 return 값으로 반환합니다. 

```java
System.out.print(set.size()); // 출력 4
```
<br>

## 3. TreeSet

### 3.1 TreeSet의 특징

- HashSet과 동일하게 데이터를 중복하여 저장할 수 없고, 데이터의 순서도 없습니다.
- TreeSet은 기본적으로 데이터를 오름차순으로 정렬합니다.

### 3.2 TreeSet 사용

```java
import java.util.*;

Set<Integer> set = new TreeSet<Integer>();
set.add(4);
set.add(1);
set.add(3);
set.add(2);
set.add(5);

// set = {1, 2, 3, 4, 5}
```

위 처럼 순서 없이 데이터를 입력해도 TreeSet의 경우에는 오름차순으로 자동 정렬하여 데이터를 관리합니다.
<br><br>

## 4. LinkedHashSet

### 4.1 LinkedHashSet의 특징

- 동일한 데이터를 중복하여 저장할 수 없습니다.
- 데이터를 입력한 순서대로 관리합니다.

### 4.2 LinkedHashSet 사용

```java
import java.util.*;

Set<String> set = new LinkedHashSet<String>();
set.add("홍길동");
set.add("강남");
set.add("강호동");

// set = {"홍길동", "강남", "강호동"}
```

위 코드를 보면 등록한 순서대로 홍길동, 강남, 강호동의 데이터가 저장되고 순서를 가지고 데이터가 관리된다.