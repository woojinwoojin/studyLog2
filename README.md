# studyLog2

\# 📘 Python 기초 학습 기록



\## 📌 주제: 모듈 (Module)



\### 2025.09.26

\- \*\*모듈 정의\*\*  

&nbsp; - 모듈은 필요할 때 가져다 쓸 수 있는, 또는 다른 프로그램의 일부가 될 수 있는 내용을 담고 있는 파일  

&nbsp; - `import`를 사용하여 불러옴  

&nbsp; - 같은 위치(디렉토리)에 있어야 사용 가능  



\- \*\*예시\*\*

&nbsp; ```python

&nbsp; # circle.py 라는 모듈 가져오기

&nbsp; import circle



특정 함수만 가져오기



모듈에 존재하는 특정 함수를 불러올 때 from ~ import ~ 사용



주의: 현재 프로그램의 함수 이름과 겹치면 안 됨



예시

\# circle.py 안의 ar\_circle 함수 가져오기

from circle import ar\_circle



모듈 이름 바꿔서 사용하기

as 키워드 사용

모듈 이름을 짧게 줄여서 쓰는 경우 유용



예시

\# circle 모듈을 cc라는 이름으로 사용

import circle as cc


# 📘 Python 기초 학습 기록

## 📌 주제: 빌트인 함수와 모듈

### 2025.09.26
- **빌트인 함수 (Built-in function)**  
  - Python 설치 시 기본 제공되는 함수  
  - `import` 선언 없이 바로 사용 가능  
  - 예시: `print()`, `len()`, `sum()`

- **빌트인 모듈 (Built-in module)**  
  - Python이 기본 제공하는 모듈  
  - `import` 선언 후 사용 가능  
  - 대표적인 모듈: `math`

- **math 모듈 주요 함수**
  ```python
  import math

  math.sqrt(16)     # 제곱근 → 4.0
  math.pow(2, 3)    # 거듭제곱 → 8.0
  math.factorial(5) # 팩토리얼 → 120
  math.gcd(12, 18)  # 최대공약수 → 6
  math.floor(3.7)   # 내림 → 3
  math.ceil(3.1)    # 올림 → 4
  math.pi           # 원주율 상수 3.141592...
  math.e            # 자연상수 2.718281...

📌 주제: 딕셔너리 (Dictionary)
12-1 딕셔너리의 이해

표현법: { 키 : 값 } 형태

값은 중복 가능하지만, 키는 중복 불가

여러 줄에 걸쳐 정의 가능

dc = { "정은호": "010-3333-56xx", "구아나": "010-2222-65xx" }

dc = {
    "코카콜라": 900,
    "바나나맛우유": 300,
    "비타500": 200
}

dc = {
    "이름": "이순동",
    "나이": 19,
    "직업": "학생",
    "키": 175
}

12-2 데이터 참조, 수정, 추가, 삭제

dc = {
    "코카콜라": 900,
    "바나나맛우유": 750,
    "비타500": 600,
    "삼다수": 450
}

# 참조
v = dc["삼다수"]       # 450

# 수정
dc["삼다수"] = 550

# 추가
dc["카페라테"] = 1300

# 삭제
del dc["비타500"]

12-3 연산자 == 과 딕셔너리 성격

d1 = {1: "a", 2: "b"}
d2 = {1: "a", 2: "b"}
d3 = {2: "b", 1: "a"}

print(d1 == d2)  # True
print(d1 == d3)  # True

➡ 딕셔너리는 저장 순서가 의미 없음

12-4 in / not in 연산

dc2 = {"새우깡": 700, "콘치즈": 850}

print("새우깡" in dc2)        # True
print("코카콜라" not in dc2) # True

➡ in 연산은 **값(value)**이 아니라 키(key) 존재 여부를 확인

12-5 딕셔너리와 for 루프

dc = {"새우깡": 700, "콘치즈": 850, "꼬깔콘": 750}

# 모든 값에 100원씩 추가
for i in dc:
    dc[i] += 100

➡ 딕셔너리 for 루프는 기본적으로 키를 순회

📌 주제: 클래스와 객체
13-1 전역변수와 지역변수

지역변수(Local Variable): 함수 안에서 선언 → 함수 실행 중에만 존재

전역변수(Global Variable): 함수 밖에서 선언 → 프로그램 전체에서 접근 가능

def func(n):
    lv = n + 1   # 지역변수
    print(lv)

func(10)   # 11

➡ 매개변수 n도 지역변수

cnt = 100

def func():
    print(cnt)  # 함수 내에서 전역변수 접근 가능

func()       # 100
print(cnt)   # 100

같은 이름의 변수 주의

cnt = 100

def func():
    cnt = 0   # 지역변수 cnt 선언
    print(cnt)

func()       # 0
print(cnt)   # 100 (전역변수 그대로 유지)

전역변수를 함수 안에서 수정하려면 global 키워드 사용

cnt = 100

def func():
    global cnt
    cnt = 0
    print(cnt)

func()       # 0
print(cnt)   # 0 (전역변수 값이 바뀜)



