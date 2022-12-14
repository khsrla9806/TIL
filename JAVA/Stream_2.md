# πΒ μ€νΈλ¦Ό (Stream)

μ΄λ²μλ μ€νΈλ¦Όμ μ€κ° μ°μ°κ³Ό μ΅μ’ μ°μ°μ λν΄μ μμλ³΄λ €κ³  ν©λλ€. 

## πΒ μ€νΈλ¦Όμ μ€κ°μ°μ°

1. μ€νΈλ¦Ό μλ₯΄κΈ° - skip(), limit()
    - μ€νΈλ¦Όμ μΌλΆλ₯Ό μλΌλΌ λ μ¬μ©νλ μ°μ°μλλ€.
    - `skip()` : μ²μ μ§μ ν μ«μμ κ°μλ§νΌ μμλ₯Ό κ±΄λλλλ€,
        
        ```java
        IntStream intStream = IntStream.rangeClosed(1, 10);
        intStream.skip(5).forEach(num -> System.out.println(num)); // 6, 7, 8, 9, 10
        ```
        
        skip(5)λ μμ 5κ° λ§νΌμ λ°μ΄ λμ΄μ λ€μ μμλ€μ λͺ¨λ μΆλ ₯ν©λλ€.
        
    - `limit()` : μ€νΈλ¦Όμ ν¬κΈ°λ₯Ό μ§μ ν  μ μμ΅λλ€.
        
        ```java
        IntStream intStream = IntStream.rangeClosed(1, 20);
        intStream.limit(5).forEach(num -> System.out.println(num));
        ```
        
    - μμ©νλ©΄ μ΄λ° μ½λλ₯Ό μμ±ν  μ μμ΅λλ€. μλ₯Ό λ€μ΄ 1λΆν° 20κΉμ§μ μ«μ μ€μμ 5, 6, 7, 8, 9 μμλ§ μ»κ³  μΆλ€λ©΄ λ€μκ³Ό κ°μ μ½λλ₯Ό μμ±ν΄μΌ ν©λλ€.
        
        ```java
        IntStream intStream = IntStream.rangeClosed(1, 20);
        intStream.skip(4).limit(5).forEach(num -> System.out.println(num));
        ```
        
2. μ€νΈλ¦Όμ μμ κ±Έλ¬λ΄κΈ° - filter(), distinct()
    - `distinct()` : μ€νΈλ¦Όμμ μ€λ³΅λ μμλ€μ μ κ±°ν  μ μμ΅λλ€.
        
        ```java
        Stream<String> name = Stream.of(new String[] {"κΉμ¨", "κΉμ¨", "λ°μ¨"});
        name.distinct().forEach(str -> System.out.println(str)); // κΉμ¨ λ°μ¨
        ```
        
        distinct()λ₯Ό μ¬μ©νκ³  λν κ²°κ³Όλ₯Ό νμΈν΄λ³΄λ©΄ μ€λ³΅λ μμμΈ βκΉμ¨βκ° νλ μ κ±°λ κ²μ νμΈν  μ μμ΅λλ€.
        
    - `filter()` : μ£Όμ΄μ§ μ‘°κ±΄μ λ§μ§ μλ μμλ€μ κ±Έλ¬λΌ μ μμ΅λλ€.
        
        ```java
        Stream<String> name = Stream.of(new String[] {"κΉμ¨", "κΉμ¨", "λ°μ¨"});
        name.filter(str -> str.startsWith("λ°")).forEach(str -> System.out.println(str));
        ```
        
        μ μ½λλ₯Ό νμΈν΄λ³΄λ©΄ βλ°βμΌλ‘ μμνλ μμκ° μλλ©΄ λͺ¨λ filter()λ₯Ό ν΅ν΄μ κ±Έλ¬λΌ μ μμ΅λλ€. κ²°κ³Όλ βλ°μ¨βλ§ λμ€λ κ²μ νμΈν  μ μμ΅λλ€.
        
3. μ€νΈλ¦Όμ μμ μ λ ¬νκΈ° - sorted()
    - `sorted()` : μ€νΈλ¦Όμ μ λ ¬ν  μ μμ΅λλ€.
        
        ```java
        Stream<Integer> stream = Stream.of(1, 9, 7, 10, 8, 2);
        stream.sorted().forEach(num -> System.out.println(num));
        ```
        
        μ λ ¬λ κ°μ μ»μ΄μ μΆλ ₯ν  μ μμ΅λλ€.
        
    - λλ€μμ μ¬μ©ν μ λ ¬λ κ°λ₯ν©λλ€.
        - μ€λ¦μ°¨μ μ λ ¬
            
            ```java
            Stream<Integer> stream = Stream.of(1, 9, 7, 10, 8, 2);
            stream.sorted((num1, num2) -> num1.compareTo(num2)).forEach(num -> System.out.println(num));
            ```
            
            κΈ°λ³Έ μ λ ¬κ³Ό λκ°μ κ²°κ³Ό μλλ€.
            
        - λ΄λ¦Όμ°¨μ μ λ ¬
            
            ```java
            Stream<Integer> stream = Stream.of(1, 9, 7, 10, 8, 2);
            stream.sorted((num1, num2) -> num2.compareTo(num1)).forEach(num -> System.out.println(num));
            ```
            
            ```java
            Stream<Integer> stream = Stream.of(1, 9, 7, 10, 8, 2);
            stream.sorted(Comparator.reverseOrder()).forEach(num -> System.out.println(num));
            ```
            
            Comparatorμ static λ©μλμΈ reverseOrderλ₯Ό μ¬μ©ν΄μ λ΄λ¦Όμ°¨μ μ λ ¬μ μ§νν κ²°κ³Ό μλλ€.
            
    - λ§μ½ μ λ ¬μ μ‘°κ±΄μ΄ μ¬λ¬ κ°κ° μμ λμ μμλ₯Ό νλ λ€μ΄λ΄μλ€.
        - νμμ μ λ ¬νλ μμ μλλ€. banμΌλ‘ λ¨Όμ  μ€λ¦μ°¨μ μ λ ¬μ ν ν, scoreλ‘ λ΄λ¦Όμ°¨μ μ λ ¬μ μ§νν©λλ€.
        
        ```java
        import java.util.Comparator;
        import java.util.stream.Stream;
        
        public class StreamEx {
            public static void main(String[] args) {
                Stream<Student> stream = Stream.of(
                        new Student("νμλ°", 1, 200),
                        new Student("κΉμλ°", 2, 150),
                        new Student("λΉμλ°", 2, 180),
                        new Student("μ΄μλ°", 1, 330),
                        new Student("μ μλ°", 3, 210),
                        new Student("μ μλ°", 3, 280),
                        new Student("μ°μλ°", 2, 320),
                        new Student("μ§μλ°", 1, 190));
        
                stream.sorted(Comparator.comparing(Student::getBan) // banμΌλ‘ μ€λ¦μ°¨μ μ λ ¬
                        .thenComparing(Comparator.naturalOrder())) // μ μν κΈ°λ³Έμ λ ¬ μ¬μ© (score)
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
                return s.score - this.score; // μ μ λ΄λ¦Όμ°¨μ μ λ ¬ κΈ°λ³Έ
            }
        }
        ```
        
        ```bash
        // μΆλ ₯ κ²°κ³Ό //
        [ μ΄μλ°, 1, 330 ]
        [ νμλ°, 1, 200 ]
        [ μ§μλ°, 1, 190 ]
        [ μ°μλ°, 2, 320 ]
        [ λΉμλ°, 2, 180 ]
        [ κΉμλ°, 2, 150 ]
        [ μ μλ°, 3, 280 ]
        [ μ μλ°, 3, 210 ]
        ```
        
        μ μ½λλ₯Ό μ΄ν΄ λ³΄κ² μ΅λλ€.
        
        - Student ν΄λμ€μμ Comparableμ implementsν΄μ μμμ μ§νν ν compareToλ₯Ό μ€λ²λΌμ΄λ ν΄μ μ μνμ΅λλ€. μ¬κΈ°μ Studentμ κΈ°λ³Έ μ λ ¬μ scoreλ₯Ό κ°μ§κ³  λ΄λ¦Όμ°¨μμΌλ‘ μ λ ¬ν©λλ€.
        - StreamEx λΆλΆ μ½λλ₯Ό λ³΄λ©΄ 8λͺμ νμ κ°μ²΄λ₯Ό λ§λ€μ΄ μ€νΈλ¦Όμ λ£κ³ , λ€μκ³Ό κ°μ΄ μμ±νμ΅λλ€
        
        ```java
        stream.sorted(Comparator.comparing(Student::getBan)
        				.thenComparing(Comparator.naturalOrder()))
        				.forEach(System.out::println);
        ```
        
        - sortedμμ μ²« λ²μ§Έλ‘ Comparator.comparing(Student::getBan)μ ν΅ν΄μ banμ κΈ°μ€μΌλ‘ μ€λ¦μ°¨μ μ λ ¬μ μ§νν©λλ€.
        - κ·Έ λ€μμΌλ‘ thenComparing(Comparator.naturalOrder())λ₯Ό ν΅ν΄μ Studentμ compareTo()λ‘ μ€μ ν΄λ κΈ°λ³Έμ λ ¬μΈ scoreμ λ΄λ¦Όμ°¨μμΌλ‘ μ λ ¬ν©λλ€.
        - μ¦, λ°(ban)μ μ€λ¦μ°¨μμΌλ‘ μ λ ¬λκ³ , μ μ(score)λ‘λ λ΄λ¦Όμ°¨μ μ λ ¬μ μ§νν©λλ€. λ°μ½ λ°(ban)λ λ΄λ¦Ό μ°¨μμΌλ‘ μ λ ¬νκ³  μΆλ€λ©΄ μ΄λ»κ² ν΄μΌλ κΉ?
        
        ```java
        stream.sorted(Comparator.comparing(Student::getBan, Comparator.reverseOrder())
        				.thenComparing(Coparator.naturalOrder()))
        				.forEach(System.out::println);
        ```
        
        - Comparator.reverseOrder() μ‘°κ±΄μ μ£Όλ©΄ λ°(ban)λ λ΄λ¦Όμ°¨μμΌλ‘ μ λ ¬ν  μ μμ΅λλ€.
        - μ λ§ νμ©λκ° λμ κ±° κ°μ μμ μλλ€.
4. μ€νΈλ¦Όμ μμλ₯Ό λ³ν - map()
    - μ€νΈλ¦Όμ μμμ μ μ₯λ κ° μ€μμ μνλ νλλ§ λ½μλ΄κ±°λ, νΉμ  ννλ‘ λ³νν΄μΌ νλ μν©μ΄ λ°μλ  λ μ¬μ©ν©λλ€.
    - `map()` : νΉμ  μμμ μνλ ν¨μλ₯Ό λͺ¨λ μ μ©μν¬ μ μμ΅λλ€.
    - μλ₯Ό λ€μ΄ {βκΉμλ°β, βλ°μλ°β, βνμλ°β, βλ°μ€νλ§β}μμ μ±λ§ μλ₯΄κ³ , μ€λ³΅λλ μ±μ μ κ±°ν΄μ {βκΉβ, βλ°β, βνβ}λΌλ λ°μ΄ν°λ₯Ό μ»κ³  μΆλ€λ©΄ λ€μκ³Ό κ°μ΄ μ½λλ₯Ό μμ±νλ©΄ λλ€.
    
    ```java
    Stream<String> nameStream = Stream.of("κΉμλ°", "λ°μλ°", "νμλ°", "λ°μ€νλ§");
    
    nameStream.map(name -> name.substring(0, 1))
            .distinct()
            .forEach(System.out::println);
    ```
    
    - map()μ μ¬μ©ν΄μ λͺ¨λ  λ°μ΄ν°μ substring()μ μ μ©ν΄μ μ±μ¨λ§ μλΌλλλ€.
    - distinct() μ¬μ©ν΄μ μ€λ³΅λλ λ°μ΄ν°λ₯Ό μ κ±°ν©λλ€.
5. μ€νΈλ¦Όμ μμλ₯Ό μ‘°ν - peek()
    - μ€νΈλ¦Ό μ°μ°μ μ§ννλ μ€κ°μ λ§μ½ λ°μ΄ν°λ₯Ό μΆλ ₯ν΄μ λ³΄κ³  μΆλ€λ©΄ μ΄λ»κ² ν΄μΌν κΉ. forEach()λ₯Ό μ°λ©΄ μ΅μ’ μ°μ°μ΄κΈ° λλ¬Έμ μ€νΈλ¦Όμ μλͺ¨νκ² λλ€. μ΄λ μ¬μ©ν  μ μλ κ²μ΄ peek()μ΄λ€.
    
    ```java
    Stream<String> nameStream = Stream.of("κΉμλ°", "λ°μλ°", "νμλ°", "λ°μ€νλ§");
    
            nameStream.map(name -> name.substring(0, 1))
                    .peek(name -> System.out.print("\"" + name + "\""))
                    .distinct()
                    .peek(name -> System.out.println("μ μ¬λΌμ§μ§ μμμ΅λλ€."))
                    .collect(Collectors.toList());
    ```
    
    ```bash
    "κΉ"μ μ¬λΌμ§μ§ μμμ΅λλ€.
    "λ°"μ μ¬λΌμ§μ§ μμμ΅λλ€.
    "ν"μ μ¬λΌμ§μ§ μμμ΅λλ€.
    "λ°"
    ```
    
    μΆλ ₯ κ²°κ³Όλ₯Ό λ³΄λ©΄ λ§μ§λ§ βλ°βμ distinct()λ₯Ό ν΅ν΄μ μ¬λΌμ Έμ λ· λ¬Έκ΅¬κ° μΆλ ₯λμ§ μμ κ²μ νμΈν  μ μμ΅λλ€.
    
6. Stream<T[]>λ₯Ό Stream<T>λ‘ λ³ν - flatMap()
    - λ°°μ΄μ΄ μΈμμΈ μ€νΈλ¦Όμ κΈ°λ³Έ νμμΌλ‘ λ°κΎΈμ΄ μμμ ν΄μΌλλ κ²½μ°κ° μμ μλ μλ€. μ΄λλ `flatMap()`μ μ¬μ©νλ©΄ λλ€.
    - μλ₯Ό νλ λ€μ΄λ³΄μ.
    
    ```java
    Stream<String[]> streamArr = Stream.of(
                    new String[] {"κΉμλ°", "νμλ°"},
                    new String[] {"λ°μλ°", "μ μλ°"}
    );
    
    List<String> nameList = streamArr.flatMap(Arrays::stream)
          .collect(Collectors.toList());
    
    System.out.println(nameList.toString());
    
    // μΆλ ₯ : [κΉμλ°, νμλ°, λ°μλ°, μ μλ°]
    ```
    
    μ μ½λλ₯Ό μ΄ν΄λ³΄λ©΄ λ°°μ΄ μμμ μλ κ²λ€μ΄ νλμ λ¦¬μ€νΈμ μ μ₯λ κ²μ νμΈν  μ μλ€. μ΄λ κ² μ€νΈλ¦Όμ λ°°μ΄λ‘ λ μμλ€μ΄ μμ λ, κ° νμμ μμλ‘ λΆλ¦¬ν΄μ νλμ μ€νΈλ¦ΌμΌλ‘ λ§λ€ μ μλ κΈ°λ₯μ΄ flatMap()μ΄λ€. 
    

## πΒ μ€νΈλ¦Όμ μ΅μ’μ°μ°

μ΅μ’μ°μ°μ μ€νΈλ¦Όμ μμλ₯Ό μλͺ¨ν΄μ κ²°κ³Όλ₯Ό λ§λ€μ΄λΈλ€. κ·Έλμ μ΅μ’ μ°μ° νμλ μ€νΈλ¦Όμ΄ λ«νκ³ , λλ μ¬μ©ν  μ μκ² λλ€.

1. `forEach()`
    - λ°ν νμμ΄ void μ΄κΈ° λλ¬Έμ μμλ₯Ό μΆλ ₯νλ μ©λλ‘ λ§μ΄ μ¬μ©λλ€.
    - μμ λ§μ΄ μ¬μ©νμ§λ§ μμλ₯Ό νλ λ€μ΄λ³΄λ©΄ λ€μκ³Ό κ°λ€.
    
    ```java
    Stream.of("κΉμλ°", "λ°μλ°", "μ μλ°")
                    .forEach(name -> System.out.print(name + " "));
    
    // μΆλ ₯ : κΉμλ° λ°μλ° μ μλ°
    ```
    
    λ€μκ³Ό κ°μ΄ μ€νΈλ¦Όμ μμλ€μ μΆλ ₯ν  μ μμ΅λλ€.
    
2. μ‘°κ±΄ κ²μ¬ - allMatch(), anyMatch(), noneMatch(), findFirst(), findAny()
    - μ€νΈλ¦Ό μμμ λν΄μ μ ν΄μ§ μ‘°κ±΄μ λͺ¨λ μΌμΉνλμ§, μΌλΆλ§ μΌμΉνλμ§, μ΄λ ν μμλ μΌμΉνμ§ μλμ§ νμΈν  μ μλ μ©λλ‘ μ¬μ©ν©λλ€. μ΄ μ°μ°λ€μ κ²°κ³Όλ‘ boolean κ°μ λ°νν©λλ€.
    - `allMatch()` : ν΄λΉ μ‘°κ±΄μ λͺ¨λ  μμκ° μ°Έμ κ°μ κ°λμ§ κ²μ¬ν©λλ€.
        
        ```java
        boolean containsJava = Stream.of("κΉμλ°", "λ°μλ°", "μ μλ°")
                        .allMatch(name -> name.contains("μλ°"));
        
        System.out.println(containsJava);  // true
        ```
        
        λͺ¨λ  μμκ° μ΄λ¦μ βμλ°βλ₯Ό ν¬ν¨νκ³  μλμ§ κ²μ¬νλ μ½λμλλ€.
        
    - `anyMatch()` : ν΄λΉ μ‘°κ±΄μ μ΄λ νλμ μμλΌλ μ°Έμ κ°μ κ°λμ§ κ²μ¬ν©λλ€.
        
        ```java
        boolean containsJava = Stream.of("κΉνμ΄μ¬", "λ°μ¨", "μ μλ°")
                        .anyMatch(name -> name.contains("μλ°"));
        
        			System.out.println(containsJava);  // true
        ```
        
        μ΄λ μμ νλλΌλ βμλ°βλ₯Ό ν¬ν¨νκ³  μλμ§ κ²μ¬νλ μ½λμλλ€.
        
    - `noneMatch()` : ν΄λΉ μ‘°κ±΄μ μ°Έμ κ°μ κ°λ μμκ° νλλ μλμ§ κ²μ¬ν©λλ€.
        
        ```java
        boolean containsJava = Stream.of("κΉνμ΄μ¬", "λ°μ¨", "μ μ½λ©")
                        .noneMatch(name -> name.contains("μλ°"));
        
        System.out.println(containsJava);  // true
        ```
        
    - `findFirst()` : filterμ μμ£Ό μ¬μ©λ©λλ€. ν΄λΉ μ‘°κ±΄μ ν΄λΉνλ μμ μ€ μ € μμ μλ μμλ₯Ό λ°νν©λλ€. λ°νλλ νμμ Optional<T> μλλ€.
        
        ```java
        Optional<String> findName = Stream.of("κΉμλ°", "λ°μλ°", "μ μλ°")
                        .filter(name -> name.contains("μλ°"))
                        .findFirst();
        
        System.out.println(findName.get());  // κΉμλ°
        ```
        
        λ³λ ¬ μ€νΈλ¦ΌμΈ κ²½μ°μλ findFirst() λμ  findAny()λ₯Ό μ¬μ©ν΄μΌ νλ€.
        
        !! λΉμ΄μλ Optional κ°μ²΄λ λ΄λΆμ μΌλ‘ nullμ μ μ₯νκ³  μμ΅λλ€. 
        
3. ν΅κ³ - count(), sum(), average(), max(), min()
    - IntStreamκ³Ό κ°μ΄ κΈ°λ³Έν μ€νΈλ¦Όμλ sum(), average()μ κ°μ μ΅μ’ μ°μ° λ©μλκ° μ‘΄μ¬ν©λλ€.
        
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
        
    - κΈ°λ³Έ μ€νΈλ¦Όμ κ²½μ°μλ count(), min(), max()μ λν ν΅κ³ μ°μ°λ§μ μ κ³΅ν©λλ€.
        
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
        
        λλΆλΆμ κ²½μ° μμΌλ‘ λ°°μλ³Ό reduce()μ collect()λ₯Ό μ¬μ©ν΄μ ν΅κ³ μ λ³΄λ₯Ό μ»μ΅λλ€.
        
4. λ¦¬λμ± - reduce()
    - μ€νΈλ¦Όμ μμλ₯Ό μ€μ¬λκ°λ©΄μ μ°μ°μ μννκ³  μ΅μ’κ²°κ³Όλ₯Ό λ°νν©λλ€. μ²μ λ μμλ₯Ό κ°μ§κ³  μ°μ°ν κ²°κ³Όλ₯Ό κ°μ§κ³  κ·Έ λ€μ μμλ₯Ό μ°μ°ν©λλ€. μ΄ κ³Όμ μμ μ€νΈλ¦Όμμ μμλ₯Ό νλμ© μλͺ¨νκ² λκ³ , μ€νΈλ¦Όμ λͺ¨λ  μμλ₯Ό μλͺ¨νλ©΄ κ·Έ κ²°κ³Όλ₯Ό λ°νν©λλ€.
    - maxμ κ²°κ³Όλ₯Ό μ»μ μ μλ μ½λλ₯Ό μμ±ν΄λ³΄κ² μ΅λλ€.
        
        ```java
        IntStream stream = IntStream.of(1, 2, 3, 4, 5);
        int max = stream.reduce(Integer.MIN_VALUE, (a,b) -> a>b ? a:b);
        System.out.println(max);
        ```
        
        μλμ κ°μ΄λ μμ±ν  μ μμ΅λλ€.
        
        ```java
        IntStream stream = IntStream.of(1, 2, 3, 4, 5);
        OptionalInt max = stream.reduce(Integer::max);
        System.out.println(max.getAsInt());
        ```
        
    - sumμ κ²°κ³Όλ₯Ό μ»μ μ μλ μ½λλ₯Ό μμ±ν΄λ΄λλ€.
        
        ```java
        IntStream stream = IntStream.of(1, 2, 3, 4, 5);
        int sum = stream.reduce(0, (a,b) -> a + b);
        System.out.println(sum);
        ```
        
        μ΄κΈ° κ°μΈ 0μ aμ μ μ₯νκ³ , μ€νΈλ¦Όμ λ€μ μμμΈ bλ₯Ό νλμ© κΊΌλ΄λ©΄μ aμ λμ ν΄λκ°λ μλ¦¬λ₯Ό μ΄μ©ν κ²μλλ€.
        
    - countμ κ²°κ³Όλ₯Ό μ»μ μ μλ μ½λλ₯Ό μμ±ν΄λ΄λλ€.
        
        ```java
        Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5);
        int count = stream.reduce(0, (a,b) -> a + 1);
        System.out.println(count);
        ```
        

## πΒ collect()

collect()κ° μ€νΈλ¦Όμ μμλ₯Ό μμ§νκΈ° μν΄μλ μ΄λ»κ² μμ§ν  κ²μΈκ°μ λν λ°©λ²μ΄ μ μλμ΄ μμ΄μΌ νλ€. μ΄ λ°©λ²μ μ μν κ²μ΄ λ°λ‘ **μ»¬λ ν°(collector)**μ΄λ€. 

μ»¬λ ν°λ Collector μΈν°νμ΄μ€λ‘ κ΅¬νν κ²μ΄κ³ , μ§μ  κ΅¬νν  μλ μκ³  λ―Έλ¦¬ μμ±λ κ²μ μ¬μ©ν  μλ μμ΅λλ€. Collector ν΄λμ€μλ λ€μν μ’λ₯μ μ»¬λ ν°λ₯Ό λ°ννλ static λ©μλκ° μ΄λ―Έ μ μλμ΄ μκ³ , κΈ°λ³Έμ μΌλ‘ μ κ³΅λλ μ»¬λ ν°λ§μΌλ‘λ λ§μ μΌλ€μ ν  μ μμ΅λλ€.

<aside>
π‘ **collect()** μ€νΈλ¦Όμ μ΅μ’μ°μ°, λ§€κ°λ³μλ‘ Collectorλ₯Ό νμλ‘ ν©λλ€. 
**Collector** μΈν°νμ΄μ€μ΄κ³ , μ»¬λ ν°λ μ΄ μΈν°νμ΄μ€λ₯Ό κ΅¬νν΄μΌ ν©λλ€.
**Collectors** ν΄λμ€μ΄κ³ , static λ©μλλ‘ λ―Έλ¦¬ μμ±λ μ»¬λ ν°λ₯Ό μ κ³΅ν©λλ€.

</aside>

## πΒ μ€νΈλ¦Όμ μ»¬λ μκ³Ό λ°°μ΄λ‘ λ³ν

Collectors ν΄λμ€μλ toList(), toSet(), toMap(), toCollection(), toArray() λ©μλλ₯Ό μ¬μ©νλ©΄ μ€νΈλ¦Όμ μ»¬λ μκ³Ό λ°°μ΄λ‘ λ³νν  μ μμ΅λλ€.

λ§μ½ List, Setμ΄ μλ ArrayListμ κ°μ νΉμ  μ»¬λ μμ μ§μ νκΈ° μν΄μλ toCollection()μ ν΄λΉ μ»¬λ μμ μμ±μ μ°Έμ‘°λ₯Ό λ§€κ°λ³μλ‘ λ£μ΄μ£Όλ©΄ λ©λλ€. μλ μ½λμμ νμΈν΄λ³΄κ² μ΅λλ€.

```java
List<String> name = List.of("κΉμλ°", "λ°μλ°", "νμλ°");

ArrayList<String> name2 = name.stream()
				.collect(Collectors.toCollection(ArrayList::new));
```

μμμ λ³΄λ©΄ nameμ΄λΌλ Listλ₯Ό toCollection(ArrayList::new)λ₯Ό μ¬μ©ν΄μ ArrayListλ‘ λ³νν κ²μ λ³Ό μ μμ΅λλ€.

1. `toMap()`
    - Mapμ ν€μ κ°μ μμΌλ‘ μ μ₯ν΄μΌνκΈ° λλ¬Έμ κ°μ²΄μ μ΄λ€ νλλ₯Ό ν€λ‘ μ¬μ©ν μ§μ κ°μΌλ‘ μ¬μ©ν μ§λ₯Ό μ§μ ν΄μ€μΌ νλ€.
    
    ```java
    public class StreamPractice {
        public static void main(String[] args) {
            Stream<Person> personStream = Stream.of(
                    new Person("κΉμλ°", 20),
                    new Person("λ°μλ°", 25),
                    new Person("νμλ°", 26)
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
    {κΉμλ°=20, λ°μλ°=25, νμλ°=26}
    ```
    
    toMap()μμλ ν€μ κ°μ λͺ¨λ λκ²¨μ€μΌ νλ€. μ μμ μμλ Person ν΄λμ€μ μ΄λ¦(name)μ keyλ‘ μ°κ³ , λμ΄(age)λ₯Ό valueλ‘ μ¬μ©νλ μ½λμλλ€.
    
2. `toArray()`
    - μ€νΈλ¦Όμ μ μ₯λ μμλ₯Ό T[] νμμ λ°°μ΄λ‘ λ³ννλ €λ©΄ toArray()λ₯Ό μ¬μ©νλ©΄ λ©λλ€.
    - μ£Όμν΄μΌν  μ μ toArray()μ μμ±μ μ°Έμ‘°λ₯Ό λ§€κ°λ³μλ‘ μ§μ ν΄μ€μΌ νλλ°, λ§μ½ λ§€κ°λ³μλ‘ μ§μ ν΄μ£Όμ§ μλλ€λ©΄ λ°νλλ νμμ Object[] μλλ€.
    
    ```java
    Student[] studentNames = studentStream.toArray(Student[]::new);
    Student[] studentNames = studentStream.toArray(); // ERROR λ°μ
    Object[] studentNames = studentStream.toArray();
    ```
