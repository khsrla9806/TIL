## 필요한 패키지 Import 해줍니다.

```java
import java.util.*;
```

`java.util.HashMap` 이렇게 선언해줘도 되는데, `java.util` 패키지는 많이 쓰이기 때문에 모든 내용을 사용한다는 의미로 `*` 을 쓰는 것이 좋습니다.

## Map 선언하기

```java
HashMap<String, Integer> map = new HashMap<String, Integer>();
```

파이썬에 있어서 딕셔너리 같은 존재의 **Map**을 선언합니다.

`Map <key, value>`의 특징을 갖고 있습니다

`key`로 식별을 하고 `value`에 있는 값을 사용합니다.

`key`는 중복이 불가하고, 동일한 `key` 값으로 넣으면 최근에 넣은 값이 적용됩니다.
<br><br>

### Map을 선언하는 방법은 아래와 같습니다.

1. `HashMap`

    : Map 안에서 key와 value에 따른 순서가 없습니다.

2. `TreeMap`

    : key 값에 따라서 오름차순으로 정렬합니다. 정렬이 들어가기 때문에 삽입, 삭제 시에 오래 걸립니다.

3. `LinkedHashMap`

    : 삽입 순서에 따라 정렬합니다.

4. `HashTable`

    : key와 value에 null을 넣을 수 없습니다.
<br><br>

## Map의 주요기능

1. Map 안에 값 넣기

    `Map.put(key, value);`

2. Map 안의 값 가져오기 → key로 value를 출력

    `Map.get(key);`

3. Map 크기 확인하기 (key의 개수)

    `Map.size();`

4. Map 안의 내용 변경하기 → `Map.put()` 으로 해도 됨.

    `Map.replace(key, value);`

5. Map 안에 특정 key, value가 있는지 확인하기

    `Map.containsKey(key);`

    `Map.containsValue(value);`

6. Map의 크기가 0인지 확인하기

    `Map.isEmpty();`

7. Map 안의 내용을 삭제하기

    `Map.remove(key);`

8. Key가 존재하면 value를 얻어내고, 없다면 default를 호출

    `Map.getOrDefault(key, default);`

9. Key가 없거나 value가 null일 때만 삽입하기

    `Map.putIfAbsent(key, value);`