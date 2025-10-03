\# 📘 Python 데이터 분석 학습 기록



\## 📌 주제: Do it! 데이터 분석을 위한 판다스 입문



---



\### 1. 파이썬 패키지 관리자 pip

\- \*\*pip\*\*: 파이썬 라이브러리(패키지)를 설치하고 관리하는 프로그램  

\- \*\*패키지(Library/Package)\*\*: 필요한 기능을 미리 작성하여 모아 둔 것 (파이썬에서는 “패키지”라 부름)  



---



\### 2. 판다스 시작하기



\#### 02-1 판다스가 왜 필요할까?

\- \*\*판다스(pandas)\*\*: 데이터 분석용 오픈소스 파이썬 라이브러리  

\- 새로운 자료형 제공

&nbsp; 1) \*\*데이터프레임(DataFrame)\*\*: 전체 스프레드시트, 직사각형 형태의 데이터  

&nbsp; 2) \*\*시리즈(Series)\*\*: 데이터프레임의 한 열(column)  



👉 “시리즈 여러 개 = 데이터프레임”으로 생각 가능  

👉 판다스는 스프레드시트처럼 동작하지만, \*\*자동화/재현성/데이터 통합\*\*에 강점  



\*\*장점\*\*

1\. 여러 데이터셋에 동일한 분석 과정을 자동화 가능  

2\. 실행 단계를 기록하여 재현성 확보  

3\. 스프레드시트보다 안정적이며, 다른 데이터베이스/데이터셋과 통합 가능  



---



\#### 02-2 데이터셋 불러오기



\*\*CSV 파일 불러오기\*\*

```python

import pandas as pd



\# CSV 파일 읽기

df = pd.read\_csv("data.csv")



\# 탭으로 구분된 파일은 sep 인자 사용

df\_tab = pd.read\_csv("data.tsv", sep="\\t")

데이터 구조 확인



python

코드 복사

print(type(df))  

\# <class 'pandas.core.frame.DataFrame'>

행/열 개수 확인



python

코드 복사

df.shape     # (1704, 6)  ← 메서드가 아니라 '속성'이라 괄호 없음

열 이름 확인



python

코드 복사

df.columns

\# Index(\['country', 'continent', 'year', 'lifeExp', 'pop', 'gdpPercap'], dtype='object')

각 열 자료형 확인



python

코드 복사

df.dtypes

\# country      object

\# continent    object

\# year          int64

\# lifeExp     float64

\# pop           int64

\# gdpPercap   float64

기본 정보 확인



python

코드 복사

df.info()

\# 행 개수, 결측치 여부, 자료형, 메모리 사용량 등을 보여줌

📌 판다스 자료형 vs 파이썬 자료형



판다스 dtype	파이썬 type	설명

object	str	문자열

int64	int	정수

float64	float	실수

datetime64	datetime	날짜/시간



02-3 데이터 추출하기

앞부분/뒷부분 확인



python

코드 복사

df.head()   # 처음 5개 행

df.tail()   # 마지막 5개 행

열(column) 데이터 추출



문자열로 추출 → 시리즈 반환



python

코드 복사

country\_series = df\["country"]

print(type(country\_series))  # <class 'pandas.core.series.Series'>

리스트로 추출 → 데이터프레임 반환



python

코드 복사

country\_df = df\[\["country"]]

print(type(country\_df))      # <class 'pandas.core.frame.DataFrame'>

여러 열 추출



python

코드 복사

df\_subset = df\[\["country", "continent", "year"]]

print(df\_subset.shape)  # (1704, 3)

📌 주의



df\[0] 처럼 인덱스로 열을 추출하면 KeyError 발생



반드시 열 이름을 사용해야 함



열 추출의 두 가지 방식 차이



문자열 방식 → Series 반환



리스트 방식 → DataFrame 반환



python

코드 복사

country\_series = df\["country"]

print(type(country\_series))  

\# <class 'pandas.core.series.Series'>



country\_df = df\[\["country"]]

print(type(country\_df))      

\# <class 'pandas.core.frame.DataFrame'>

점 표기법



python

코드 복사

df\["country"]   # 대괄호 표기법

df.country      # 점 표기법 (단축 표기법)

단, 점 표기법은 열 이름이 기본 속성과 충돌하지 않을 때만 가능.

예: 열 이름이 count, sum 등과 같다면 점 표기법 불가.

