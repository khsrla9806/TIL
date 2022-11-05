# ✏️ 변수명 네이밍 규칙

### 좋은 변수명 짓기

- 의도를 분명히 밝혀 이름을 지어야 한다.
    - 따로 주석이 필요하다면 의도가 분명한 이름이 아니라는 의미.
    - 이름은 구체적이어야한다.
    - 모호하거나 하나 이상의 목적으로 사용될 수 있는 이름은 피해라.
- 협업을 염두해서 짓기
    - 숫자와 같은 상수들은 모호한 의미를 줄 수 있기 때문에 변수에 이름을 붙여서 의미를 표현한다.
- 맥락을 고려해서 짓기
    - 이름이 지나치게 짧은 경우 변수의 용도를 알기 어렵다.
    - 의미가 불분명한 짧은 이름은 피하는 것이 좋다.
- `boolean` 타입 변수의 작명
    - `done`, `error`, `found`, `success`, `ok`와 같이 성공합을 의미하는 구체적인 이름이 있다면 다른 이름을 사용하는 것이 좋다.
    - 참이나 거짓의 의미를 함축하는 `boolean` 변수의 이름을 사용한다.
        - 예를 들어 `statusOk`, `sourceFileAvailable`, `sourceFileFound`
    - `not` 보다는 `is`를 붙인 변수명을 짓는다.
- 메소드가 여러번 호출된 한눈에 보기 힘든 코드
    - 변수에 일부 함수를 호출한 결과값을 담아서 길이를 줄여준다.
- 변수 이름에 자료형이 들어가는 경우
    - 다른 자료형을 써야하는 경우가 오면 결국 변수 이름을 바꿔줘야하기 때문에 추천하지 않는다.

# ✏️ 메소드 네이밍 규칙

### 메소드 네이밍에서 고려해야하는 것

1. 왜 존재해야 하는가?
2. 무슨 작업을 하는 메소드인가?
3. 어떻게 사용하는 메소드인가?

### 메소드 명명 규칙

- `lowerCamelCase`로 작성하기
    - 첫 번째 단어는 소문자, 이어지는 단어의 첫글자는 대문자로 작성.
    - 메소드명은 기본적으로 `동사`로 시작.
    - 다른 타입으로 전환하는 메소드나 빌더 패턴을 구현한 클래스의 메소드에는 `전치사`를 쓸 수 있다.
        - 예를 들면 `toString()`

### 메소드 이름으로 자주 사용되는 동사

- `get` / `set`
    - 객체의 데이터에 마음대로 접근이 가능하다면 메소드를 통해 만들어진 데이터는 의미가 없게 된다.
        - 클래스의 캡슐화를 통해서 객체의 데이터를 보호할 수 있다.
- `init`
    - 데이터를 초기화하는 메소드
- `is` / `has` / `can`
    - 위 3개는 boolean 값을 리턴합니다.
    - `is` : 맞는지 틀린지 판단하는 메소드명
    - `has` : 데이터가 있는지 없는지 확인하는 메소드명
    - `can` : 할 수 있는지 없는지 확인하는 메소드명
- `create`
    - 새로운 객체를 만든 후 리턴해주는 메소드명
- `find`
    - 데이터를 찾는 메서드명
- `to`
    - 해당 객체를 다른 형태의 객체로 변환해주는 메서드명

# ✏️ 네이밍할 때 참고하면 좋을 개발자 영어

### 함수와 메서드

1. 함수는 동작을 나타내기 때문에 현재형 동사로 시작해야 한다.
    - 현재형 동사로 시작하는 문장은 명령형을 나타낸다.
    - 함수를 호출한다는 것은 일반적으로 컴퓨터, 객체, 서버 무언가에게 명령을 내리는 행동이다.
2. 현재형 동사로 시작되지 않는 함수는 99% 잘못됐습니다. 예외는 존재한다.
    - onClick과 같은 함수가 예외이다.
    - 위와 같은 경우는 명령을 내리는 것보다는 받는 입장이라고 생각하면 된다.

```java
gameStart() -> startGame()
imageProcess() -> processImage()
```

### 변수와 상수

1. 변수는 값을 나타낸다. 메서드와 다르게 동사 원형으로 시작하면 안 된다.
    - `is`는 동사이지만 잘 알려진 컨벤션에 속합니다.
    - `was` 또한 마찬가지로 잘 알려진 컨벤션에 속합니다.
    - be 동사의 경우에는 그 자체로써의 행위를 나타내지 않고, 뒤에 따라오는 단어와 결합해 상태를 나타냅니다.
    - boolean 변수로 예를 들어봅시다.
        
        ```java
        boolean playVideo() // 변수 이름보다는 함수이름에 어울립니다.
        
        boolean isPlaying() // be 동사를 사용하여 변수이름으로 적합.
        ```
        
        - be 동사는 메서드 이름으로도 적합하고, 변수명으로 사용해도 적합합니다.

### 클래스

1. 클래스 이름은 명사 또는 명사구로 작성하면 됩니다.

### 동사를 두 개 사용하고 싶은 경우

- 최대한 피해야하고, 쓰지 않는 것이 적극 권장됩니다.
- 즉, 메서드(함수)는 하나의 기능만 할 수 있도록 최소 단위로 나누는 것이 좋습니다.

### 복수형

- 3인칭 단수는 일반적으로 `동사 + s` 의 형태를 써야 합니다.
- `hava`는 `has`로 사용해야하고, `contain`은 `contains`를 사용해야 합니다.
- 배열에서 자주 사용하는 메서드인 `contains`를 예시로 들 수 있습니다.
    - `[”사과”, “배”, “바나나”]`의 배열에 `“레몬”`이 있는지 확인하는 코드를 써보자.
    
    ```java
    ["사과", "배", "바나나"].contains("레몬");
    ```
    
    - 위 코드를 보면 배열은 3개의 인자를 가지고 있지만, 하나의 배열 객체로 보기 때문에 `contain`이 아닌 `contains`를 사용합니다.

### 수동태

- `pick`은 선택하다라는 동사입니다.
- 만약 선택된 아이템을 나타내는 변수명을 만들고 싶다면?
    - `pickedItem`이라는 변수명을 사용하면 됩니다.

### 줄임말

- 이름을 마음대로 축약하는 것은 피하는 것이 좋습니다.
- 저도 많이 사용했던 축약어 중에 하나는 `Array`를 `arr`로 많이 줄여서 사용했었습니다.
- 축약어 쓰지 않는 것이 좋습니다.

### 반의어

- `enable`의 반대는 `inactive`가 아닙니다. `disable`입니다.
- 이렇게 짝을 이루는 것들은 여럿 있습니다.
- `accept`의 반대는 `reject`이고, `set`과 `get`은 거의 가족입니다.