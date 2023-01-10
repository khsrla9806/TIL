### 📖 RR 스케쥴러란?

**RR (Round-Robin) 스케쥴러**는 들어온 순서대로 정해진 time quantum 마다 프로세스를 실행시키고 주어진 time quantum이 지나면 Ready Queue로 들어가서 대기를 한 후 자신의 차례를 기다리는 알고리즘을 사용한다.

### 🤔 헷갈렸던 문제

<img width="715" alt="image" src="https://user-images.githubusercontent.com/70641477/211487208-bc53aa6f-b10e-45bc-9c2f-4dbca662dc5c.png">

### 레디 큐를 시각적으로 보면서 이해해봅시다.

1. **P1부터 주어진 time quantum을 수행하고, 1초에 P2가 도착하여 Ready Queue에 들어가 있습니다.**
    
    <img width="708" alt="image" src="https://user-images.githubusercontent.com/70641477/211487244-d2a1ab7e-40d1-4e6d-90e6-08fe18244406.png">
    
2. **P2가 Running 상태가 되어 실행되는 중간에 3초가 되면 P3 프로세스가 Ready Queue에 들어옵니다.**
    
    <img width="718" alt="image" src="https://user-images.githubusercontent.com/70641477/211487290-1d671098-dc4c-47b9-b8bb-69618f32a4c2.png">

    
3. **위 와 같은 방법으로 계속 실행하다 보면 가장 먼저 종료되는 프로세스가 발생합니다.**
    
    <img width="717" alt="image" src="https://user-images.githubusercontent.com/70641477/211487330-80dfe39c-35ec-4bbf-bd6e-58b17ab7952c.png">
    
    - 1번 프로세스가 가장 먼저 종료됩니다.
    
4. **계속 이어서 다음 프로세스를 진행합니다.**
    
    <img width="725" alt="image" src="https://user-images.githubusercontent.com/70641477/211487372-6fed7055-d170-4f80-8418-c5362fff90e7.png">
    

즉, 정답은 `P1 > P3 > P2` 순서로 프로세스가 종료됩니다.
