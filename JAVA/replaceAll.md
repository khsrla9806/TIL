## 1. replace() 메서드

String 클래스의 메서드 중 하나입니다. 대상 문자열을 원하는 문자 값으로 변환하는 함수입니다.

### 1.1 사용 방법

`replace(CharSequence target, CharSequence replacement)`

변환하고자 하는 대상이 되는 문자열(target)과 변환할 문자열(replacement)을 매개변수로 넣어주면 사용이 가능합니다.

```java
String test = "안녕하세요. 김훈섭입니다.";

System.out.println(test.replace("안녕하세요.", "Hello"));

// 출력 : Hello 김훈섭입니다.
```
<br>

## 2. replaceAll() 메서드

대상 문자열을 원하는 문자 값으로 변환할 수 있는 함수입니다.

### 2.1 사용 방법

`replaceAll(String regex, String replacement)`

변환하고자 하는 대상이 되는 문자열(regex)과 변환할 문자열(replacement)을 매개변수로 넣어주면 사용이 가능합니다.

```java
String test = "안녕하세요. 안녕하세요. 김훈섭입니다.";

System.out.println(test.replaceAll("안녕하세요.", "Hello");

// 출력 : Hello Hello 김훈섭입니다.
```
<br>

## 3. replace()와 replaceAll()의 차이점

첫 번째는 replace()는 인자로 CharSequence를 받고, replaceAll()은 인자로 String을 받는다는 차이점이 있습니다.

두 번째는 replaceAll()의 첫 번째 인자를 보면 regex라고 되어 있는데, 정규 표현식을 사용할 수 있다는 것을 의미합니다.

### 3.1 사용 비교

```java
String test = "aaabbbvccacfgdracabtghd";

System.out.println(test.replace("ab", "0");
// 000000vccacfgdrac0tghd

Ststem.out.println(test.replaceAll("[ab]", "0");
// 000000vcc0cfgdr0c00tghd
```
<br>

## 4. 정규 표현식의 사용

- `\uAC00-\uD7A30` : 모든 한글 음절
- `a-z` : 영어 소문자
- `A-Z` : 영어 대문자
- `0-9` : 숫자
- `\\s` : 띄어쓰기

정규 표현식에서 `^`는 정규표현식에 해당하지 않는 경우를 의미합니다.

```java
String.replaceAll("[^\uAC00-\uD7A30-9a-zA-z\\s]", "");
```

위 코드는 모든 한글, 영어 소문자, 영어 대문자, 숫자, 공백이 아닌 문자만 모두 찾아서 제거하라는 코드입니다.

```java
String.replaceAll("[^0-9]", "");
```

위 코드는 숫자가 아닌 문자는 모두 찾아서 제거하라는 코드입니다.

```java
String.replaceAll("[0-9]", "");
```

위 코드는 반대로 숫자만 찾아서 모두 제거하라는 코드입니다.

이처럼 정규 표현식과 replaceAll()을 적절히 사용하면 원하는 문자들만 남기고 모두 제거할 수 있습니다. 

예시로는 공백을 제거하는데도 사용되기도 합니다.