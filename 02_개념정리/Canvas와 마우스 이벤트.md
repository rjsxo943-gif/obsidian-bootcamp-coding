# Canvas와 마우스 이벤트

## 핵심 요약

`Canvas`는 선, 도형, 그림을 그릴 수 있는 tkinter 위젯이다.  
그림판 프로그램에서는 Canvas와 마우스 이벤트를 연결해 선을 그렸다.

---

## Canvas 생성

```python
self.canvas = tk.Canvas(master, bg="white", highlightthickness=0)
self.canvas.pack(fill="both", expand=True)
```

흰색 배경의 그림판 영역을 만든다.

---

## 마우스 이벤트 연결

```python
self.canvas.bind("<Button-1>", self.start_draw)
self.canvas.bind("<B1-Motion>", self.draw)
self.canvas.bind("<ButtonRelease-1>", self.stop_draw)
```

|이벤트|의미|
|---|---|
|`<Button-1>`|마우스 왼쪽 버튼 클릭|
|`<B1-Motion>`|왼쪽 버튼 누른 채 이동|
|`<ButtonRelease-1>`|왼쪽 버튼 떼기|

---

## 선 그리기

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

이전 좌표에서 현재 좌표까지 선을 긋는다.

---

## 좌표 저장 원리

```python
self.last_x = event.x
self.last_y = event.y
```

마우스가 움직일 때마다 현재 좌표를 다음 선의 시작점으로 저장한다.

---

## 지우개 원리

```python
def current_color(self):
    return "white" if self.eraser else self.color
```

지우개는 실제 삭제가 아니라 흰색으로 그리는 방식이다.

---

## 전체 삭제

```python
self.canvas.delete("all")
```

캔버스의 모든 객체를 삭제한다.

---

## 내 식으로 이해

그림판은 어려운 그래픽 엔진이 아니라 좌표를 계속 이어 붙이는 것이다.

```text
처음 좌표 저장
→ 마우스 이동
→ 이전 좌표와 현재 좌표를 선으로 연결
→ 현재 좌표를 다시 저장
→ 반복
```

---

## 연결 노트

- [[tkinter GUI 기본 구조]]
- [[이벤트와 콜백 함수]]
- [[코드해설 - 0706 dr.py 그림판 실행파일]]

---

## 태그

#python #개념정리 #canvas #마우스이벤트 #그림판
