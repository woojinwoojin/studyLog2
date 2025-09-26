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



