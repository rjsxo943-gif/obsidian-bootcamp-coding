# tkinter GUI 기본 구조

## 핵심 요약

`tkinter`는 Python에서 기본으로 제공하는 GUI 라이브러리이다.  
창을 만들고, 버튼/텍스트창/메뉴 같은 위젯을 배치해서 프로그램을 만든다.

---

## 기본 구조

```python
import tkinter as tk

root = tk.Tk()
root.title("프로그램 제목")
root.geometry("800x600")

root.mainloop()
```

|코드|의미|
|---|---|
|`tk.Tk()`|메인 창 생성|
|`title()`|창 제목 설정|
|`geometry()`|창 크기 설정|
|`mainloop()`|GUI 이벤트 루프 시작|

---

## 위젯

위젯은 GUI에 들어가는 부품이다.

|위젯|역할|
|---|---|
|`Button`|버튼|
|`Label`|글자 표시|
|`Entry`|한 줄 입력|
|`Text`|여러 줄 입력|
|`Menu`|메뉴바|
|`Canvas`|그림 그리는 영역|
|`Frame`|위젯을 묶는 영역|
|`Scale`|슬라이더|

---

## 배치 방식

```python
widget.pack()
```

`pack()`은 위젯을 위/아래/왼쪽/오른쪽으로 간단히 배치한다.

```python
widget.grid(row=0, column=0)
```

`grid()`는 표처럼 행과 열 위치에 배치한다.

---

## 오늘 코드에서 나온 예시

```python
self.text = tk.Text(self.root, undo=True, wrap="word")
self.text.pack(fill="both", expand=True)
```

메모장에서는 `Text` 위젯을 창 전체에 꽉 차게 배치했다.

```python
self.canvas = tk.Canvas(master, bg="white")
self.canvas.pack(fill="both", expand=True)
```

그림판에서는 `Canvas`를 그림 그리는 공간으로 사용했다.

---

## 내 식으로 이해

`tkinter` 프로그램은 레고 조립 느낌이다.

```text
창 만들기 → 부품 만들기 → 부품 배치하기 → 이벤트 연결하기 → mainloop 실행
```

---

## 연결 노트

- [[이벤트와 콜백 함수]]
- [[Canvas와 마우스 이벤트]]
- [[파일 열기와 저장]]
- [[코드해설 - 0706 2.ipynb tkinter GUI와 NumPy]]

---

## 태그

#python #개념정리 #tkinter #gui
