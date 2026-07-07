# tkinter GUI 기초

> 0706 `tkinter` 관련 개념을 한 파일로 합친 통합 노트이다.  
> GUI 기본 구조, 이벤트/콜백, 메모장 파일 열기/저장, Canvas 그림판을 여기서 한 번에 복습한다.

---

## 1. 한 줄 정의

`tkinter`는 Python에서 창이 있는 프로그램을 만들 때 사용하는 기본 GUI 라이브러리이다.

```text
tkinter GUI = 창 만들기 + 위젯 배치 + 이벤트 연결 + mainloop 실행
```

---

## 2. 기본 구조

```python
import tkinter as tk

root = tk.Tk()
root.title("메모장")
root.geometry("800x600")
root.mainloop()
```

|코드|의미|
|---|---|
|`tk.Tk()`|메인 창 생성|
|`title()`|창 제목 설정|
|`geometry()`|창 크기 설정|
|`mainloop()`|이벤트 대기 시작|

`mainloop()`가 실행되면 프로그램은 바로 끝나지 않고, 사용자의 클릭이나 키보드 입력을 기다린다.

---

## 3. 위젯

위젯은 GUI 화면에 들어가는 부품이다.

|위젯|역할|
|---|---|
|`Button`|버튼|
|`Label`|글자 표시|
|`Entry`|한 줄 입력|
|`Text`|여러 줄 입력|
|`Menu`|메뉴바|
|`Canvas`|그림 그리는 공간|
|`Frame`|위젯을 묶는 영역|
|`Scale`|슬라이더|

0706 메모장에서는 `Text`, `Menu`, `Scrollbar`를 사용했고, 그림판에서는 `Canvas`, `Button`, `Scale`을 사용했다.

---

## 4. 이벤트와 콜백 함수

이벤트는 사용자의 행동이고, 콜백 함수는 이벤트가 발생했을 때 실행되는 함수이다.

```text
버튼 클릭 → command에 연결된 함수 실행
마우스 드래그 → bind에 연결된 함수 실행
키보드 단축키 → bind_all에 연결된 함수 실행
```

### 버튼 이벤트

```python
tk.Button(toolbar, text="색상", command=self.choose_color)
```

버튼을 누르면 `choose_color()`가 실행된다.

### 마우스 이벤트

```python
self.canvas.bind("<Button-1>", self.start_draw)
self.canvas.bind("<B1-Motion>", self.draw)
self.canvas.bind("<ButtonRelease-1>", self.stop_draw)
```

|이벤트|의미|
|---|---|
|`<Button-1>`|마우스 왼쪽 버튼 누름|
|`<B1-Motion>`|왼쪽 버튼을 누른 채 이동|
|`<ButtonRelease-1>`|왼쪽 버튼 뗌|

---

## 5. 메모장 구조

```python
class Notepad:
    def __init__(self, root):
        self.root = root
        self.root.title("메모장")
        self.root.geometry("800x600")
        self.file_path = None
        self.create_widgets()
```

메모장 프로그램 전체를 `Notepad` 클래스로 묶었다.

- `root`: 메인 창
- `file_path`: 현재 열려 있는 파일 경로
- `create_widgets()`: 텍스트창, 메뉴, 스크롤바 생성

---

## 6. 파일 열기와 저장

파일 선택 창은 `filedialog`를 사용한다.

```python
path = filedialog.askopenfilename(
    defaultextension=".txt",
    filetypes=[("텍스트 파일", "*.txt"), ("모든 파일", "*.*")]
)
```

파일 읽기:

```python
with open(path, "r", encoding="utf-8") as f:
    self.text.delete("1.0", tk.END)
    self.text.insert("1.0", f.read())
```

파일 저장:

```python
with open(path, "w", encoding="utf-8") as f:
    f.write(self.text.get("1.0", tk.END))
```

`"1.0"`은 Text 위젯의 첫 번째 줄 0번째 글자이고, `tk.END`는 마지막 위치이다. 즉 전체 텍스트를 의미한다.

한글이 깨지지 않도록 `encoding="utf-8"`을 지정하는 것이 중요하다.

---

## 7. Canvas와 그림판

`Canvas`는 선, 도형, 그림을 그릴 수 있는 위젯이다.

```python
self.canvas = tk.Canvas(master, bg="white", highlightthickness=0)
self.canvas.pack(fill="both", expand=True)
```

마우스를 누른 위치를 저장하고, 이동할 때마다 이전 좌표와 현재 좌표를 선으로 연결한다.

```python
self.canvas.create_line(
    self.last_x, self.last_y,
    event.x, event.y,
    fill=self.current_color(),
    width=self.width,
    capstyle="round",
    smooth=True
)
```

---

## 8. 지우개 원리

```python
def current_color(self):
    return "white" if self.eraser else self.color
```

지우개는 실제 삭제가 아니라, 흰색 선으로 덮어 그리는 방식이다.

전체 지우기는 다음 코드로 처리한다.

```python
self.canvas.delete("all")
```

---

## 9. 내 식으로 이해

GUI는 위에서 아래로 한 번 실행하고 끝나는 코드가 아니다.

```text
창을 띄워둔다
→ 사용자가 클릭하거나 입력한다
→ 이벤트가 발생한다
→ 연결된 함수가 실행된다
```

메모장은 `Text`와 파일 입출력을 연습한 코드이고, 그림판은 `Canvas`와 마우스 이벤트를 연습한 코드이다.

---

## 10. 관련 코드

- [[0706 코드 해설]]
- [[2026-07-06]]

---

## 태그

#python #개념정리 #tkinter #gui #이벤트 #콜백 #canvas #메모장 #그림판