---
layout: post
title: "[python] txt 파일 읽기/쓰기"
author: optboy
categories: [Python]
---

프로그래밍을 어느정도 하다보면 프로그램 내부적으로 txt파일을 읽고 써야하는 상황이 많이 발생한다.  
이번에는 python을 통해 txt파일을 다루는 방법에 대해 정리해보려 한다.

# 파일 열기

파일을 읽거나 쓰기 위해서는 먼저 파일을 열어야 한다. 여는 방법은 아래와 같다.

```python
f = open("새파일.txt", 'w')
f.close()
# 해당 코드가 실행된 경로에 "새파일.txt"라는 이름의 파일이 생겼을 것이다.
# 만약 이미 같은 이름의 파일이 존재했을 경우, 원래 내용이 모두 사라진다.
```
이때 `open()`함수는 파이썬 내장함수로, 어떤 모듈을 import할 필요도 없다.  
그리고 `w`는 쓰기모드를 뜻한다. 파일을 여는 모드는 다음와 같은 것들이 있다.

| 모드      | 뜻                                      | 
| -------  | -----------                            |
| `r`      | 읽기모드 - 파일을 읽을 때                    |  
| `w`      | 쓰기모드 - 파일을 쓸 때                     |
| `a`      | 추가모드 - 파일의 마지막 부분에 내용을 추가할 때 |  

이때, 파일의 경로를 직접 입력하고 싶다면, `새파일.txt` 대신 경로를 직접 입력해주기만 하면 된다.  

`f.close()`는 꼭 안해도 되지만 오류를 방지하기 위해 최대한 해주는게 좋다. 

# 파일에 출력값 적기

파일에 원하는 내용을 적고싶다면, 아래와 같은 방식으로 `write()`함수를 쓰면 된다.

```python
f = open("새파일.txt", 'w')
for i in range(1, 11):
    data = "%d번째 줄입니다.\n" % i
    f.write(data)
f.close()
```
앞서 설명한 파일을 여는 방법을 통해 파일을 연 다음, `write()`함수를 통해서 원하는 값을 넣었다.

# 파일의 내용 읽기

파일의 내용을 읽고 싶다면, 다음과 같이 `readline()` 함수를 사용하면 된다.  
이때, open의 모드는 `'r'`이다.

```python
f = open("새파일.txt", 'r')
line = f.readline()
print(line)
f.close()
```

만약 위 출력 예제를 그대로 따라했다면, '1번째 줄입니다.'가 출력될 것이다.  
`readline()`함수는 파일을 한 줄씩 읽는다. 이때, 더 이상 읽을 줄이 없다면 빈 문자열 `""`을 리턴한다.  

그리고 만약 파일의 모든 줄을 한번에 읽어오고 싶다면 다음과 같이 `readlines()`함수를 사용할 수 있다.

```python
f = open("새파일.txt", 'r')
lines = f.readlines()
for line in lines:
    print(line)
f.close()
```

`readlines()`는 파일의 모든 줄을 읽어서 각 라인을 요소로 갖는 리스트를 리턴한다.  
따라서 위 코드를 통해 모든 줄을 출력할 수 있게 된다.

다른 방법으로는, `read()`함수를 사용하는 방법이 있다.

```python
f = open("새파일.txt", 'r')
data = f.read()
print(data)
f.close()
```

`read()`함수는 파일의 전체 내용을 문자열로 리턴한다.

# 파일에 새로운 내용 추가하기

앞서 설명한 쓰기 모드('w')로 파일을 열게 되면, 파일의 모든 내용이 사라지게 된다.  
하지만 기존 내용을 유지한 채 내용을 추가하고 싶을 수 있다. 그럴 때는 추가 모드('a')로 파일을 열면 된다.

```python
f = open("새파일.txt",'a')
for i in range(11, 20):
    data = "%d번째 줄입니다.\n" % i
    f.write(data)
f.close()
```

# with문을 사용해서 파일열기

이때까진 `open()`함수를 사용해서 파일을 열었다. 하지만 이는 `close()`도 해줘야 하기 때문에 번거롭다.
그래서 with문을 통해 열고 닫는걸 동시에 처리할 수 있다.  

앞선 예시를 with문으로 바꿔보면 다음과 같다.  

```python
with open("새파일.txt",'a') as f:
    for i in range(11, 20):
        data = "%d번째 줄입니다.\n" % i
        f.write(data)
```

#### 참고
- [점프 투 파이썬](https://wikidocs.net/26)
- [GeeksforGeeks](https://www.geeksforgeeks.org/reading-writing-text-files-python/)