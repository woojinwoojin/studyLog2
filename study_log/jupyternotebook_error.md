🐍 Jupyter Notebook / Lab 7.x 비밀번호 로그인 문제 해결 가이드

📌 문제 증상



Jupyter Notebook 7.4.7 (jupyter-server 기반)에서 로그인 시도 시 401 Unauthorized 발생



올바른 비밀번호를 입력해도 로그인 실패



토큰 모드("token": "...")에서는 정상 접속 가능



--debug 로그에 ServerApp.password, NotebookApp.password, IdentityProvider.hashed\_password가 동시에 출력됨 → 충돌 발생



🔎 원인



Notebook 7.x는 더 이상 .py 설정 파일의 ServerApp.password 방식이 아닌,

jupyter\_server\_config.json 의 IdentityProvider 블록을 사용해야 함.



하지만 사용자 폴더(%USERPROFILE%\\.jupyter)에 남아 있던 옛 설정 파일들:



jupyter\_lab\_config.py



jupyter\_notebook\_config.py

이 안에 c.ServerApp.password = 'argon2:...' 같은 라인이 남아 있어서

서로 다른 비밀번호 해시가 동시에 로드 → 항상 인증 실패.



🛠 해결 과정

1\. 충돌나는 설정 찾기

findstr /S /I /N "ServerApp.password NotebookApp.password IdentityProvider.hashed\_password" "%USERPROFILE%\\.jupyter\\\*.\*"





👉 결과에서 jupyter\_lab\_config.py, jupyter\_notebook\_config.py 안에 활성 줄 발견.



2\. 옛 설정 비활성화



가장 확실한 방법: 파일 이름 변경



ren "%USERPROFILE%\\.jupyter\\jupyter\_lab\_config.py" "jupyter\_lab\_config.py.disabled"

ren "%USERPROFILE%\\.jupyter\\jupyter\_notebook\_config.py" "jupyter\_notebook\_config.py.disabled"





또는 해당 줄에 # 붙여 주석 처리.



3\. 비밀번호 재설정



Notebook 7.x에서는 notebook.auth 모듈이 없으므로:



jupyter server password





👉 새 비밀번호 입력

👉 C:\\Users\\<사용자>\\.jupyter\\jupyter\_server\_config.json 자동 갱신됨



예시 JSON:



{

&nbsp; "IdentityProvider": {

&nbsp;   "hashed\_password": "argon2:$argon2id$v=19$m=10240,t=10,p=8$jc6ryg...Q3M",

&nbsp;   "token": ""

&nbsp; }

}



4\. 서버 재시작 \& 확인

jupyter lab --debug





로그에 IdentityProvider.hashed\_password=... 만 보이면 정상



더 이상 ServerApp.password 나 NotebookApp.password는 나오면 안 됨



접속:



같은 PC: http://127.0.0.1:8888/lab



다른 기기: http://<서버IP>:8888/lab



👉 로그인 창에 새 비밀번호 입력 → 성공 🎉



✅ 교훈 \& 권장 방법



Notebook 7.x에서는 반드시 jupyter\_server\_config.json 하나만 관리



옛 .py 설정(jupyter\_lab\_config.py, jupyter\_notebook\_config.py)은 삭제/비활성화



비밀번호 변경은 jupyter server password 한 줄이면 충분



가능하면 숫자 IP 주소(127.0.0.1, 192.168.x.x) 로 접속 (호스트명 인코딩 문제 예방)



문제 발생 시 jupyter lab --debug 로 로드되는 설정을 확인



💡 이 과정을 따르면 Notebook 7.x 환경에서 401 로그인 문제를 빠르게 해결할 수 있습니다.

