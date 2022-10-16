## 1. Stream 생성하기 전 준비

### 1.1 Stream import 하기

```java
import java.util.stream.Stream;
```

stream()의 결과를 Stream 객체로 받아들이기 위해서는 위와 같은 import가 필요합니다.

### 1.2 배열/컬렉션 생성하기

```java
import java.util.*;

String[] arr = new String[]{"abc", "def", "ghi"};

List<String> list = Arrays.asList("abc", "def", "ghi");
```

스트림을 사용하기 위해서는 배열을 먼저 생성해야 합니다. 스트림은 배열 또는 컬렉션 인스턴스를 사용해서 생성할 수 있습니다. 
<br><br>

## 2. Stream 생성하기

### 2.1 배열을 스트림으로 사용하기

```java
Stream<String> stream = Arrays.stream(arr);
```

### 2.2 원하는 범위 만큼의 배열만 스트림으로 사용하기

```java
Stream<String> partOfStream = Arrays.stream(arr, 1, 3);
// 이 경우에는 ["abc", "def"] 까지만 스트림으로 사용.
```

### 2.3 컬렉션(리스트)을 스트림으로 사용하기

```java
Stream<String> stream2 = list.stream();
```
<br>

## 3. Stream 사용하기

### 3.1 Stream.filter()

```java
List<String> list = Arrays.asList("홍길동", "홍길수", "황길수");

Stream<String> stream = list.stream()
				.filter(name -> name.startsWith("홍"));

stream.forEach(name -> System.out.println(name));

// 출력
// 홍길동
// 홍길수
```

위 코드는 stream의 filter를 사용해서 ‘홍’으로 시작되는 이름들만 골라낸 예제 입니다. 

마무리는 stream의 forEach()를 사용해주면 filter로 걸러진 스트림 객체에 한 번씩 해당 함수(println)를 적용시킬 수 있습니다.

### 3.2 Stream.sorted()

```java
List<Integer> list = Arrays.asList(5, 4, 7, 1, 9, 23);

list.stream().sorted().forEach(x -> System.out.print(x + " "));

// 출력 1 4 5 7 9 23
```

Stream의 sorted()를 이용하면 오름차순 정렬을 할 수 있습니다. 그럼 내림차순의 해당하는 코드는 아래와 같습니다.

```java
List<Integer> list = Arrays.asList(5, 4, 7, 1, 9, 23);

list.stream().sorted(Comparator.reverseOrder()).forEach(x -> System.out.print(x + " "));

// 출력 23 9 7 5 4 1
```

Comparator.reverseOrder()를 sorted()의 인자로 넣어주면 내림차순으로 Stream을 정렬합니다.

### 3.3 Stream.map()과 Stream.collect()

map()은 모든 스트림 객체들에 원하는 함수를 적용시킬 수 있고, collect()는 Collector 타입의 인자를 받아서 스트림을 처리해주는 종료 작업입니다.

상품 번호와 이름을 받는 객체인 Product가 있다고 하고 예제를 시작하겠습니다.

```java
List<Product> productList = 
		Arrays.asList(new Product(12, "orange"),
									new Product(24, "pen"),
									new Product(32, "banana"));
```

위에서 만든 productList를 map()과 collect()를 이용하여 상품의 이름만 갖고 있는 새로운 리스트를 만들어봅니다.

```java
List<String> productNameList = productList.stream()
				.map(Product::getName)
				.collect(Collectors.toList());
// 결과 [orange, pen, banana]
```

### 3.4 Stream.count()

count()를 사용하면 Stream에 해당하는 객체가 몇 개 있는지 셀 수 있습니다. 반환값은 long 타입으로 반환됩니다.

```java
List<String> list = Arrays.asList("abc", "asd", "bbc", "aec");

int count = (int) list.stream().filter(x -> x.contains("a")).count();

System.out.println(count);

// 출력 3
```

위 코드는 list에 저장된 값 중에서 “a”를 포함하고 있는 요소들의 개수를 count()를 사용해서 얻어내는 코드입니다. 

long 타입으로 반환되기 때문에 (int)를 사용해서 int 타입 변수에 넣어줍니다.