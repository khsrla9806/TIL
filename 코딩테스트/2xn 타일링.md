`Level 2`

## 코딩테스트 연습 > 연습문제 > 2 x n 타일링

### **문제 설명**

가로 길이가 2이고 세로의 길이가 1인 직사각형모양의 타일이 있습니다. 이 직사각형 타일을 이용하여 세로의 길이가 2이고 가로의 길이가 n인 바닥을 가득 채우려고 합니다. 타일을 채울 때는 다음과 같이 2가지 방법이 있습니다.

- 타일을 가로로 배치 하는 경우
- 타일을 세로로 배치 하는 경우

예를들어서 n이 7인 직사각형은 다음과 같이 채울 수 있습니다.

![https://i.imgur.com/29ANX0f.png](https://i.imgur.com/29ANX0f.png)

직사각형의 가로의 길이 n이 매개변수로 주어질 때, 이 직사각형을 채우는 방법의 수를 return 하는 solution 함수를 완성해주세요.

### 제한사항

- 가로의 길이 n은 60,000이하의 자연수 입니다.
- 경우의 수가 많아 질 수 있으므로, 경우의 수를 1,000,000,007으로 나눈 나머지를 return해주세요.

---

### 입출력 예

| n | result |
| --- | --- |
| 4 | 5 |

### 입출력 예 설명

입출력 예 #1다음과 같이 5가지 방법이 있다.

![https://i.imgur.com/keiKrD3.png](https://i.imgur.com/keiKrD3.png)

![https://i.imgur.com/O9GdTE0.png](https://i.imgur.com/O9GdTE0.png)

![https://i.imgur.com/IZBmc6M.png](https://i.imgur.com/IZBmc6M.png)

![https://i.imgur.com/29LWVzK.png](https://i.imgur.com/29LWVzK.png)

![https://i.imgur.com/z64JbNf.png](https://i.imgur.com/z64JbNf.png)

### 👨🏻‍💻 나의 소스코드

> 해결 못했습니다.
> 

```java
class Solution {
    public int solution(int n) {
        int answer = 1;
        int twoCount = 0;

        while (true) {
            if (n - 2 < 0) {
                break;
            }
            n -= 2;
            twoCount++;

            answer += combination(twoCount + n, twoCount);
        }

        return answer;
    }
    
    public int combination(int n, int r) {
        int totalN = n;
        int totalR = r;

        while (r != 1) {
            n--;
            r--;
            totalN *= n;
            totalR *= r;
        }

        return totalN / totalR;
    }
}
```

### 🔎 다른 사람의 소스코드

```java
lass Solution {
    public int solution(int n) {
        int answer = 0;
        int current = 1;
        int previous = 1;

        for (int i = 0; i < n - 1; i++) {
            answer = (current + previous) % 1000000007;
            previous = current;
            current = answer;
        }

        return answer;
    }
}
```

### 🤔 피드백

1. **조합을 이용해서 풀어보려고 접근**
    
    정답은 나왔는데 계속해서 런타임 에러가 발생해서 실패했습니다. 테스트 케이스를 추가해서 봤는데도 통과는 했지만 `1000000007`로 나눴을 때의 나머지를 반환하는 과정에서 아마 코드가 잘못되었을 거라고 생각이된다.
    
    <img width="836" alt="image" src="https://user-images.githubusercontent.com/70641477/212301712-4ee00fbc-6381-4ed6-b1b7-f0827ef14d6a.png">
    
2. **다른 사람의 풀이를 봤을 때, 피보나치 수열….**
    
    진짜 천재다. 이걸 보고 피보나치 수열이라고 생각했다는 것에 일단 배우고 갑니다.
    
    경우의 수를 써보면 1, 2, 3, 5, 8…순서로 증가하는 것을 확인할 수 있다. 이거는 피보나치 수열임을 깨닫고 문제를 풀면 정말 쉽게 코드를 작성할 수 있다.
    
    하지만 주어진 문제에서는 `1000000007`로 나눈 나머지의 값을 반환하도록 하라는 조건이 있었고, 경우의 수가 너무 커지면 overFlow 에러가 발생하기 때문에 중간 중간에 계속 나눠주는 것을 확인할 수 있다.
