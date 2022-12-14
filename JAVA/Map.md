## 1. 필요한 패키지 Import 해줍니다.

```java
import java.util.*;
```

`java.util.HashMap` 이렇게 선언해줘도 되는데, `java.util` 패키지는 많이 쓰이기 때문에 모든 내용을 사용한다는 의미로 `*` 을 쓰는 것이 좋습니다.

## 2. Map 선언하기

```java
HashMap<String, Integer> map = new HashMap<String, Integer>();
```

파이썬에 있어서 딕셔너리 같은 존재의 **Map**을 선언합니다.

`Map <key, value>`의 특징을 갖고 있습니다

`key`로 식별을 하고 `value`에 있는 값을 사용합니다.

`key`는 중복이 불가하고, 동일한 `key` 값으로 넣으면 최근에 넣은 값이 적용됩니다.
<br><br>

## 3. Map의 주요기능

3.1 Map 안에 값 넣기

    `Map.put(key, value);`
<br>

3.2 Map 안의 값 가져오기 → key로 value를 출력

    `Map.get(key);`
<br>

3.3 Map 크기 확인하기 (key의 개수)

    `Map.size();`
<br>

3.4 Map 안의 내용 변경하기 → `Map.put()` 으로 해도 됨.

    `Map.replace(key, value);`
<br>

3.5 Map 안에 특정 key, value가 있는지 확인하기

    `Map.containsKey(key);`

    `Map.containsValue(value);`
<br>

3.6 Map의 크기가 0인지 확인하기

    `Map.isEmpty();`
<br>

3.7 Map 안의 내용을 삭제하기

    `Map.remove(key);`
<br>

3.8 Key가 존재하면 value를 얻어내고, 없다면 default를 호출

    `Map.getOrDefault(key, default);`
    
```java
HashMap<String, Integer> map = new HashMap<>();

System.out.println(map.getOrDefault("Me", 0));

// 출력 0
```
위 코드를 보면 "Me"라는 키 값이 없기 때문에 0이라는 Default 값이 출력되는 것을 확인할 수 있습니다. 
<br>

3.9 Key가 없거나 value가 null일 때만 삽입하기

    `Map.putIfAbsent(key, value);`
<br>

## 4. Map을 사용한 예제
4.1 Map에 초기값을 넣어 선언하기
```java
HashMap<String, Integer> map = new HashMap<String, Integer>() {{
    put("홍길동", 23);
    put("조나단", 25);
}};
```
<br>

4.2 Map에서 Comparator를 사용하여 내림차순으로 정렬하기
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();

        map.put("key1", 1);
        map.put("key2", 2);
        map.put("key3", 3);

        if(map.containsKey("key1") && map.containsValue(1)) {
            System.out.println("true");
        }

        List<String> keyList = new ArrayList<>(map.keySet());

        // key를 가지고 내림차순으로 정렬. 비교는 value로 한다.
        Collections.sort(keyList, new Comparator<String>() {
            public int compare(String str1, String str2) {
                int value1 = map.get(str1);
                int value2 = map.get(str2);

                return Integer.compare(value2, value1);
            }
        });

        for(String s : keyList) {
            System.out.println(s + " = " + map.get(s));
        }
    }
}

// 출력
// true
// key3 = 3
// key2 = 2
// key1 = 1
```
