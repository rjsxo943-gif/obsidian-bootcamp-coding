# PyInstaller 실행파일 만들기

## 한 줄 정의

PyInstaller는 Python 프로젝트를 배포 가능한 실행 형태로 묶을 때 사용하는 도구이다.

0706에서는 `memo.py`, `dr.py`를 만들면서 `.spec`, `build`, `dist` 같은 빌드 관련 파일과 폴더가 생겼다.

---

## 0706에서 확인한 파일과 폴더

```text
0706/memo.py
0706/memo.spec
0706/dr.py
0706/dr.spec
0706/build/
0706/dist/
```

|항목|역할|
|---|---|
|`.py`|원본 Python 코드|
|`.spec`|빌드 설정 파일|
|`build/`|빌드 중간 산출물|
|`dist/`|최종 결과물이 들어가는 폴더|

---

## 기본 명령어

PyInstaller 공식 문서 기준 기본 형태는 다음과 같다.

```bash
pyinstaller 파일명.py
```

예를 들어 메모장 프로그램을 묶으려면 `memo.py`가 있는 폴더에서 실행한다.

```powershell
cd "C:\Users\rjsxo\bootcamp\mycodehouse\0706"
pyinstaller memo.py
```

그림판도 같은 방식이다.

```powershell
pyinstaller dr.py
```

이렇게 실행하면 보통 아래 파일과 폴더가 생긴다.

```text
memo.spec
build/
dist/
```

---

## 자주 쓰는 옵션

### 1. 폴더 형태로 만들기

기본값은 폴더 형태이다.

```powershell
pyinstaller memo.py
```

결과는 보통 다음 위치에 생긴다.

```text
dist/memo/
```

### 2. 파일 하나로 묶기

```powershell
pyinstaller --onefile memo.py
```

결과는 보통 다음 위치에 생긴다.

```text
dist/memo.exe
```

### 3. GUI 프로그램에서 콘솔창 숨기기

`tkinter`처럼 창이 따로 뜨는 프로그램은 콘솔창이 같이 뜨면 보기 싫을 수 있다.

```powershell
pyinstaller --windowed memo.py
```

또는 같은 의미로 다음 옵션도 자주 쓴다.

```powershell
pyinstaller --noconsole memo.py
```

### 4. 파일 하나 + 콘솔창 숨기기

메모장이나 그림판처럼 GUI 프로그램을 하나의 실행파일로 묶고 싶을 때 많이 쓴다.

```powershell
pyinstaller --onefile --windowed memo.py
```

그림판이면 다음처럼 한다.

```powershell
pyinstaller --onefile --windowed dr.py
```

---

## 오늘 코드 기준 추천 명령어

0706 폴더에서 실행한다고 하면 다음 두 개가 제일 실전적이다.

```powershell
pyinstaller --onefile --windowed memo.py
pyinstaller --onefile --windowed dr.py
```

빌드가 끝나면 `dist` 폴더 안에서 결과물을 확인한다.

```text
0706/dist/memo.exe
0706/dist/dr.exe
```

---

## `.spec` 파일로 다시 만들기

한 번 PyInstaller를 실행하면 `.spec` 파일이 생긴다.

```text
memo.spec
dr.spec
```

이 설정 파일을 기준으로 다시 빌드할 수도 있다.

```powershell
pyinstaller memo.spec
pyinstaller dr.spec
```

`.spec` 파일은 아이콘, 추가 파일, 숨은 import 같은 설정을 더 세밀하게 조정할 때 사용한다.

---

## GitHub에 올릴 때 생각할 점

보통 GitHub에는 원본 코드와 설명 문서를 중심으로 올린다.

```text
권장: .py, README.md, 필요한 설정 파일
주의: build/, dist/ 같은 결과물 폴더
```

`build/`, `dist/`는 용량이 커질 수 있고, 다시 만들 수 있는 결과물이기 때문에 매번 올릴 필요는 없다.

---

## 내 식으로 이해

Python 파일은 원본 코드이고, PyInstaller 관련 파일은 그 코드를 실행 가능한 형태로 묶는 과정에서 생기는 산출물이다.

즉 오늘 기억할 핵심은 이 구조다.

```text
원본 코드 → pyinstaller 명령어 실행 → .spec 생성 → build 생성 → dist 결과물 생성
```

가장 자주 쓸 명령어는 이거다.

```powershell
pyinstaller --onefile --windowed 파일명.py
```

---

## 관련 코드

- [[0706 코드 해설]]
- [[2026-07-06]]

---

## 태그

#python #개념정리 #pyinstaller #빌드 #배포