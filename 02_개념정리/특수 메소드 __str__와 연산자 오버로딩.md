# 특수 메소드 __str__와 연산자 오버로딩

## 핵심 요약

특수 메소드는 Python이 특정 상황에서 자동으로 호출하는 메소드이다.

대표적으로 다음이 있다.

- `__str__`: 객체를 문자열로 표현할 때 호출
- `__add__`: 객체끼리 `+` 연산할 때 호출

---

## __str__

```python
def __str__(self):
    return f"Television(channel={self.channel}, volume={self.volume}, on={self.on})"
```

객체를 `print()`로 출력하면 `__str__`이 호출된다.

```python
print(tv1)
```

출력:

```text
Television(channel=1, volume=10, on=True)
```

---

## __add__

```python
def __add__(self, other):
    new_width = self.width + other.width
    new_height = self.height + other.height
    return Rectangle(new_width, new_height)
```

객체끼리 더하기를 할 때 호출된다.

```python
rect3 = rect1 + rect2
```

실제로는 이런 느낌이다.

```python
rect3 = rect1.__add__(rect2)
```

---

## 연산자 오버로딩

원래 `+`는 숫자끼리 더하거나 문자열을 붙이는 데 사용된다.

```python
1 + 2
"hello" + "world"
```

그런데 `__add__`를 직접 정의하면 내가 만든 객체에도 `+`의 의미를 부여할 수 있다.

```python
rect1 + rect2
```

이것을 연산자 오버로딩이라고 한다.

---

## 내 식으로 이해

특수 메소드는 Python이 “이 상황이면 이 함수를 부르면 되겠다” 하고 자동으로 찾아 쓰는 약속이다.

- `print(객체)` → `__str__`
- `객체 + 객체` → `__add__`

내가 직접 호출하지 않아도 특정 문법을 썼을 때 자동으로 실행되는 함수라고 보면 된다.

---

## 연결 노트

- [[객체와 클래스]]
- [[코드해설 - 0706 1.ipynb 객체지향]]

---

## 태그

#python #개념정리 #특수메소드 #str #add #연산자오버로딩
