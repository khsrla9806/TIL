# 👨🏻‍💻 단위 테스트와 통합 테스트

### 단위 테스트(Unit Test)란?

하나의 모듈을 기준으로 독립적으로 진행되는 가장 작은 단위의 테스트를 말한다. 여기서 하나의 모듈이란 애플리케이션을 작동시키는 하나의 기능 또는 메서드를 말합니다. 단위 테스트의 목적은 애플리케이션을 실행시키기 위해서 구현한 어떤 하나의 기능(메서드)이 올바른 결과 값을 도출하는지 독립적으로 테스트함에 있습니다. 간단하게 “어떤 기능이 실행되면 어떤 결과가 나온다.” 정도로 테스트를 진행하면 된다.

### 통합 테스트(Integration Test)란?

모듈을 통합하는 과정에서 모듈 간의 호환성을 확인하기 위한 테스트입니다. 애플리케이션에는 여러개의 모듈이 존재하고, 여러개의 모듈이 서로 메시지(함수)를 주고 받으면서 기능을 실행시킵니다. 그렇기 때문에 통합된 여러개의 모듈이 정상적으로 실행되는지 확인하는 것이 통합 테스트의 목적입니다. 통합 테스트는 단위 테스트와는 다르게 독립적인 테스트가 아니고 웹 페이지로부터 API를 호출하고 올바르게 동작하는지 테스트하는 것을 말합니다.

### 단위 테스트 작성의 필요성

통합 테스트는 여러 컴포넌트 사이의 상호작용을 테스트 하기 때문에 모든 컴포넌트가 구동된 상태에서 테스트를 진행합니다. 그 뜻은 컴포넌트가 많아질 수록 구동해야 하는 컴포넌트가 증가하고 그 결과 테스트에 필요한 비용(시간)이 증가하게 됩니다. 반면에 단위 테스트의 경우에는 해당 부분의 독립적인 기능에 대해서 테스트 하기 때문에 코드를 리펙토링 하더라도 빠르게 테스트를 진행해볼 수 있습니다.

- 테스트 비용(시간)을 절약할 수 있습니다.
- 새로운 기능 추가 시 빠르게 테스트해볼 수 있습니다.
- 코드에 대한 문서가 될 수 있습니다.
- 리펙토링 시에 안전성을 확보할 수 있습니다.

그렇기 때문에 실무에서 사용되는 TDD(Test Driven Development, 테스트 주도 개발)도 단위 테스트를 의미합니다. 

### 단위 테스트의 문제점과 stub

어떤 객체가 자체적으로 모든 기능을 다 할 수 있다면 좋겠지만, 일반적인 애플리케이션에서는 다른 객체와 메시지를 주고 받으면서 기능을 수행하게 됩니다. 하지만 단위 테스트는 한 가지 기능에 대한 단위 테스트이기 때문에 다른 객체와 데이터를 주고 받는 경우 문제가 발생하게 됩니다. 

이때 사용하는 것이 가짜 객체(Mock Obkect)를 주입하여 어떤 결과를 반환하라는 정해진 답변을 준비해야하는데 이것을 stub라고 합니다. 예를 들어 데이터 베이스에 입력받은 데이터를 주입하는 테스트를 진행할 때, 가짜 데이터베이스(Mock Database)를 주입하여 insert 처리 시에 반드시 반환값이 1이 나오도록 정해주는 것이 stub입니다.

### 좋은 단위 테스트의 특징

요구 사항은 날이 갈수록 변화하고, 그 요구 사항에 따라서 코드를 계속 수정해나가야 합니다. 하지만 코드가 변경된다는 것은 그만큼 잠재적 버그가 발생할 가능성을 증가시킵니다. 여기서 만약 좋은 테스트 코드가 존재한다면 테스트 코드를 돌려서 변경된 코드를 검증할 수 있습니다. 또한 코드가 변경됨에 따라 테스트 코드가 변경되어야 하는 경우가 있는데 이를 대비해서 테스트 코드도 가독성 있게 작성하기 위한 노력을 해야 합니다. 

그렇기에 테스트 코드를 작성할 때 다음과 같은 사항을 준수하는 것이 좋습니다.

1. 1개의 테스트 함수에 대해서 assert를 최소화하라.
2. 1개의 테스트 함수는 1가지 개념만을 테스트하라.

또한 깨끗한 테스트 코드는 FIRST라는 5가지 규칙을 따라야 합니다.

- Fast : 테스트는 빠르게 동작하여 자주 돌릴 수 있어야 한다.
- Independent : 각각의 테스트는 독립적이며 서로 의존해서는 안된다.
- Repeatable : 어느 환경에서도 반복이 가능해야 한다.
- Self-validating : 테스트는 성공/실패로 boolean 값으로 결과를 내어 자체적으로 검증해야 한다.
- Timely : 테스트는 적시에 즉, 테스트하려는 실제 코드를 구현하기 직전에 구현해야 한다.

[[TDD] 단위 테스트(Unit Test) 작성의 필요성 (1/3)](https://mangkyu.tistory.com/143#recentComments)

# 👨🏻‍💻 Junit을 활용한 Java 단위 테스트 코드 작성

### java 단위 테스트 코드를 작성하기 위해 필요한 라이브러리

1. Junit5 : 자바 단위 테스트를 위한 테스팅 프레임워크
2. AssertJ : 자바 테스트를 돕기 위해서 다양한 문법을 지원하는 라이브러리

Junit만으로도 테스트를 진행할 수 있지만 테스트 코드의 가독성을 확보하기 위해서 Junit과 AssertJ를 함께 사용합니다.

IntelliJ에서 Gradle로 프로젝트를 생성한 후 build.gradle에 들어가서 의존성을 확인해봅니다. Gradle로 만들게 되면 junit에 대한 의존성은 이미 추가가 되어있습니다.

assertJ를 사용하기 위해서 의존성을 추가해줬습니다.

```java
testImplementation 'org.assertj:assertj-core:3.11.1'
```

### given-when-then 패턴

요즘 단위 테스트 작성에서 사용하는 패턴이라고 합니다. given-when-then 패턴은 1개의 단위 테스트를 3가지 단계로 나누어 작성하는 패턴입니다.

- given(준비) : 어떤 데이터가 준비되었을 때
- when(실행) : 어떤 함수를 실행하면
- then(검증) : 어떤 결과가 나와야 한다.

### 테스트 코드 공통 작성 규칙

```java
@DisplayName("테스트 이름")
@Test
void 테스트함수_이름() {
		// given
		
		// when

		// then
}
```

- @Test는 해당 테스트가 단위 테스트임을 명시하는 어노테이션입니다. Junit에서는 해당 어노테이션이 붙은 메소드를 단위 테스트로 인식하여 실행시킵니다.
- @DisplayName()을 사용하여 테스트 이름을 설정할 수 있습니다.

### 테스트 코드 작성

- 테스트 코드 작성을 위해서 필요한 구현 코드를 먼저 작성해보겠습니다.
    
    ```java
    import java.util.List;
    import java.util.Random;
    import java.util.stream.Collectors;
    
    public class LottoNumberGenerator {
        public List<Integer> generate(final int money) {
            if (!isValidMoney(money)) {
                throw new RuntimeException("올바른 금액이 아닙니다.");
            }
            return generate();
        }
    
        private boolean isValidMoney(final int money) {
            return money == 1000;
        }
    
        private List<Integer> generate() {
            return new Random()
                    .ints(1, 45 + 1)
                    .distinct() // 중복된 요소를 제거한 후 Stream을 다시 반환
                    .limit(6)
                    .boxed()
                    .collect(Collectors.toList());
        }
    }
    ```
    
    1000원을 입력하면 로또 번호를 랜덤으로 생성해서 리스트로 반환하는 함수 generate() 입니다.
    

### 세 가지 테스트를 진행

1. 로또 번호 갯수 테스트
    
    ```java
    @DisplayName("로또 번호 갯수 테스트")
        @Test
        void lottoNumberSizeTest() {
            // Given
            LottoNumberGenerator lottoNumberGenerator = new LottoNumberGenerator();
            final int price = 1000;
    
            // When
            List<Integer> lottoNumber = lottoNumberGenerator.generate(price);
    
            // Then
            assertThat(lottoNumber.size()).isEqualTo(6);
        }
    ```
    
    - Given : 로또를 생성할 객체와 로또 생성에 필요한 돈 1000원을 준비합니다.
    - When : 돈(price)를 로또 생성기의 generate() 메서드에 입력하여 로또를 받습니다.
    - Then : 받은 lottoNumber의 개수가 6개 인지 확인합니다. 이때 assertThat을 사용합니다.
2. 로또 번호 범위 테스트
    
    ```java
    @DisplayName("로또 번호 범위 테스트")
        @Test
        void lottoNumberRangeTest() {
            // Given
            LottoNumberGenerator lottoNumberGenerator = new LottoNumberGenerator();
            final int price = 1000;
    
            // When
            List<Integer> lottoNumber = lottoNumberGenerator.generate(price);
    
            // Then
            assertThat(lottoNumber.stream().allMatch(lotto -> lotto >= 1 && lotto <= 45)).isTrue();
        }
    ```
    
    - Given, When은 위와 동일합니다.
    - Then에서 Stream의 allMatch를 사용해서 로또 숫자 범위인 1부터 45에 모두 참의 값을 가지는지 확인하기 위해서 isTrue() 메서드를 사용합니다.
        - 그 이외에도 isFalse(), isNull(), isNotNull() 등이 있습니다.
3. 잘못된 로또 금액 테스트
    
    ```java
    @DisplayName("잘못된 로또 금액 테스트")
        @Test
        void lottoNumberInvalidMoneyTest() {
            // Given
            LottoNumberGenerator lottoNumberGenerator = new LottoNumberGenerator();
            final int price = 2000;
    
            // When
            final RuntimeException exception = assertThrows(RuntimeException.class, () -> lottoNumberGenerator.generate(price));
    
            // Then
            assertThat(exception.getMessage()).isEqualTo("올바른 금액이 아닙니다.");
        }
    ```
    
    - 잘못된 가격을 확인하기 위해서 price를 2000원으로 바꿉니다.
    - 실행되는 메서드인 generate()를 assertThrows로 감싸줍니다.
    - 메서드 실행 후 발생하는 exception의 메시지가 우리가 구현한 코드의 메시지와 동일한지 확인합니다.

[[Java] JUnit을 활용한 Java 단위 테스트 코드 작성법 (2/3)](https://mangkyu.tistory.com/144)
