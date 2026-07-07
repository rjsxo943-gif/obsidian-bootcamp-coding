# PyInstaller 실행파일 만들기

## 핵심 요약

PyInstaller는 Python 코드를 `.exe` 같은 실행파일로 묶어주는 도구이다.  
`0706` 폴더에 있는 `.spec`, `build`, `dist`는 실행파일 빌드 과정에서 생기는 파일과 폴더이다.

---

## 관련 파일

```text
0706/memo.py
0706/memo.spec
0706/dr.py
0706/dr.spec
0706/build/
0706/dist/
```

---

## 역할 정리

|항목|역할|
|---|---|
|`.py`|원본 Python 코드|
|`.spec`|PyInstaller 빌드 설정 파일|
|`build/`|빌드 중간 산출물|
|`dist/`|최종 실행파일이 들어가는 폴더|

---

## 일반적인 명령어

```bash
pyinstaller memo.py
```

또는 콘솔창 없이 GUI 프로그램만 띄우고 싶을 때:

```bash
pyinstaller --windowed memo.py
```

하나의 파일로 묶고 싶을 때:

```bash
pyinstaller --onefile --windowed memo.py
```

---

## 내 식으로 이해

Python 코드는 원래 Python이 설치된 환경에서 실행된다.  
하지만 PyInstaller를 쓰면 Python 코드와 필요한 실행 정보를 묶어서 다른 사람이 더 쉽게 실행할 수 있는 형태로 만들 수 있다.

```text
.py 파일 → PyInstaller → dist 폴더 안 실행파일
```

---

## 주의할 점

- 실행파일은 운영체제별로 따로 만들어야 한다.
- Windows에서 만든 `.exe`는 보통 Windows용이다.
- 빌드 결과물은 용량이 커질 수 있다.
- `build/`, `dist/`는 GitHub에 반드시 올릴 필요는 없다.
- 소스 관리에서는 보통 `.py`, `README.md`, 필요하면 `.spec` 정도만 남기는 경우가 많다.

---

## 연결 노트

- [[코드해설 - 0706 memo.py 메모장 실행파일]]
- [[코드해설 - 0706 dr.py 그림판 실행파일]]

---

## 태그

#python #개념정리 #pyinstaller #실행파일 #exe
