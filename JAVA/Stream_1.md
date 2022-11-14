# 📘 스트림(Stream)

지금까지 많은 수의 데이터를 다룰 때마다 컬렉션 또는 배열을 사용해서 데이터를 담고, for문이나 Iterator를 사용하여 코드를 작성했습니다. 이렇게 작성한 코드는 길이가 길고, 이해하기 어렵다는 문제점을 가지고 있습니다. 그리고 사용하면서도 느꼈겠지만, List의 경우에는 정렬할 때 `Collections.sort()`를 사용하고, Array의 경우에는 정렬할 때 `Arrays.sort()`를 사용한다. 같은 정렬이지만 다른 방법을 사용해야되는 문제점이 있습니다.

이런 문제점을 해결하기 위해서 생긴 것이 스트림(Stream)입니다. 스트림에는 데이터를 다루는데 자주 사용되는 메서드들을 정의해 놓았습니다. 

배열과 리스트를 스트림으로 바꿔서 정렬하고 출력하는 간단한 예시를 한번 들어봅시다.

```java
String[] strArr = {"ddd", "eee", "aaa", "bbb", "ccc"};
List<String> strList = Arrays.asList(strArr);

Stream<String> arrStream = Arrays.stream(strArr);
Stream<String> listStream = strList.stream();

arrStream.sorted().forEach(System.out::println);
listStream.sorted().forEach(System.out::println);
```

마지막 두 줄을 확인해보면 두 데이터의 소스는 서로 다르지만 정렬(sorted)하고 출력(println)하는 방법은 완전히 동일한 것을 확인할 수 있습니다.

## 📖 스트림의 특징

1. 스트림은 데이터 소스를 변경하지 않습니다.
    - 스트림은 데이터 소스로 부터 데이터를 읽기만할 뿐이지 데이터 소스를 변경하지는 않습니다. 필요에 따라서 정렬된 결과를 컬렉션이나 배열에 담아서 반환할 수도 있습니다.
    
    ```java
    String[] strArr = {"ddd", "eee", "aaa", "bbb", "ccc"};
    
    List<String> strList = Arrays.stream(strArr)
    				.sorted()
    				.collect(Collectors.toList());
    ```
    
    이렇게 작성하면 strArr를 스트림에서 정렬한 후 strList라는 리스트 형태로 반환할 수도 있습니다.
    
2. 스트림은 일회용입니다.
    - Iterator 처럼 스트림도 일회용입니다. 스트림은 한번 사용하면 닫혀서 사용할 수 없습니다. 필요하다면 다시 스트림을 생성해야 합니다.
    
    ```java
    String[] strArr = {"ddd", "eee", "aaa", "bbb", "ccc"};
    Stream<String> stream1 = Arrays.stream(strArr);
    
    stream1.forEach(System.out::println);
    long number = stream1.count(); // 컴파일 에러 발생
    ```
    
    ```bash
    Exception in thread "main" java.lang.IllegalStateException: stream has already been operated upon or closed
    	at java.base/java.util.stream.AbstractPipeline.evaluate(AbstractPipeline.java:229)
    	at java.base/java.util.stream.ReferencePipeline.count(ReferencePipeline.java:605)
    	at StreamPractice.main(StreamPractice.java:13)
    ```
    
3. 스트림은 작업을 내부 반복으로 처리합니다.
    - 내부 반복이라는 것은 반복문을 메서드 내부에 숨길 수 있다는 것을 의미합니다. 예를 들어 위에서 계속 예시로 사용했던 `forEach()`라는 메서드는 스트림에 정의된 메서드 중의 하나로서 매개변수에 대입된 람다식을 데이터 소스의 모든 요소에 적용하는 메서드입니다.
    
    ```bash
    String[] strArr = {"ddd", "eee", "aaa", "bbb", "ccc"};
    
    Arrays.stream(strArr).forEach(str -> System.out.println(str));
    Arrays.stream(strArr).forEach(System.out::println);
    ```
    
    마지막 두 줄은 같은 코드이지만 서로 다른 표현 방법입니다. 
    

## 📖 스트림의 연산

스트림에서 제공하는 연산은 중간 연산과 최종 연산으로 분류할 수 있습니다. 

**중간 연산**이란 연산 결과를 스트림으로 반환하기 때문에 중간 연산을 연속해서 연결할 수 있습니다. 

**최종 연산**은 스트림의 요소를 소모하면서 연산을 수행하기 때문에 단 한번만 연산이 가능합니다.

```bash
stream.distinct().limit(5).sorted().forEach(System.out::println);
```

위 코드에서 distinct, limit, sorted는 중간 연산을 의미하고, forEach는 최종 연산을 의미합니다.

**스트림 연산에서 중요한 점은 최종 연산이 수행되기 전까지는 중간 연산이 수행되지 않는다**는 것입니다. 즉, distinct(), sorted() 와 같은 중간 연산은 forEach() 와 같은 최종 연산이 있어야 수행된다는 것을 의미합니다. 

## 📖 스트림 생성하기

스트림의 소스가 될 수 있는 대상은 배열, 컬렉션, 임의의 수 등 다양합니다. 

1. 컬렉션
    - 컬렉션의 최고 위에 있는 Collection에 stream()이 정의되어 있기 때문에 그 아래 구현되어 있는 List, Set을 구현한 컬렉션 클래스들은 모두 스트림으로 생성이 가능합니다.
    - 예를 들어 List를 스트림으로 변환하는 코드는 다음과 같습니다.
    
    ```java
    List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7);
    Stream<Integer> stream = list.stream();
    ```
    
    위 코드에서 모든 요소를 출력하고 싶다면 우리는 최종 연산인 forEach()를 사용해주면 됩니다.
    
    ```java
    stream.forEach(System.out::println);
    ```
    
    하지만 앞서 말했듯이 forEach()의 경우에는 스트림의 요소를 소모하며 작업을 수행하기 때문에 같은 스트림에서 forEach()를 두 번 이상 호출할 수 없습니다.
    
2. 배열
    - 배열을 스트림으로 변환하는 코드는 다음과 같습니다.
    
    ```java
    String[] arr = {"a", "b", "c", "d"};
            
    Stream<String> stream1 = Arrays.stream(arr);
    Stream<String> stream2 = Stream.of(arr);
    Stream<String> stream3 = Stream.of(new String[] {"a", "b", "c", "d"});
    ```
    
    - 배열에서는 int, long, double과 같은 기본형 배열을 소스로 하는 스트림을 생성하는 메서드도 존재합니다. long과 double 모두 동일한 방법으로 선언하기 때문에 int를 예시로 확인하고 넘어가겠습니다.
    
    ```java
    IntStream intStream = IntStream.of(new int[] {1, 2, 3, 4, 5});
    ```
    
3. 특정 범위의 정수
    - IntStream과 LongStream의 경우에는 지정된 범위의 숫자를 스트림으로 만들 수 있는 range()와 rangeClosed() 메서드를 가지고 있습니다.
    
    ```java
    IntStream intStream1 = IntStream.range(1, 5);        // 1, 2, 3, 4
    IntStream intStream2 = IntStream.rangeClosed(1, 5);  // 1, 2, 3, 4, 5
    ```
    
    둘의 차이는 뒤에있는 숫자를 범위에 추가하는가 안 하는가의 차이 입니다. 
    
4. 임의의 수
    - Random 클래스에는 ints(), doubles(), longs()의 메서드가 존재합니다. 해당 타입을 가지는 임의의 난수를 반환합니다.
    - 하지만 사용에 주의해야 할 점은 Random 클래스의 해당 메서드는 ‘무한 스트림’이기 때문에 크기를 항상 지정해줘야 합니다.
    
    ```java
    IntStream randomStream1 = new Random().ints(5);
    randomStream1.forEach(num -> System.out.println(num));
    
    IntStream randomStream2 = new Random().ints();
    randomStream2.limit(5).forEach(num -> System.out.println(num));
    ```
    
    위에 있는 첫 번째 코드 처럼 ints() 내부에 값을 넣어 크기를 지정할 수도 있고, 두 번째 코드 처럼 중간 연산인 limit()를 사용해서 크기를 지정해줄 수 있습니다.
    
    - ints()와 longs()의 범위는 각각 Integer.MIN_VALUE ~ Integer.MAX_VALUE와 long.MIN_VALUE ~ long.MAX_VALUE입니다.
    - doubles()의 경우에는 0.0 ~ 1.0의 범위에서 임의의 난수를 뽑아냅니다.
    - 그리고 아래 코드 처럼 작성해주면 원하는 범위에 있는 숫자들 중에서 임의의 수를 뽑아낼 수 있습니다.
    
    ```java
    IntStream rangeStream = new Random().ints(10,1, 5);
    
    rangeStream.forEach(num -> System.out.println(num));
    ```
    
    사용하는 방법은 다음과 같습니다.
    
    `ints(long streamSize, int begin, int end)` 첫 번째 인자로 몇 개의 수를 뽑을 건지 적어주고, 두 번째 인자로는 시작 범위 숫자, 세 번째 인자로는 끝 범위 숫자를 입력합니다. 여기서 끝 범위 숫자는 포함되지 않습니다. 즉, 위에 작성된 코드는 1에서 4까지의 숫자 중에서 10개의 숫자를 임의로 뽑는 것을 말합니다.
    
5. 빈 스트림
    - 요소가 하나도 없는 비어있는 스트림을 생성할 수도 있다. 스트림에 만약 연산을 수행한 결과가 하나도 없다면 null 보다는 비어있는 스트림을 반환하는 것이 훨씬 낫다.
    
    ```java
    Stream<Long> stream = Stream.empty();
    long count = stream.count();
    System.out.println(count);    // 0
    ```
    
6. 두 스트림을 하나로 연결
    - concat() 메서드를 사용하면 두 스트림을 하나로 연결할 수 있습니다. 여기서 주의할 점은 연결하려는 두 스트림의 타입은 동일해야 합니다.
    
    ```java
    Stream<String> stream1 = Stream.of(new String[] {"가", "나", "다"});
    Stream<String> stream2 = Stream.of(new String[] {"라", "마", "바"});
    Stream<String> concatStream = Stream.concat(stream1, stream2);
    
    concatStream.forEach(str -> System.out.print(str + " "));
    ```
    
    위 출력 결과를 보면 “가 나 다 라 마 바”가 나오는 것을 볼 수 있습니다.
