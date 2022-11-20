## 1. 터미널에서 mySQL의 bin이 있는 곳으로 접근

```bash
cd /usr/local/mysql/bin
```

## 2. root 계정으로 접근

```bash
./mysql -u root -p
```

```bash
Enter password: {자신이 mySQL을 다운로드 받을 때 입력한 비밀번호}
```

<img width="476" alt="image" src="https://user-images.githubusercontent.com/70641477/202910786-277f481b-0c73-4ace-b8af-bd55550d8fc2.png">


접속이 성공하면 위와 같은 문구가 나옴.

## 3. 새로운 계정 만들기

계속 root 계정을 사용할 수는 없으니 새로운 계정을 만들어준다.

- 지금 존재하는 계정 확인하기
    
    ```bash
    mysql> use mysql;
    ```
    
    mysql 스키마를 사용한다는 의미입니다.
    
    ```bash
    mysql> select user, host from user;
    ```
    
    <img width="491" alt="image" src="https://user-images.githubusercontent.com/70641477/202910812-10eeca4d-84dd-44c1-853c-517f0142b2f6.png">

    
- 새로운 계정 만들기
    
    ```bash
    mysql> create user {username}@{ip} identified by '{password}';
    ```
    
- 기존에 접속해있는 root 계정에서 나가기
    
    ```bash
    mysql> exit;
    ```
    
- 새로 만든 계정에 접근하기
    
    ```bash
    ./mysql -u {username} -p
    ```
    

## 4. 계정 삭제하기

```bash
mysql> drop user {username};
```

## 5. 권한 설정하기

```bash
mysql> show grants for {username}@{ip};
```

<img width="490" alt="image" src="https://user-images.githubusercontent.com/70641477/202910830-7be0c810-f319-4083-b207-621d7410bfd2.png">


위에 나타나는 kimhunsope@localhost의 권한은 `USAGE`입니다. 이는 권한 없음을 나타냅니다.

- 권한을 추가하기
    
    ```bash
    mysql> grant {권한} privileges on {스키마}.{테이블} to {username}@{ip};
    ```
    
    - 사용 예시 알아보기
        
        ```bash
        grant all privileges on *.* to {username}@{ip};
        ```
        
        모든 스키마.테이블에 대한 모든 권한을 부여한다는 의미입니다.
        
         
        
        ```bash
        grant select, insert privileges on {스키마}.* to {username}@{ip};
        ```
        
        특정 스키마에 있는 모든 테이블에 insert와 select에 대한 권한을 부여한다는 의미입니다.
        
- 권한을 제거하기
    
    ```bash
    mysql> revoke {권한} privileges on {스미카}.{테이블} from {username}@{ip};
    ```
    

이렇게 `grant to`로 권한을 부여하고, `revoke from`으로 권한을 제거할 수 있습니다.
