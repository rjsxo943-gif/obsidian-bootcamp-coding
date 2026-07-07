# 생성자 __init__과 self

## 핵심 요약

`__init__`은 객체가 생성될 때 자동으로 실행되는 메소드이다.  
`self`는 현재 만들어진 객체 자신을 가리킨다.

---

## 기본 형태

```python
class Television:
    def __init__(self, channel, volume, on):
        self.channel = channel
        self.volume = volume
        self.on = on
```

---

## 객체 생성 시 동작

```python
tv1 = Television(1, 10, True)
```

위 코드는 내부적으로 이런 의미를 가진다.

```text
tv1.channel = 1
tv1.volume = 10
tv1.on = True
```

---

## self가 필요한 이유

```python
self.channel = channel
```

왼쪽 `self.channel`은 객체 안에 저장되는 값이다.  
오른쪽 `channel`은 생성자로 전달받은 값이다.

```text
전달받은 channel 값을
현재 객체의 channel 속성에 저장한다.
```

---

## 헷갈리는 부분

### 왜 `self`를 직접 넣는데 호출할 때는 안 넣나?

정의할 때:

```python
def get_channel(self):
    return self.channel
```

호출할 때:

```python
tv1.get_channel()
```

실제로는 Python이 `tv1`을 자동으로 `self` 자리에 넣어준다.

```text
tv1.get_channel()
→ Television.get_channel(tv1)
```

---

## 내 식으로 이해

`self`는 “내 것”이라는 표시다.

```python
self.channel
```

은 그냥 채널이 아니라 “이 객체의 채널”이다.

`tv1.channel`과 `tv2.channel`이 따로 존재할 수 있는 이유가 바로 `self` 때문이다.

---

## 연결 노트

- [[객체와 클래스]]
- [[인스턴스 변수와 클래스 변수]]
- [[코드해설 - 0706 1.ipynb 객체지향]]

---

## 태그

#python #개념정리 #self #init #객체지향
