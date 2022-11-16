# 📘 스트림 (Stream)

이번에는 스트림의 중간 연산과 최종 연산에 대해서 알아보려고 합니다. 

## 📖 스트림의 중간연산

1. 스트림 자르기 - skip(), limit()
    - 스트림의 일부를 잘라낼 때 사용하는 연산입니다.
    - `skip()` : 처음 지정한 숫자의 개수만큼 요소를 건너뜁니다,
        
        ```java
        IntStream intStream = IntStream.rangeClosed(1, 10);
        intStream.skip(5).forEach(num -> System.out.println(num)); // 6, 7, 8, 9, 10
        ```
        
        skip(5)는 앞에 5개 만큼을 뛰어 넘어서 다음 요소들을 모두 출력합니다.
        
    - `limit()` : 스트림의 크기를 지정할 수 있습니다.
        
        ```java
        IntStream intStream = IntStream.rangeClosed(1, 20);
        intStream.limit(5).forEach(num -> System.out.println(num));
        ```
        
    - 응용하면 이런 코드를 작성할 수 있습니다. 예를 들어 1부터 20까지의 숫자 중에서 5, 6, 7, 8, 9 요소만 얻고 싶다면 다음과 같은 코드를 작성해야 합니다.
        
        ```java
        IntStream intStream = IntStream.rangeClosed(1, 20);
        intStream.skip(4).limit(5).forEach(num -> System.out.println(num));
        ```
        
2. 스트림의 요소 걸러내기 - filter(), distinct()
    - `distinct()` : 스트림에서 중복된 요소들을 제거할 수 있습니다.
        
        ```java
        Stream<String> name = Stream.of(new String[] {"김씨", "김씨", "박씨"});
        name.distinct().forEach(str -> System.out.println(str)); // 김씨 박씨
        ```
        
        distinct()를 사용하고 난후 결과를 확인해보면 중복된 요소인 “김씨”가 하나 제거된 것을 확인할 수 있습니다.
        
    - `filter()` : 주어진 조건에 맞지 않는 요소들을 걸러낼 수 있습니다.
        
        ```java
        Stream<String> name = Stream.of(new String[] {"김씨", "김씨", "박씨"});
        name.filter(str -> str.startsWith("박")).forEach(str -> System.out.println(str));
        ```
        
        위 코드를 확인해보면 “박”으로 시작하는 요소가 아니면 모두 filter()를 통해서 걸러낼 수 있습니다. 결과는 “박씨”만 나오는 것을 확인할 수 있습니다.
        
3. 스트림의 요소 정렬하기 - sorted()
    - `sorted()` : 스트림을 정렬할 수 있습니다.
        
        ```java
        Stream<Integer> stream = Stream.of(1, 9, 7, 10, 8, 2);
        stream.sorted().forEach(num -> System.out.println(num));
        ```
        
        정렬된 값을 얻어서 출력할 수 있습니다.
        
    - 람다식을 사용한 정렬도 가능합니다.
        - 오름차순 정렬
            
            ```java
            Stream<Integer> stream = Stream.of(1, 9, 7, 10, 8, 2);
            stream.sorted((num1, num2) -> num1.compareTo(num2)).forEach(num -> System.out.println(num));
            ```
            
            기본 정렬과 똑같은 결과 입니다.
            
        - 내림차순 정렬
            
            ```java
            Stream<Integer> stream = Stream.of(1, 9, 7, 10, 8, 2);
            stream.sorted((num1, num2) -> num2.compareTo(num1)).forEach(num -> System.out.println(num));
            ```
            
            ```java
            Stream<Integer> stream = Stream.of(1, 9, 7, 10, 8, 2);
            stream.sorted(Comparator.reverseOrder()).forEach(num -> System.out.println(num));
            ```
            
            Comparator의 static 메서드인 reverseOrder를 사용해서 내림차순 정렬을 진행한 결과 입니다.
            
    - 만약 정렬의 조건이 여러 개가 있을 때의 예시를 하나 들어봅시다.
        - 학생을 정렬하는 예제입니다. ban으로 먼저 오름차순 정렬을 한 후, score로 내림차순 정렬을 진행합니다.
        
        ```java
        import java.util.Comparator;
        import java.util.stream.Stream;
        
        public class StreamEx {
            public static void main(String[] args) {
                Stream<Student> stream = Stream.of(
                        new Student("홍자바", 1, 200),
                        new Student("김자바", 2, 150),
                        new Student("빅자바", 2, 180),
                        new Student("이자바", 1, 330),
                        new Student("유자바", 3, 210),
                        new Student("정자바", 3, 280),
                        new Student("우자바", 2, 320),
                        new Student("지자바", 1, 190));
        
                stream.sorted(Comparator.comparing(Student::getBan) // ban으로 오름차순 정렬
                        .thenComparing(Comparator.naturalOrder())) // 정의한 기본정렬 사용 (score)
                        .forEach(student -> System.out.println(student));
            }
        }
        
        class Student implements Comparable<Student> {
            String name;
            int ban;
            int score;
        
            Student(String name, int ban, int score) {
                this.name = name;
                this.ban = ban;
                this.score = score;
            }
        
            public int getBan() {
                return ban;
            }
        
            public String toString() {
                return String.format("[ %s, %d, %d ]", name, ban, score);
            }
        
            @Override
            public int compareTo(Student s) {
                return s.score - this.score; // 점수 내림차순 정렬 기본
            }
        }
        ```
        
        ```bash
        // 출력 결과 //
        [ 이자바, 1, 330 ]
        [ 홍자바, 1, 200 ]
        [ 지자바, 1, 190 ]
        [ 우자바, 2, 320 ]
        [ 빅자바, 2, 180 ]
        [ 김자바, 2, 150 ]
        [ 정자바, 3, 280 ]
        [ 유자바, 3, 210 ]
        ```
        
        위 코드를 살펴 보겠습니다.
        
        - Student 클래스에서 Comparable을 implements해서 상속을 진행한 후 compareTo를 오버라이드 해서 정의했습니다. 여기서 Student의 기본 정렬은 score를 가지고 내림차순으로 정렬합니다.
        - StreamEx 부분 코드를 보면 8명의 학생 객체를 만들어 스트림에 넣고, 다음과 같이 작성했습니다
        
        ```java
        stream.sorted(Comparator.comparing(Student::getBan)
        				.thenComparing(Comparator.naturalOrder()))
        				.forEach(System.out::println);
        ```
        
        - sorted에서 첫 번째로 Comparator.comparing(Student::getBan)을 통해서 ban을 기준으로 오름차순 정렬을 진행합니다.
        - 그 다음으로 thenComparing(Comparator.naturalOrder())를 통해서 Student의 compareTo()로 설정해둔 기본정렬인 score을 내림차순으로 정렬합니다.
        - 즉, 반(ban)은 오름차순으로 정렬되고, 점수(score)로는 내림차순 정렬을 진행합니다. 반약 반(ban)도 내림 차순으로 정렬하고 싶다면 어떻게 해야될까?
        
        ```java
        stream.sorted(Comparator.comparing(Student::getBan, Comparator.reverseOrder())
        				.thenComparing(Coparator.naturalOrder()))
        				.forEach(System.out::println);
        ```
        
        - Comparator.reverseOrder() 조건을 주면 반(ban)도 내림차순으로 정렬할 수 있습니다.
        - 정말 활용도가 높을 거 같은 예제입니다.
4. 스트림의 요소를 변환 - map()
    - 스트림의 요소에 저장된 값 중에서 원하는 필드만 뽑아내거나, 특정 형태로 변환해야 하는 상황이 발생될 때 사용합니다.
    - `map()` : 특정 요소에 원하는 함수를 모두 적용시킬 수 있습니다.
    - 예를 들어 {”김자바”, “박자바”, “홍자바”, “박스프링”}에서 성만 잘르고, 중복되는 성은 제거해서 {”김”, “박”, “홍”}라는 데이터를 얻고 싶다면 다음과 같이 코드를 작성하면 된다.
    
    ```java
    Stream<String> nameStream = Stream.of("김자바", "박자바", "홍자바", "박스프링");
    
    nameStream.map(name -> name.substring(0, 1))
            .distinct()
            .forEach(System.out::println);
    ```
    
    - map()을 사용해서 모든 데이터에 substring()을 적용해서 성씨만 잘라냅니다.
    - distinct() 사용해서 중복되는 데이터를 제거합니다.
5. 스트림의 요소를 조회 - peek()
    - 스트림 연산을 진행하는 중간에 만약 데이터를 출력해서 보고 싶다면 어떻게 해야할까. forEach()를 쓰면 최종 연산이기 때문에 스트림을 소모하게 된다. 이때 사용할 수 있는 것이 peek()이다.
    
    ```java
    Stream<String> nameStream = Stream.of("김자바", "박자바", "홍자바", "박스프링");
    
            nameStream.map(name -> name.substring(0, 1))
                    .peek(name -> System.out.print("\"" + name + "\""))
                    .distinct()
                    .peek(name -> System.out.println("은 사라지지 않았습니다."))
                    .collect(Collectors.toList());
    ```
    
    ```bash
    "김"은 사라지지 않았습니다.
    "박"은 사라지지 않았습니다.
    "홍"은 사라지지 않았습니다.
    "박"
    ```
    
    출력 결과를 보면 마지막 “박”은 distinct()를 통해서 사라져서 뒷 문구가 출력되지 않은 것을 확인할 수 있습니다.
    
6. Stream<T[]>를 Stream<T>로 변환 - flatMap()
    - 배열이 인자인 스트림을 기본 타입으로 바꾸어 작업을 해야되는 경우가 있을 수도 있다. 이때는 `flatMap()`을 사용하면 된다.
    - 예를 하나 들어보자.
    
    ```java
    Stream<String[]> streamArr = Stream.of(
                    new String[] {"김자바", "홍자바"},
                    new String[] {"박자바", "정자바"}
    );
    
    List<String> nameList = streamArr.flatMap(Arrays::stream)
          .collect(Collectors.toList());
    
    System.out.println(nameList.toString());
    
    // 출력 : [김자바, 홍자바, 박자바, 정자바]
    ```
    
    위 코드를 살펴보면 배열 요소에 있는 것들이 하나의 리스트에 저장된 것을 확인할 수 있다. 이렇게 스트림에 배열로 된 요소들이 있을 때, 각 타입의 요소로 분리해서 하나의 스트림으로 만들 수 있는 기능이 flatMap()이다. 
    

## 📖 스트림의 최종연산

최종연산은 스트림의 요소를 소모해서 결과를 만들어낸다. 그래서 최종 연산 후에는 스트림이 닫히고, 더는 사용할 수 없게 된다.

1. `forEach()`
    - 반환 타입이 void 이기 때문에 요소를 출력하는 용도로 많이 사용된다.
    - 앞서 많이 사용했지만 예시를 하나 들어보면 다음과 같다.
    
    ```java
    Stream.of("김자바", "박자바", "정자바")
                    .forEach(name -> System.out.print(name + " "));
    
    // 출력 : 김자바 박자바 정자바
    ```
    
    다음과 같이 스트림의 요소들을 출력할 수 있습니다.
    
2. 조건 검사 - allMatch(), anyMatch(), noneMatch(), findFirst(), findAny()
    - 스트림 요소에 대해서 정해진 조건에 모두 일치하는지, 일부만 일치하는지, 어떠한 요소도 일치하지 않는지 확인할 수 있는 용도로 사용합니다. 이 연산들은 결과로 boolean 값을 반환합니다.
    - `allMatch()` : 해당 조건에 모든 요소가 참의 값을 갖는지 검사합니다.
        
        ```java
        boolean containsJava = Stream.of("김자바", "박자바", "정자바")
                        .allMatch(name -> name.contains("자바"));
        
        System.out.println(containsJava);  // true
        ```
        
        모든 요소가 이름에 “자바”를 포함하고 있는지 검사하는 코드입니다.
        
    - `anyMatch()` : 해당 조건에 어느 하나의 요소라도 참의 값을 갖는지 검사합니다.
        
        ```java
        boolean containsJava = Stream.of("김파이썬", "박씨", "정자바")
                        .anyMatch(name -> name.contains("자바"));
        
        			System.out.println(containsJava);  // true
        ```
        
        어느 요소 하나라도 “자바”를 포함하고 있는지 검사하는 코드입니다.
        
    - `noneMatch()` : 해당 조건에 참의 값을 갖는 요소가 하나도 없는지 검사합니다.
        
        ```java
        boolean containsJava = Stream.of("김파이썬", "박씨", "정코딩")
                        .noneMatch(name -> name.contains("자바"));
        
        System.out.println(containsJava);  // true
        ```
        
    - `findFirst()` : filter와 자주 사용됩니다. 해당 조건에 해당하는 요소 중 젤 앞에 있는 요소를 반환합니다. 반환되는 타입은 Optional<T> 입니다.
        
        ```java
        Optional<String> findName = Stream.of("김자바", "박자바", "정자바")
                        .filter(name -> name.contains("자바"))
                        .findFirst();
        
        System.out.println(findName.get());  // 김자바
        ```
        
        병렬 스트림인 경우에는 findFirst() 대신 findAny()를 사용해야 한다.
        
        !! 비어있는 Optional 객체는 내부적으로 null을 저장하고 있습니다. 
        
3. 통계 - count(), sum(), average(), max(), min()
    - IntStream과 같이 기본형 스트림에는 sum(), average()와 같은 최종 연산 메서드가 존재합니다.
        
        ```java
        IntStream intStream = IntStream.of(1, 2, 3, 4, 5);
        int sum = intStream.sum();
        System.out.println(sum);  // 15
        ```
        
        ```java
        IntStream intStream = IntStream.of(1, 2, 3, 4, 5);
        OptionalDouble average = intStream.average();
        System.out.println(average.getAsDouble());  // 3.0
        ```
        
    - 기본 스트림의 경우에는 count(), min(), max()에 대한 통계 연산만을 제공합니다.
        
        ```java
        Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5);
        long count = stream.count();
        System.out.println(count);  // 5
        ```
        
        ```java
        Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5);
        Optional<Integer> max = stream.max(Comparator.naturalOrder());
        System.out.println(max.get());  // 5
        ```
        
        ```java
        Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5);
        Optional<Integer> min = stream.min(Comparator.naturalOrder());
        System.out.println(min.get());  // 1
        ```
        
        대부분의 경우 앞으로 배워볼 reduce()와 collect()를 사용해서 통계 정보를 얻습니다.
        
4. 리듀싱 - reduce()
    - 스트림의 요소를 줄여나가면서 연산을 수행하고 최종결과를 반환합니다. 처음 두 요소를 가지고 연산한 결과를 가지고 그 다음 요소를 연산합니다. 이 과정에서 스트림에서 요소를 하나씩 소모하게 되고, 스트림의 모든 요소를 소모하면 그 결과를 반환합니다.
    - max의 결과를 얻을 수 있는 코드를 작성해보겠습니다.
        
        ```java
        IntStream stream = IntStream.of(1, 2, 3, 4, 5);
        int max = stream.reduce(Integer.MIN_VALUE, (a,b) -> a>b ? a:b);
        System.out.println(max);
        ```
        
        아래와 같이도 작성할 수 있습니다.
        
        ```java
        IntStream stream = IntStream.of(1, 2, 3, 4, 5);
        OptionalInt max = stream.reduce(Integer::max);
        System.out.println(max.getAsInt());
        ```
        
    - sum의 결과를 얻을 수 있는 코드를 작성해봅니다.
        
        ```java
        IntStream stream = IntStream.of(1, 2, 3, 4, 5);
        int sum = stream.reduce(0, (a,b) -> a + b);
        System.out.println(sum);
        ```
        
        초기 값인 0을 a에 저장하고, 스트림의 다음 요소인 b를 하나씩 꺼내면서 a에 누적해나가는 원리를 이용한 것입니다.
        
    - count의 결과를 얻을 수 있는 코드를 작성해봅니다.
        
        ```java
        Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5);
        int count = stream.reduce(0, (a,b) -> a + 1);
        System.out.println(count);
        ```
        

## 📖 collect()

collect()가 스트림의 요소를 수집하기 위해서는 어떻게 수집할 것인가에 대한 방법이 정의되어 있어야 한다. 이 방법을 정의한 것이 바로 **컬렉터(collector)**이다. 

컬렉터는 Collector 인터페이스로 구현한 것이고, 직접 구현할 수도 있고 미리 작성된 것을 사용할 수도 있습니다. Collector 클래스에는 다양한 종류의 컬렉터를 반환하는 static 메서드가 이미 정의되어 있고, 기본적으로 제공되는 컬렉터만으로도 많은 일들을 할 수 있습니다.

<aside>
💡 **collect()** 스트림의 최종연산, 매개변수로 Collector를 필요로 합니다. 
**Collector** 인터페이스이고, 컬렉터는 이 인터페이스를 구현해야 합니다.
**Collectors** 클래스이고, static 메서드로 미리 작성된 컬렌터를 제공합니다.

</aside>

## 📖 스트림을 컬렉션과 배열로 변환

Collectors 클래스에는 toList(), toSet(), toMap(), toCollection(), toArray() 메서드를 사용하면 스트림을 컬렉션과 배열로 변환할 수 있습니다.

만약 List, Set이 아닌 ArrayList와 같은 특정 컬렉션을 지정하기 위해서는 toCollection()에 해당 컬렉션의 생성자 참조를 매개변수로 넣어주면 됩니다. 아래 코드에서 확인해보겠습니다.

```java
List<String> name = List.of("김자바", "박자바", "홍자바");

ArrayList<String> name2 = name.stream()
				.collect(Collectors.toCollection(ArrayList::new));
```

위에서 보면 name이라는 List를 toCollection(ArrayList::new)를 사용해서 ArrayList로 변환한 것을 볼 수 있습니다.

1. `toMap()`
    - Map은 키와 값의 쌍으로 저장해야하기 때문에 객체의 어떤 필드를 키로 사용할지와 값으로 사용할지를 지정해줘야 한다.
    
    ```java
    public class StreamPractice {
        public static void main(String[] args) {
            Stream<Person> personStream = Stream.of(
                    new Person("김자바", 20),
                    new Person("박자바", 25),
                    new Person("홍자바", 26)
            );
    
            Map<String, Integer> map = personStream
                    .collect(Collectors.toMap(p -> p.getName(), p -> p.getAge()));
    
            System.out.println(map.toString());
        }
    }
    
    class Person {
        String name;
        int age;
    
        Person(String name, int age) {
            this.name = name;
            this.age = age;
        }
    
        public String getName() {
            return name;
        }
    
        public int getAge() {
            return age;
        }
    }
    ```
    
    ```bash
    {김자바=20, 박자바=25, 홍자바=26}
    ```
    
    toMap()에서는 키와 값을 모두 넘겨줘야 한다. 위 예제에서는 Person 클래스의 이름(name)을 key로 쓰고, 나이(age)를 value로 사용하는 코드입니다.
    
2. `toArray()`
    - 스트림에 저장된 요소를 T[] 타입의 배열로 변환하려면 toArray()를 사용하면 됩니다.
    - 주의해야할 점은 toArray()에 생성자 참조를 매개변수로 지정해줘야 하는데, 만약 매개변수로 지정해주지 않는다면 반환되는 타입은 Object[] 입니다.
    
    ```java
    Student[] studentNames = studentStream.toArray(Student[]::new);
    Student[] studentNames = studentStream.toArray(); // ERROR 발생
    Object[] studentNames = studentStream.toArray();
    ```
