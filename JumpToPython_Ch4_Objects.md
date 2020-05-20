# 파이썬 날개달기




## 클래스



### 클래스는 왜 필요한가?

클래스가 없어도 프로그램을 충분히 만들 수 있다.

하지만 프로그램을 작성할 때 클래스를 적재적소에 사용하면 프로그래머가 얻을 수 있는 이익은 상당하다.

계산기에 숫자 3을 입력하고 + 기호를 입력한 후 4를 입력하면 결괏값으로 7을 보여 준다. 다시 한 번 + 기호를 입력한 후 3을 입력하면 기존 결괏값 7에 3을 더해 10을 보여 준다. 즉 계산기는 이전에 계산한 결괏값을 항상 메모리 어딘가에 저장하고 있어야 한다.

계산기의 "더하기" 기능을 구현한 파이썬 코드는 다음과 같다.

```python
# add 함수는 매개변수 num에 받은 값을 이전에 계산한 결괏값에 더한 후 돌려주는 함수
result = 0
def add(num):
    global result
    result += num
    return result

print(add(3))           # 3
print(add(4))           # 7
```

만일 한 프로그램에서 2대의 계산기가 필요한 상황이 발생하면? 각 계산기는 각각의 결괏값을 유지해야 하기 때문에 `add` 함수 하나만으로는 결괏값을 따로 유지할 수 없다.

다음과 같이 함수를 각각 따로 만들어야 한다.

```python
# 각 함수에서 계산한 결괏값을 유지하면서 저장하는 전역 변수 result1, result2가 필요
result1 = 0
result2 = 0

def add1(num):
    global result1
    result1 += num
    return result1

def add2(num):
    global result2
    result2 += num
    return result2

print(add1(3))          # 3
print(add1(4))          # 7
print(add2(3))          # 3
print(add2(7))          # 10
```

계산기가 점점 더 많이 필요해진다면 어떻게 해야할까? 그 때마다 전역 변수와 함수를 추가할 것인가? 빼기나 곱하기 등의 기능을 추가해야 된다면 상황은 점점 더 어려워질 것이다.

위와 같은 경우에 클래스를 사용하면 다음과 같이 간단하게 해결할 수 있다.

```python
class Calculator:
    def __init__(self):
        self.result = 0

    def add(self, num):
        self.result += num
        return self.result

cal1 = Calculator()
cal2 = Calculator()

print(cal1.add(3))              # 3
print(cal1.add(4))              # 7
print(cal2.add(3))              # 3
print(cal2.add(7))              # 10
```

`Calculator` 클래스로 만든 별개의 계산기 `cal1`, `cal2`(파이썬에서는 이것을 **객체**라고 부른다)가 각각의 역할을 수행한다. 계산기 (`cal1`, `cal2`)의 결괏값 역시 다른 계산기의 결괏값과 상관없이 독립적인 값을 유지한다. 클래스를 사용하면 계산기 대수가 늘어나더라도 객체를 생성만 하면 되기 때문에 함수를 사용하는 경우와 달리 매우 간단해진다. 만약 빼기 기능을 더하려면 `Calculator` 클래스에 다음과 같은 빼기 기능 함수를 추가해 주면 된다.

```python
    def sub(self, num):
        self.result += num
        return self.result
```



### 클래스와 객체

![클래스와 객체](https://wikidocs.net/images/page/28/class_cookie.png)

* 과자 틀 → 클래스 (class)
* 과자 틀에 의해서 만들어진 과자 → 객체 (object)

클래스(class)란 똑같은 무엇인가를 계속해서 만들어 낼 수 있는 설계 도면이고(과자 틀), 객체(object)란 클래스로 만든 피조물(과자 틀을 사용해 만든 과자)을 뜻한다.

클래스로 만든 객체에는 중요한 특징이 있다. 바로 객체마다 고유한 성격을 가진다는 것이다. 과자 틀로 만든 과자에 구멍을 뚫거나 조금 베어 먹더라도 다른 과자에는 아무 영향이 없는 것과 마찬가지로 동일한 클래스로 만든 객체들은 서로 전혀 영향을 주지 않는다.

```python
# 아무 기능도 갖고 있지 않은 껍질뿐인 클래스
class Cookie:
    pass

# 껍질뿐인 클래스도 객체를 생성하는 기능이 있음
# 1개의 클래스는 무수히 많은 객체를 만들어 낼 수 있음
a = Cookie()
b = Cookie()
```


#### 객체와 인스턴스의 차이

클래스로 만든 객체를 인스턴스라고도 한다. `a = Cookie()` 이렇게 만든 `a`는 객체이다. 그리고 `a` 객체는 `Cookie`의 인스턴스이다. 즉 인스턴스라는 말은 특정 객체(`a`)가 어떤 클래스(`Cookie`)의 객체인지를 관계 위주로 설명할 때 사용한다. "`a`는 인스턴스"보다는 "`a`는 객체"라는 표현이 어울리며 "`a`는 `Cookie`의 객체"보다는 "`a`는 `Cookie`의 인스턴스"라는 표현이 훨씬 잘 어울린다.



### 사칙연산 클래스 만들기


#### 클래스를 어떻게 만들지 먼저 구상하기

```python
# a라는 객체를 만든다
a = FourCal()

# 숫자 4와 2를 a에 지정
a.setdata(4, 2)

# a.add(): 두 수를 합한 결과
# a.mul(): 두 수를 곱한 결과
# a.sub(): 두 수를 뺀 결과
# a.div(): 두 수를 나눈 결과
print(a.add())      # 6
print(a.mul())      # 8
print(a.sub())      # 2
print(a.div())      # 2
```


#### 클래스 구조 만들기

객체를 만들 수 있게 `pass`란 문장만을 포함한 `FourCal` 클래스를 만든다.

> `pass`는 아무것도 수행하지 않는 문법으로 임시로 코드를 작성할 때 주로 쓴다.

```python
class FourCal:
    pass

a = FourCal()
type(a)             # <class '__main__.FourCal'
```


#### 객체에 숫자 지정할 수 있게 만들기

`a` 객체에 사칙연산을 할 때 사용할 2개의 숫자를 먼저 알려주어야 한다. 연산을 수행할 대상을 객체에 지정할 수 있게 만들어 보자.

> 클래스 안에 구현된 함수는 다른 말로 **매서드**(Method)라고 부른다.

```python
class FourCal:
    def setdata(self, first, second):
        self.first = first
        self.second = second
```


##### (1) `setdata` 메서드의 매개변수

일반 함수와는 달리 메서드의 첫 번째 매개변수 `self`는 특별한 의미를 가진다.

> 객체를 통해 클래스의 메서드를 호출하려면 `a.setdata(4, 2)`와 같이 도트(`.`) 연산자를 사용해야 한다.

```python
a = FourCal()
a.setdata(4, 2)
```

`setdata`의 메서드에는 `self`, `first`, `second` 총 3개의 매개변수가 필요한데 실제로는 2개 값만 전달했다. 그 이유는 `a.setdata(4, 2)` 처럼 호출하면 `setdata` 메서드의 첫 번재 매개변수 `self`에는 `setdata` 메서드를 호출한 객체 `a`가 자동으로 전달되기 때문이다.

![setdata 메서드의 매개변수](https://wikidocs.net/images/page/12392/setdata.png)

파이썬 매서드의 첫 번째 매개변수 이름은 관례적으로 `self`를 사용한다. 객체를 호출할 때 호출한 객체 자신이 전달되기 때문에 `self`를 사용한 것이다. 다른 이름을 사용해도 상관없다.

> 메서드의 첫 번째 매개변수 `self`를 명시적으로 구현하는 것은 파이썬만의 독특한 특징이다. 예를 들어 자바 같은 언어는 첫 번째 매개변수 `self`가 필요없다.


##### (2) `setdata` 메서드의 수행문

```python
def setdata(self, first, second):
    self.first = first
    self.second = second
```

* 해석

```python
# a.setdata(4, 2)처럼 호출하면 setdata 메서드의 매개변수 first, second에는 각각 4와 2가 전달되어 다음과 같이 해석
self.first = 4
self.second = 2

# self는 전달된 객체 a이므로 다시 다음과 같이 해석
a.first = 4
a.second = 2
```

`a.first = 4` 문장이 수행되면 `a` 객체에 객체변수 `first`가 생성되고 값 4가 저장된다. `a.second = 2` 문장이 수행되면 `a` 객체에 객체변수 `second`가 생성되고 값 2가 저장된다.

> 객체에 생성되는 객체만의 변수를 객체변수라고 부른다.

```python
a = FourCal()
a.setdata(4, 2)
print(a.first)      # 4
print(a.second)     # 2
```

* `a`, `b` 객체 생성

`a` 객체의 `first` 값은 `b` 객체의 `first` 값에 영향받지 않고 원래 값을 유지하고 있다. **클래스로 만든 객체의 객체변수는 다른 객체의 객체변수에 상관없이 독립적인 값을 유지한다.** `a`객체의 `first` 주소 값과 `b` 객체의 `first` 주소 값이 서로 다르므로 각각 다른 곳에 저장된다는 것을 알 수 있다. 객체변수는 그 객체의 고유 값을 저장할 수 있는 공간이다.

> `id` 함수는 객체의 주소를 돌려주는 파이썬 내장 함수이다.

```python
a = FourCal()
b = FourCal()
a.setdata(4, 2)
print(a.first)      # 4
b.setdata(3, 7)
print(b.first)      # 3
print(a.first)      # 4
id(a.first)         # 140711486277376
id(b.first)         # 140711486277344
```

* 현재까지 완성된 `FourCal` 클래스

```python
class FourCal:
    def setdata(self, first, second):
        self.first = first
        self.second = second
```


#### 메서드의 또 다른 호출 방법

* 클래스를 통해 메서드를 호출하는 것도 가능
* `클래스 이름.메서드` 형태로 호출할 때는 객체 `a`를 첫 번째 매개변수 `self`에 꼭 전달해 주어야 함
* `객체.메서드` 형태로 호출할 때는 `self`를 반드시 생략해서 호출

```
python
a = FourCal()
FourCal.setdata(a, 4, 2)
a.setdata(4, 2)
```


#### 더하기 기능 만들기
```python
a = FourCal()
a.setdata(4, 2)
print(a.add())      # 6
```

* `add` 메서드 추가

```python
class FourCal:
    def setdata(self, first, second):
        self.first = first
        self.second = second
    def add(self):
        result = self.first + self.second
        return result

a = FourCal()
a.setdata(4, 2)
print(a.add())                      # 6
```

* 해석

```python
# add 메서드의 매개변수는 self이고 반환 값은 result
result = self.first + self.second

# a.add()와 같이 a 객체에 의해 add 메서드가 수행되면 add 메서드의 self에는 객체 a가 자동으로 입력
result = a.first + a.second

# a.setdata(4, 2)가 먼저 호출되어 a.first = 4, a.second = 2라고 이미 설정
result = 4 + 2

# a.add() 호출
print(a.add())                          # 6
```


#### 곱하기, 빼기, 나누기 기능 만들기

```python
class FourCal:
    def setdata(self, first, second):
        self.first = first
        self.second = second
    def add(self):
        result = self.first + self.second
        return result
    def mul(self):
        result = self.first * self.second
        return result
    def sub(self):
        result = self.first - self.second
        return result
    def div(self):
        result = self.first / self.second
        return result

a = FourCal()
b = FourCal()
a.setdata(4, 2)
b.setdata(3, 8)
print(a.add())                      # 6
print(a.mul())                      # 8
print(a.sub())                      # 2
print(a.div())                      # 2
print(a.add())                      # 11
print(a.mul())                      # 24
print(a.sub())                      # -5
print(a.div())                      # 0.375
```



### 생성자 (Constructor)

```python
# FourCal 클래스 사용
a = FourCal()
a.add()             # AttributeError
```

`FourCal` 클래스의 인스턴스 `a`에 `setdata` 메서드를 수행하지 않고 `add` 메서드를 수행하면 "AttributeError: 'FourCal' object has no attribute 'first'" 오류가 발생한다. `setdata` 메서드를 수행해야 객체 `a`의 객체변수 `first`와 `second`가 생성되기 때문이다.

이렇게 객체에 초깃값을 설정해야 할 필요가 있을 때는 `setdata`와 같은 메서드를 호출하여 초깃값을 설정하기보다는 생성자를 구현하는 것이 안전한 방법이다. 생성자(Constructor)란 **객체가 생성될 때 자동으로 호출되는 메서드를 의미**한다.

파이썬 메서드 이름으로 `__init__`를 사용하면 이 메서드는 생성자가 된다.

```python
class FourCal:
    def __init__(self, first, second):
        self.first = first
        self.second = second
    def setdata(self, first, second):
        self.first = first
        self.second = second
    def add(self):
        result = self.first + self.second
        return result
    def mul(self):
        result = self.first * self.second
        return result
    def sub(self):
        result = self.first - self.second
        return result
    def div(self):
        result = self.first / self.second
        return result

a = FourCal()                               # TypeError
a = FourCal(4, 2)
print(a.first)                              # 4
print(a.second)                             # 2
a.add()                                     # 6
a.div()                                     # 2.0
```

오류가 발생한 이유는 매개변수 `first`와 `second`에 해당하는 값이 전달되지 않았기 때문이다.



### 클래스의 상속

클래스를 상속하기 위해서는 다음처럼 클래스 이름 뒤 괄호 안에 상속할 클래스 이름을 넣어주면 된다.

```python
class 클래스 이름(상속할 클래스 이름)
```

상속(Inheritance)이란 "물려받다"라는 뜻으로, 상속 개념을 사용하여 FourCal 클래스에 ab을 구할 수 있는 기능을 추가해 보자.

```python
class MoreFourCal(FourCal):
    pass
```

`MoreFourCal` 클래스는 `FourCal` 클래스를 상속했으므로 `FourCal` 클래스의 모든 기능을 사용할 수 있다.

> 보통 상속은 기존 클래스를 변경하지 않고 기능을 추가하거나 기존 기능을 변경하려고 할 때 사용한다. "클래스에 기능을 추가하고 싶으면 기존 클래스를 수정하면 되는데 왜 굳이 상속을 받아서 처리해야 하지?" 라는 의문이 들 수도 있다. 하지만 기존 클래스가 라이브러리 형태로 제공되거나 수정이 허용되지 않는 상황이라면 상속을 사용해야 한다.

```python
class MoreFourCal(FourCal):
    def pow(self):
        result = self.first ** self.second
        return result

a = MoreFourCal(4, 2)
a.pow()                         # 16
```



### 메서드 오버라이딩

`FourCal` 클래스의 객체 `a`에 4와 0 값을 설정하고 `div` 메서드를 호출하면 4를 0으로 나누려고 하기 때문에 ZeroDivisionError가 발생한다. 하지만 0으로 나눌 때 오류가 아닌 0을 돌려주도록 만들고 싶다면 어떻게 해야 할까?

```python
a = FourCal(4, 0)
a.div()                             # ZeroDivisionError

class SafeFourCal(FourCal):
    def div(self):
        if self.second == 0:
            return 0
        else:
            return self.first / self.second

a = SafeFourCal(4, 0)
a.div                               # 0
```

`SafeFourCal` 클래스는 `FourCal` 클래스에 있는 `div` 메서드를 동일한 이름으로 다시 작성하였다. 이렇게 부모 클래스(상속한 클래스)에 있는 메서드를 동일한 이름으로 다시 만드는 것을 **메서드 오버라이딩**(Overriding, 덮어쓰기)이라고 한다. 이렇게 매서드를 오버라이딩하면 부모클래스의 메서드 대신 오버라이딩한 메서드가 호출된다.

`SafeFourCal` 클래스에 오버라이딩한 `div` 메서드는 나누는 값이 0인 경우에는 0을 돌려주도록 수정했다.



### 클래스 변수

클래스 변수는 `클래스이름.클래스 변수`로 사용할 수 있다. 또는 `Family` 클래스로 만든 객체를 통해서도 클래스 변수를 사용할 수 있다.

```python
class Family:
    lastname = "김"

print(Family.lastname)      # 김

a = Family()
b = Family()
print(a.lastname)           # 김
print(b.lastname)           # 김
```

클래스 변수는 클래스로 만든 모든 객체에 공유된다는 특징이 있다.

```python
Family.lastname = "박"
print(a.lastname)           # 박
print(b.lastname)           # 박
id(Family.lasname)          # 2793533478592
id(a.lastname)              # 2793533478592
id(b.lastname)              # 2793533478592
```

클래스에서 클래스 변수보다는 객체변수가 훨씬 중요하다. 실무 프로그래밍을 할 때도 클래스 변수보다는 객체변수를 사용하는 비율이 훨씬 높다.




## 모듈

모듈이란 함수나 변수 또는 클래스를 모아 놓은 파일이다.



### 모듈 만들기

```python
# mod1.py
def add(a, b):
    return a + b

def sub(a, b):
    return a - b
```

이 mod1.py 파일이 바로 모듈이다.

> 파이썬 확장자 .py로 만든 파이썬 파일은 모두 모듈이다.



### 모듈 불러오기

```python
import mod1                 # import mod1.py로 입력하지 않도록 주의
print(mod1.add(3, 4))       # 7
print(mod1.sub(4, 2))       # 2
```

`import`는 이미 만들어 놓은 파이썬 모듈을 사용할 수 있게 해주는 명령어이다.

```python
import 모듈이름

# 모듈 이름 없이 함수 이름만 쓰고 싶은 경우
from 모듈이름 import 모듈함수
```

```python
from mod1 import add
add(3, 4)                   # 7
```

`add` 함수와 `sub` 함수를 둘 다 사용하고 싶다면 어떻게 해야 할까?

```python
# 콤마로 구분
from mod1 import add, sub

# * 문자 사용 (모든 것)
from mod1 import *
```

> `import`는 현재 디렉터리에 있는 파일이나 파이썬 라이브러리가 저장된 디렉터리에 있는 모듈만 불러올 수 있다. 파이썬 라이브러리는 파이썬을 설치할 때 자동으로 설치되는 파이썬 모듈을 말한다.



### `if __name__ == "__main__"`: 의 의미

```python
# mod1.py
def add(a, b):
    return a + b

def sub(a, b):
    return a - b

print(add(1, 4))
print(sub(4, 2))
```

mod1.py 파일의 `add` 함수와 `sub` 함수를 사용하기 위해 `mod1` 모듈을 import할 때는 좀 이상한 문제가 생긴다. `import mod1`을 수행하는 순간 `mod1.py`가 실행이 되어 결괏값을 출력한다.

이러한 문제를 방지하려면 mod1.py 파일을 다음처럼 변경해야 한다.

```python
# mod1.py

def add(a, b):
    return a + b

def sub(a, b):
    return a - b

if __name__ == "__main__":
    print(add(1, 4))
    print(sub(4, 2))
```

`if __name__ == "__main__":`을 사용하면 직접 이 파일을 실행했을 때는 참이 되어 `if`문 다음 문장이 수행된다. 반대로 대화형 인터프리터나 다른 파일에서 이 모듈을 불러서 사용할 때는 거짓이 되어 `if` 문 다음 문장이 수행되지 않는다.


#### `__name__` 변수란?

파이썬의 `__name__` 변수는 파이썬이 내부적으로 사용하는 특별한 변수 이름이다. 직접 파일을 실행할 경우 mod1.py의 `__name__` 변수에는 `__main__` 값이 저장된다. 하지만 파이썬 셸이나 다른 파이썬 모듈에서 `mod1`을 import 할 경우에는 `__name__` 변수에는 `mod1`이 저장된다.



### 클래스나 변수 등을 포함한 모듈

```python
# mod2.py
PI = 3.141592

class Math:
    def solv(self, r):
        return PI * (r ** 2)

def add(a, b):
    return a + b
```

* 모듈 사용 (대화형 인터프리터)

```python
# mod2.py 파일에 있는 PI 변수 값 사용
import mod2
print(mod2.PI)                      # 3.0141592

# mod2.py에 있는 Math 클래스 사용: "."(도트 연산자)로 클래스 이름 앞에 모듈 이름을 먼저 입력
a = mod2.Math()
print(a.solv(2))                    # 12.566368

# mod2.py에 있는 add 함수 사용
print(mod2.add(mod2.PI, 4.4))       # 7.541592
```



### 다른 파일에서 모듈 불러오기

대화형 인터프리터에서 한 것과 마찬가지 방법이다.

```python
# modtest.py
import mod2
result = mod2.add(3, 4)
print(result)               # 7
```


#### 모듈을 불러오는 또 다른 방법

* 모듈을 저장한 디렉터리로 이동하지 않고 모듈을 불러와서 사용하는 방법

##### 1. `sys.path.append`(모듈을 저장한 디렉터리) 사용하기

```python
import sys
sys.path.append("C:/doit/mymod")

import mod2
print(mod2.add(3, 4))                   # 7
```

##### 2. PYTHONPATH 환경 변수 사용하기

```
set PYTHONPATH=C:\doit\mymod
```

```python
import mod2
print(mod2.add(3, 4))       # 7
```




## 패키지



### 패키지란 무엇인가?

패키지(Packages)는 도트(`.`)를 사용하여 파이썬 모듈을 계층적(디렉터리 구조)으로 관리할 수 있게 해준다.

파이썬 패키지는 디렉터리와 파이썬 모듈로 이루어지며 구조는 다음과 같다.

*가상의 game 패키지 예*

```
game/
    __init__.py
    sound/
        __init__.py
        echo.py
        wav.py
    graphic/
        __init__.py
        screen.py
        render.py
    play/
        __init__.py
        run.py
        test.py
```

* game: 패키지의 루트 디렉터리
* sound, graphic, play: 서브 디렉터리

패키지 구조로 모듈을 만들면 다른 모듈과 이름이 겹치더라도 더 안전하게 사용할 수 있다.



### 패키지 만들기


#### 패키지 기본 구성 요소 준비하기

1. `C:/doit` 디렉터리 밑에 game 및 기타 서브 디렉터리를 생성하고 .py 파일들을 다음과 같이 만들어 보자.

   ```
   C:/doit/game/__init__.py
   ```

   ```
   C:/doit/game/sound/__init__.py
   ```

   ```
   C:/doit/game/sound/echo.py
   ```

   ```
   C:/doit/game/graphic/__init__.py
   ```

   ```
   C:/doit/game/graphic/render.py
   ```

2. 각 디렉터리에 `__init__.py` 파일을 만들어 놓기만 하고 내용은 일단 비워 둔다.

3. echo.py 파일은 다음과 같이 만든다.

   ```python
   # echo.py
   def echo_test():
       print("echo")
   ```

4. render.py 파일은 다음과 같이 만든다.

   ```python
   # render.py
   def render_test():
       print("render")
   ```

5. 다음 예제를 수행하기 전에 game 패키지를 참조할 수 있도록 명령 프롬프트 창에서 set 명령어로 `PYTHONPATH` 환경 변수에 `C:/doit` 디렉터리를 추가한다. 그리고 파이썬 인터프리터를 실행한다.



### 패키지 안의 함수 실행하기

* `echo` 모듈을 import하여 실행하는 방법

```python
import game.sound.echo
game.sound.echo.echo_test()                 # echo
```

* `echo` 모듈이 있는 디렉터리까지를 `from ... import` 하여 실행하는 방법

```python
from game.sound import echo
echo.echo_test()                            # echo
```

* `echo` 모듈의 `echo_test` 함수를 직접 import하여 실행하는 방법

```python
from game.sound.echo import echo_test
echo_test()                                 # echo
```


#### 불가능

* `import game`을 수행하면 game 디렉터리의 모듈 또는 game 디렉터리의 `__init__.py`에 정의한 것만 참조할 수 있음

```python
import game
game.sound.echo.echo_test()             # AttributeError
```

* 도트 연산자(`.`)를 사용해서 `import a.b.c`처럼 import할 때 가장 마지막 항목은`c`는 반드시 모듈 또는 패키지여야만 함

```python
import game.sound.echo.echo_test        # ImportError
```



### `__init__.py`의 용도

해당 디렉터리가 패키지의 일부임을 알려주는 역할을 한다. 패키지에 포함된 디렉터리에 `__init__.py` 파일이 없다면 패키지로 인식되지 않는다.

> python3.3 버전 부터는 `__init__.py` 파일이 없어도 패키지로 인식한다(PEP 420, Implicit Namespace Package). 하지만 하위 버전 호환을 위해 `__init__.py` 파일을 생성하는 것이 안전한 방법이다.

```python
from game.sound import *
echo.echo_test()                # NameError
```

특정 디렉터리의 모듈을 `*`을 사용하여 import할 때에는 다음과 같이 해당 디렉터리의 `__init__.py` 파일에 `__all__` 변수를 설정하여 import할 수 있는 모듈을 정의해 주어야 한다.

```python
# C:/doit/game/sound/__init__.py
__all__ = ['echo']
```

`__all__`이 의미하는 것은 sound 디렉터리에서 `*` 기호를 사용하여 import할 경우 이곳에 정의된 `echo` 모듈만 import된다는 의미이다.

> `from game.sound.echo import *`는 `__all__`과 상관없이 무조건 import된다. `__all__`과 상관없이 무조건 import되는 경우는 `from a.b.c import *`에서 from의 마지막 항목인 `c`가 모듈인 경우이다.

```python
from game.sound import *
echo.echo_test()                # echo
```



### `relative` 패키지

graphic 디렉터리의 render.py 모듈이 sound 디렉터리의 echo.py 모듈을 사용하고 싶다면 어떻게 해야 할까?

```python
# render.py
from game.sound.echo import echo_test
def render_test():
    print("render")
    echo_test()
```

* 수행

```python
from game.graphic.render import render_test
render_test()

    # render
    # echo
```

`from game.sound.echo import echo_test`를 입력해 전체 경로를 사용하여 import할 수도 있지만 다음과 같이 relative하게 import하는 것도 가능

```python
# render.py
from ..sound.echo import echo_test
def render_test():
    print("render")
    echo_test()
```

`..`은 부모 디렉터리를 의미한다. graphic과 sound 디렉터리는 동일한 깊이(depth)이므로 부모 디렉터리(`..`)를 사용하여 import가 가능한 것이다.

* relative한 접근자
  - `..` - 부모 디렉터리
  - `.` - 현재 디렉터리

`..`과 같은 relative한 접근자는 render.py처럼 모듈 안에서만 사용해야 한다. 파이썬 인터프리터에서 relative한 접근자를 사용하면 "SystemError: cannot perform relative import" 오류가 발생한다.




## 예외 처리



### 오류는 어떤 때 발생하는가?

* 디렉터리 안에 없는 파일을 열려고 시도했을 때 발생하는 오류

```python
f = open("나없는파일", 'r')
```

```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
FileNotFoundError: [Errno 2] No such file or directory: '나없는파일'
```

* 0으로 다른 숫자를 나누는 경우

```python
4 / 0
```

```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ZeroDivisionError: division by zero
```

* 리스트에서 얻을 수 없는 값

```python
a = [1, 2, 3]
a[4]
```

```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
```



### 오류 예외 처리 기법


#### `try`, `except`문

```python
try:
    ...
except [발생 오류[as 오류 메시지 변수]]:
    ...
```

##### 1. `try`, `except`만 쓰는 방법

오류 종류에 상관없이 오류가 발생하면 `except` 블록을 수행한다.

```python
try:
    ...
except:
    ...
```

##### 2. 발생 오류만 포함한 `except`문

오류가 발생했을 때 `except`문에 미리 정해 놓은 오류 이름과 일치할 때만 `except` 블록을 수행한다는 뜻이다.

```python
try:
    ...
except 발생 오류:
    ...
```

##### 3. 발생 오류와 오류 메시지 변수까지 포함한 `except`문

```python
try:
    ...
except 발생 오류 as 오류 메시지 변수:
    ...

# 예
try:
    4 / 0
except ZeroDivisionError as e:
    print(e)                        # division by zero
```


#### `try` .. `finally`

`finally`절은 `try`문 수행 도중 예외 발생 여부에 상관없이 항상 수행된다. 보통 `finally`절은 사용한 리소스를 close해야 할 때에 많이 사용한다.

```python
f = open('foo.txt', 'w')
try:
    # 무언가를 수행한다.
finally:
    f.close()
```

foo.txt 파일을 쓰기 모드로 연 후에 `try`문을 수행한 후 예외 발생 여보와 상관없이 `finally`절에서 `f.close()`로 열린 파일을 닫을 수 있다.


#### 여러개의 오류처리하기

```python
try:
    ...
except 발생 오류1:
    ...
except 발생 오류2:
    ...
```

0으로 나누는 오류와 인덱싱 오류를 다음과 같이 처리할 수 있다.

```python
try:
    a = [1, 2]
    print(a[3])
    4 / 0
except ZeroDivisionError:
    print("0으로 나눌 수 없습니다.")
except IndexError:
    print("인덱싱 할 수 없습니다.")

    # 인덱싱 할 수 없습니다.
```

인덱싱 오류가 먼저 발생했으므로 ZeroDivisionError 오류는 발생하지 않았다.

오류 메시지도 가져올 수 있다.

```python
try:
    a = [1, 2]
    print(a[3])
    4 / 0
except ZeroDivisionError as e:
    print(e)
except IndexError as e:
    print(e)

    # list index out of range
```

2개 이상의 오류를 동시에 처리하기 위해서는 괄호를 사용하여 함께 묶어 처리하면 된다.

```python
try:
    a = [1, 2]
    print(a[3])
    4 / 0
except (ZeroDivisionError, IndexError) as e:
    print(e)
```



### 오류 회피하기

특정 오류가 발생할 경우 그냥 통과시켜야 할 때가 있다.

* `pass`를 사용하여 오류를 그냥 회피하도록 작성

```python
try:
    f = open("나없는파일", 'r')
except FileNotFoundError:
    pass
```



### 오류 일부러 발생시키기

파이썬은 `raise` 명령어를 사용해 오류를 강제로 발생시킬 수 있다.

> NotImplementedError는 파이썬 내장 오류로, 꼭 작성해야 하는 부분이 구현되지 않았을 경우 일부러 오류를 일으키기 위해 사용한다.

```python
# Bird 클래스를 상속받는 자식 클래스는 반드시 fly라는 함수를 구현하도록 만들고 싶은 경우
class Bird:
    def fly(self):
        raise NotImplementedError
```

* 자식 클래스가 `fly` 함수를 구현하지 않은 상태로 `fly` 함수를 호출한다면?

```python
class Eagle(Bird):
    pass

eagle = Eagle()
eagle.fly()         # NotImplementedError
```

* NotImplementedError가 발생되지 않게 하려면 `Eagle` 클래스에 `fly` 함수를 반드시 구현

```python
class Eagle(Bird):
    def fly(self):
        print("very fast")

eagle = Eagle()
eagle.fly                       # very fast
```



### 예외 만들기

프로그램 수행 도중 특수한 경우에만 예외 처리를 하기 위해서 종종 예외를 만들어서 사용한다. 예외는 파이썬 내장 클래스인 `Exception` 클래스를 상속하여 만들 수 있다.

```python
class MyError(Exception):
    pass

# 별명을 출력해주는 함수
def say_nick(nick):
    if nick == '바보':
        raise MyError()
    print(nick)

say_nick("천사")
say_nick("바보")
```

```
천사
Traceback (mpost recent call last):
  File "...", line 11, in <module>
    say_nick("바보")
  File "...", line 7, in say_nick
    raise MyError()
__main__.MyError
```

예외 처리 기법을 이용하여 MyError 발생을 예외 처리해 보자.

```python
try:
    say_nick("천사")
    say_nick("바보")
except MyError:
    print("허용되지 않는 별명입니다.")
```

```
천사
허용되지 않는 별명입니다.
```

오류 메시지를 사용하고 싶다면 다음처럼 예외 처리를 하면 된다.

```python
# 오류 메시지를 출력했을 때 오류 메시지가 보이게 하려면 오류 클래스에 __sfr__ 메서드를 구현
class MyError(Exception):
    def __str__(self):
        return "허용되지 않는 별명입니다."

try:
    say_nick("천사")
    say_nick("바보")
except MyError as e:
    print(e)
```

```
천사
허용되지 않는 별명입니다.
```




## 내장 함수



### `abs`

```python
# 어떤 숫자를 입력받았을 때, 그 숫자의 절댓값을 돌려주는 함수
abs(3)          # 3
abs(-3)         # 3
abs(-1.2)       # 1.2
```



### `all`

```python
# 반복 가능한(iterable) 자료형 x를 입력 인수로 받음
# 이 x가 모두 참이면 True, 거짓이 하나라도 있으면 False
all([1, 2, 3])          # True
all([1, 2, 3, 0])       # False
```



### `any`

```python
# x 중 하나라도 참이 있으면 True, x가 모두 거짓일 때에만 False
# all(x)의 반대
any([1, 2, 3, 0])       # True
any([0, ""])            # False
```



### `chr`

```python
# 아스키(ASCII) 코드 값을 입력받아 그 코드에 해당하는 문자를 출력하는 함수
chr(97)     # 'a'
chr(48)     # '0'
```



### `dir`

```python
# 객체가 자체적으로 가지고 있는 변수나 함수를 보여줌
dir([1, 2, 3])
    # ['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
dir({'1': 'a'})
    # ['__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'clear', 'copy', 'fromkeys', 'get', 'items', 'keys', 'pop', 'popitem', 'setdefault', 'update', 'values']
```



### `divmod`

```python
# divmod(a, b)는 a를 b로 나눈 몫과 나머지를 튜플 형태로 돌려주는 함수
divmod(7, 3)        # (2, 1)
7 // 3              # 2
7 % 3               # 1
```



### `enumerate`

> 보통`enumerate` 함수는 `for`문과 함께 자주 사용

```python
# 순서가 있는 자료형(리스트, 튜플, 문자열)을 입력으로 받음
# 인덱스 값을 포함하는 enumerate 객체를 돌려줌
for i, name in enumerate(['body', 'foo', 'bar']):
    print(i, name)

    # 0 body
    # 1 foo
    # 2 bar
```



### `eval`

```python
# 실행 가능한 문자열을 입력으로 받아 문자열을 실행한 결괏값을 돌려주는 함수
# 입력받은 문자열로 파이썬 함수나 클래스를 동적으로 실행하고 싶을 때 사용
eval('1+2')             # 3
eval("'hi' + 'a'")      # 'hia'
eval('divmod(4, 3)')    # (1, 1)
```



### `filter`

```python
# 첫 번째 인수로 함수 이름을, 두 번째 인수로 함수에 차례로 들어갈 반복 가능한 자료형을 받음
# 두 번째 인수가 첫 번째 인수에 입력되었을 때 반환 값이 참인 것만 묶어서 돌려줌
# positive.py
def positive(l):
    result = []
    for i in l:
        if i > 0:
            result.append(i)
    return result

print(positive([1, -3, 2, 0, -5, 6]))       # [1, 2, 6]

# filter 함수를 사용
# filter1.py
def positive(x):
    return x > 0

print(list(filter(positive, [1, -3, 2, 0, -5, 6])))
    # [1, 2, 6]

# lambda를 사용
list(filter(lambda x: x > 0, [1, -3, 2, 0, -5, 6]))
    # [1, 2, 6]
```



### `hex`

```python
# 정수 값을 입력받아 16진수(hexadecimal)로 변환하여 돌려주는 함수
hex(234)        # '0xea'
hex(3)          # '0x3'
```



### `id`

```python
# 객체를 입력받아 객체의 고유 주소 값(레퍼런스)을 돌려주는 함수
a = 3
id(3)       # 140728627414752
id(a)       # 140728627414752
b = a
id(b)       # 140728627414752
id(4)       # 140728627414784
```



### `input`

```python
# 사용자 입력을 받는 함수
a = input()
    # hi
a                           # 'hi'
b = input("Enter: ")
    # Enter: hi
b                           # 'hi'
```



### `int`

```python
# 문자열 형태의 숫자나 소수점이 있는 숫자 등을 정수 형태로 돌려주는 함수
# 정수를 입력으로 받으면 그대로 돌려줌
int('3')            # 3
int(3.4)            # 3

# int(x, radix): radix 진수로 표현된 문자열 x를 10진수로 변환하여 돌려줌
int('11', 2)        # 3
int('1A', 16)       # 26
```



### `isinstance`

```python
# 첫 번째 인수로 인스턴스, 두 번째 인수로 클래스 이름을 받음
# 입력으로 받은 인스턴스가 그 클래스의 인스턴스인지를 판단하여 참이면 True, 거짓이면 False
class Person: pass
...
a = Person()
isinstance(a, Person)       # True
b = 3
isinstance(b, Person)       # False
```



### `len`

```python
# 입력값의 길이(요소의 전체 개수)를 돌려주는 함수
len("python")       # 6
len([1, 2, 3])      # 3
len((1, 'a'))       # 2
```



### `list`

```python
# 반복 가능한 자료형을 입력받아 리스트로 만들어 돌려주는 함수
list("python")      # ['p', 'y', 't', 'h', 'o', 'n']
list((1, 2, 3))     # [1, 2, 3]
a = [1, 2, 3]
b = list(a)
b                   # [1, 2, 3]
```



### `map`

```python
# 함수(f)와 반복 가능한(interable) 자료형을 입력으로 받음
# 입력받은 자료형의 각 요소를 함수 f가 수행한 결과를 묶어서 돌려주는 함수
# two_times.py
def two_times(numberList):
    result = []
    for number in numberList:
        result.append(number*2)
    return result

result = two_times([1, 2, 3, 4])
print(result)                               # [2, 4, 6, 8]

# map 함수 사용
def two_times(x):
    return x*2

list(map(two_times, [1, 2, 3, 4]))          # [2, 4, 6, 8]

# lambda 사용
list(map(lambda a: a*2, [1, 2, 3, 4]))      # [2, 4, 6, 8]
```



### `max`

```python
# 인수로 반복 가능한 자료형을 입력받아 그 최댓값을 돌려주는 함수
max([1, 2, 3])      # 3
max("python")       # 'y'
```



### `min`

```python
# 인수로 반복 가능한 자료형을 입력받아 그 최솟값을 돌려주는 함수
min([1, 2, 3])      # 1
min("python")       # 'h'
```



### `oct`

```python
# 정수 형태의 숫자를 8진수 문자열로 바꾸어 돌려주는 함수
oct(34)         # '0o42'
oct(12345)      # '0o30071'
```



### `open`

| mode | 설명                      |
| ---- | ------------------------- |
| `w`  | 쓰기 모드로 파일 열기     |
| `r`  | 읽기 모드로 파일 열기     |
| `a`  | 추가 모드로 파일 열기     |
| `b`  | 바이너리 모드로 파일 열기 |

```python
# "파일 이름"과 "읽기 방법"을 입력받아 파일 객체를 돌려주는 함수
# 읽기 방법(mode)을 생략하면 기본값인 읽기 전용 모드(r)로 파일 객체를 만들어 돌려줌
# b는 w, r, a와 함께 사용
f = open("binary_file", "rb")

# fread와 fread2는 동일한 방법 (기본값으로 읽기 모드 r을 갖게 됨)
fread = open("read_mode.txt", 'r')
fread2 = open("read_mode.txt")

# 추가 모드로 파일 열기
fappend = open("append_mode.txt", 'a')
```



### `ord`

```python
# 문자의 아스키 코드 값을 돌려주는 함수
# chr 함수와 반대
ord('a')        # 97
ord('0')        # 48
```



### `pow`

```python
# pow(x, y)는 x의 y 제곱한 결괏값을 돌려주는 함수
pow(2, 4)       # 16
pow(3, 3)       # 27
```



### `range`

```python
# 입력받은 숫자에 해당하는 범위 값을 반복 가능한 객체로 만들어 돌려줌
# for문과 함께 자주 사용하는 함수

# 1. 인수가 하나일 경우: 0부터 시작
list(range(5))              # [0, 1, 2, 3, 4]

# 2. 인수가 2개일 경우: 시작 숫자와 끝 숫자, 끝 숫자는 해당 범위에 포함되지 않음
list(range(5, 10))          # [5, 6, 7, 8, 9]

# 3. 인수가 3개일 경우: 세 번째 인수는 숫자 사이의 거리
list(range(1, 10, 2))       # [1, 3, 5, 7, 9]
list(range(0, -10, -1))     # [0, -1, -2, -3, -4, -5, -6, -7, -8, -9]
```



### `round`

```python
# 숫자를 입력받아 반올림해 주는 함수
round(4.6)          # 5
round(4.2)          # 4

# 두 번째 매개변수는 반올림하여 표시하고 싶은 소수점의 자릿수(ndigits)
round(5.678, 2)     # 5.68
```



### `sorted`

```python
# 입력값을 정렬한 후 그 결과를 리스트로 돌려주는 함수
sorted([3, 1, 2])           # [1, 2, 3]
sorted(['a', 'c', 'b'])     # ['a', 'b', 'c']
sorted("zero")              # ['e', 'o', 'r', 'z']
sorted((3, 2, 1))           # [1, 2, 3]
```

> 리스트 자료형에도 `sort` 함수가 있지만 리스트 객체 그 자체를 정렬만 할 뿐 정렬된 결과를 돌려주지는 않음



### `str`

```python
# 문자열 형태로 객체를 변환하여 돌려주는 함수
str(3)                  # '3'
str('hi')               # 'hi'
str('hi'.upper())       # 'HI'
```



### `sum`

```python
# 입력받은 리스트나 튜플의 모든 요소의 합을 돌려주는 함수
sum([1, 2, 3])      # 6
sum((4, 5, 6))      # 15
```



### `tuple`

```python
# 반복 가능한 자료형을 입력받아 튜플 형태로 바꾸어 돌려주는 함수
tuple("abc")            # ('a', 'b', 'c')
tuple([1, 2, 3])        # (1, 2, 3)
tuple((1, 2, 3))        # (1, 2, 3)
```



### `type`

```python
# 입력값의 자료형이 무엇인지 알려 주는 함수
type("abc")                 # <class 'str'>
type([])                    # <class 'list'>
type(open("test", 'w'))     # <class '_io.TextIOWrapper'>
```



### `zip`

```python
# 동일한 개수로 이루어진 자료형을 묶어 주는 역할을 하는 함수
list(zip([1, 2, 3], [4, 5, 6]))     # [(1, 4), (2, 5), (3, 6)]
list(zip([1, 2, 3], [4, 5, 6], [7, 8, 9]))
    # [(1, 4, 7), (2, 5, 8), (3, 6, 9)]
list(zip("abc", "def"))             # [('a', 'd'), ('b', 'e'), ('c', 'f')]
```




## 외장 함수



### `sys`

* 파이썬 인터프리터가 제공하는 변수와 함수를 직접 제어할 수 있게 해주는 모듈


#### 명령 행에서 인수 전달하기 - `sys.argv`

명령 프롬프트 창에서 뒤에 다른 값을 함께 넣어 주면 `sys.argv` 리스트에 그 값이 추가됨

```
C:/User/home> python test.py abc pey guido
```

```python
# argv_test.py
import sys
print(sys.argv)
```

`python` 명령어 뒤의 모든 것들이 공백을 기준으로 나뉘어서 `sys.argv` 리스트의 요소가 됨

```
C:/doit/Mymod> python argv_test.py you need python
['argv_test.py', 'you', 'need', 'python']
```


#### 강제로 스크립트 종료하기 - `sys.exit`

프로그램 파일 안에서 사용하면 프로그램을 중단

```python
sys.exit()
```


#### 자신이 만든 모듈 불러와 사용하기 - `sys.path`

`sys.path`는 파이썬 모듈들이 저장되어 있는 위치를 나타냄

```python
import sys
sys.path
    # ['', 'C:\\Program Files\\Python38\\Lib\\idlelib', 'C:\\Program Files\\Python38\\python38.zip', 'C:\\Program Files\\Python38\\DLLs', 'C:\\Program Files\\Python38\\lib', 'C:\\Program Files\\Python38', 'C:\\Program Files\\Python38\\lib\\site-packages']
```

`sys.path.append`를 사용해 경로 이름을 추가할 수 있음

```python
# C:/doit/mymod 디렉터리에 있는 파이썬 모듈을 불러와서 사용할 수 있음
# path_append.py
import sys
sys.path.append("C:/doit/mymod")
```



### `pickle`

* 객체의 형태를 그대로 유지하면서 파일에 저장하고 불러올 수 있게 하는 모듈
* 어떤 자료형이든 저장하고 불러올 수 있음

```python
# pickle 모듈의 dump 함수를 사용하여 딕셔너리 객체인 data를 그대로 파일에 저장하는 방법
import pickle
f = open("test.txt", 'wb')
data = {1: 'python', 2: 'you need'}
pickle.dump(data, f)
f.close()

# pickle.load를 사용하여 원래 있던 딕셔너리 객체(data) 상태 그대로 불러오는 예
import pickle
f = open("test.txt", 'rb')
data = pickle.load(f)
print(data)                             # {2: 'you need', 1: 'python'}
```



### `os`

* 환경 변수나 디렉터리, 파일 등의 OS 자원을 제어할 수 있게 해주는 모듈


#### 내 시스템의 환경 변수 값을 알고 싶을 때 - `os.environ`

```python
import os
os.environ
    # environ({'ALLUSERSPROFILE': 'C:\\ProgramData', 'APPDATA': ... (생략)

# 돌려받은 객체가 딕셔너리이기 때문에 다음과 같이 호출 가능
os.environ['PATH']
    # 'C:\\Program Files\\Python38\\Scripts\\; ... (생략)
```


#### 디렉터리 위치 변경하기 - `os.chdir`

```python
os.chdir("C:\WINDOWS")
```


#### 디렉터리 위치 돌려받기 - `os.getcwd`

```python
os.getcwd()     # 'C:\WINDOWS'
```


#### 시스템 명령어 호출하기 - `os.system`

```python
# 현재 디렉터리에서 시스템 명령어 dir을 싱행하는 예
os.system("dir")
```


#### 실행한 시스템 명령어의 결괏값 돌려받기 - `os.popen`

```python
# 시스템 명령어를 실행한 결괏값을 읽기 모드 형태의 파일 객체로 돌려줌
f = os.popen("dir")

# 읽어 들은 파일 객체의 내용을 보기
print(f.read())
```


#### 기타 유용한 os 관련 함수

| 함수                  | 설명                                                            |
| --------------------- | --------------------------------------------------------------- |
| `os.mkdir(디렉터리)`  | 디렉터리를 생성한다.                                            |
| `os.rmdir(디렉터리)`  | 디렉터리를 삭제한다. 단, 디렉터리가 비어있어야 삭제가 가능하다. |
| `os.unlink(파일)`     | 파일을 지운다.                                                  |
| `os.rename(src, dst)` | `src`라는 이름의 파일을 `dst`라는 이름으로 바꾼다.              |



### `shutil`

* 파일을 복사해 주는 파이썬 모듈

```python
# src라는 이름의 파일을 dst로 복사
# dst가 디렉터리 이름이라면 src라는 파일 이름으로 dst 디렉터리에 복사
# 동일한 파일 이름이 있을 경우에는 덮어씀
import shutil
shutil.copy("src.txt", "dst.txt")
```



### `glob`

* 파일을 읽고 쓰는 기능이 있는 프로그램을 만들다 보면 특정 디렉터리에 있는 파일 이름 모두를 알아야 할 때 사용하는 모듈


#### 디렉터리에 있는 파일들을 리스트로 만들기 - `glob(pathname)`

```python
# C:/doit 디렉터리에 있는 파일 중 이름이 mark로 시작하는 파일을 모두 찾아서 읽어들이는 예
import glob
glob.glob("c:/doit/mark*")
    # ['c:/doit\\marks1.py', 'c:/doit\\marks2.py', 'c:/doit\\marks3.py']
```



### `tempfile`

* 파일을 임시로 만들어서 사용할 때 유용한 모듈
* `tempfile.mkstemp()`는 중복되지 않는 임시 파일의 이름을 무작위로 만들어서 돌려줌

```python
import tempfile
filename = tempfile.mkstemp()
filename
    # (4, 'C:\\Users\\sm1.seo\\AppData\\Local\\Temp\\tmp35a6bd44')
```

* `tempfile.TemporaryFile()`은 임시 저장 공간으로 사용할 파일 객체를 돌려줌
* 이 파일은 기본적으로 바이너리 쓰기 모드(wb)를 가짐
* `f.close()`가 호출되면 이 파일 객체는 자동으로 사라짐

```python
import tempfile
f = tempfile.TemporaryFile()
f.close()
```



### `time`

* 시간과 관련된 모듈


#### `time.time`

```python
# UTC(Universal Time Coordinated, 협정 세계 표준시)를 사용하여 현재 시간을 실수 형태로 돌려주는 함수
# 1970년 1월 1일 0시 0분 0초를 기준으로 지난 시간을 초단위로 돌려줌
import time
time.time()     # 1587101503.3409982
```



#### `time.localtime`

```python
# time.time()이 돌려준 실수 값을 사용해서 연도, 월, 일, 시, 분, 초, ...의 형태로 바꾸어 주는 함수
time.localtime(time.time())
    # time.struct_time(tm_year=2020, tm_mon=4, tm_mday=17, tm_hour=14, tm_min=33, tm_sec=0, tm_wday=4, tm_yday=108, tm_isdst=0)
```



#### `time.asctime`

```python
# time.localtime에 의해서 반환된 튜플 형태의 값을 인수로 받아서
# 날짜와 시간을 알아보기 쉬운 형태로 돌려주는 함수
time.asctime(time.localtime(time.time()))       # 'Fri Apr 17 14:34:04 2020'
```



#### `time.ctime`

```python
# time.asctime(time.localtime(time.time()))을 time.ctime()으로 간편하게 표시
# asctime과 다른 점은 ctime은 항상 현재 시간만을 돌려줌
time.ctime()        # 'Mon Apr 20 11:38:37 2020'
```



#### `time.strftime`

```python
# 시간에 관계된 것을 세밀하게 표현하는 여러 가지 포맷 코드 제공
time.strftime('출력할 형식 포맷 코드', time.localtime(time.time()))
```

| 포맷코드 | 설명                                  | 예                  |
| -------- | ------------------------------------- | ------------------- |
| `%a`     | 요일 줄임말                           | `Mon`               |
| `%A`     | 요일                                  | `Monday`            |
| `%b`     | 달 줄임말                             | `Jan`               |
| `%B`     | 달                                    | `January`           |
| `%c`     | 날짜와 시간을 출력함                  | `06/01/01 17:22:21` |
| `%d`     | 날(day)                               | `[01, 31]`          |
| `%H`     | 시간(hour)-24시간 출력 형태           | `[00, 23]`          |
| `%I`     | 시간(hour)-12시간 출력 형태           | `[01, 12]`          |
| `%j`     | 1년 중 누적 날짜                      | `[001, 366]`        |
| `%m`     | 달                                    | `[01, 12]`          |
| `%M`     | 분                                    | `[01, 59]`          |
| `%p`     | AM or PM                              | `AM`                |
| `%S`     | 초                                    | `[00, 59]`          |
| `%U`     | 1년 중 누적 주-일요일을 시작으로      | `[00, 53]`          |
| ` %w`    | 숫자로 된 요일                        | `[0(일요일), 6]`    |
| `%W`     | 1년 중 누적 주-월요일을 시작으로      | `[00, 53]`          |
| `%x`     | 현재 설정된 로케일에 기반한 날짜 출력 | `06/01/01`          |
| `%X`     | 현재 설정된 로케일에 기반한 시간 출력 | `17:22:21`          |
| `%Y`     | 년도 출력                             | `2001`              |
| `%Z`     | 시간대 출력                           | `대한민국 표준시`   |
| `%%`     | 문자                                  | `%`                 |
| `%y`     | 세기부분을 제외한 년도 출력           | `01`                |

```python
import time
time.strftime('%x', time.localtime(time.time()))
    # '05/01/01'
time.strftime('%c', time.localtime(time.time()))
    # '05/01/01 17:22:21'
```


#### `time.sleep`

```python
# 주로 루프 안에서 많이 사용
# 일정한 시간 간격을 두고 루프를 실행할 수 있음
# sleep1.py
import time
for i in range(10):
    print(i)
    time.sleep(1)
```



### `calendar`

* 달력을 볼 수 있게 해주는 모듈


#### `calendar.calendar(연도)`

```python
# 그 해의 전체 달력
import calendar
print(calendar.calendar(2020))
```


#### `calendar.prcal(연도)`

```python
# calendar.calendar(연도)와 똑같은 결괏값
calendar.prcal(2020)
```


#### `calendar.prmonth`

```python
# 2020년 4월의 달력만 보여줌
calendar.prmonth(2020, 4)
    #      April 2020
    # Mo Tu We Th Fr Sa Su
    #        1  2  3  4  5
    #  6  7  8  9 10 11 12
    # 13 14 15 16 17 18 19
    # 20 21 22 23 24 25 26
    # 27 28 29 30
```


#### `calendar.weekday`

```python
# 그 날짜에 해당하는 요일 정보를 돌려줌
calendar.weekday(2020, 12, 31)      # 3
```


#### `calendar.monthrange`

```python
# 입력받은 달의 1일이 무슨 요일인지와 그 달이 며칠까지 있는지를 튜플 형태로 돌려줌
calendar.monthrange(2020, 4)        # (2, 30)
```



### `random`

* 난수(규칙이 없는 임의의 수)를 발생시키는 모듈

```python
# 0.0에서 1.0 사이의 실수 중에서 난수 값을 돌려주는 예
import random
random.random()             # 0.7376084820881715

# 1에서 10 사이의 정수 중에서 난수 값을 돌려줌
random.randint(1, 10)       # 7

# 1에서 55 사이의 정수 중에서 난수 값을 돌려줌
random.randint(1, 55)       # 18
```

* 리스트의 요소 중에서 무작위로 하나를 선택하여 꺼낸 다음 그 값을 돌려줌

```python
# random_pop.py
import random
def random_pop(data):
    number = random.randint(0, len(data)-1)
    return data.pop(number)

if __name__ == "__main__":
    data = [1, 2, 3, 4, 5]
    while data:
        print(random_pop(data))

    # 2
    # 5
    # 3
    # 1
    # 4
```

* `Choice` 함수 사용

```python
# random.choice 함수는 입력으로 받은 리스트에서 무작위로 하나를 선택하여 돌려줌
def random_pop(data):
    number = random.choice(data)
    data.remove(number)
    return number
```

* 리스트의 항목을 무작위로 섞고 싶을 때

```python
# random.shuffle 함수 사용
import random
data = [1, 2, 3, 4, 5]
random.shuffle(data)
data                        # [5, 1, 3, 4, 2]
```



### `webbrowser`

* 자신의 시스템에서 사용하는 기본 웹 브라우저를 자동으로 실행하는 모듈

```python
# 웹 브라우저를 자동으로 실행하고 해당 URL인 google.com으로 가게 해 줌
# 웹 브라우저가 이미 실행된 상태라면 입력 주소로 이동
# 웹 브라우저가 실행되지 않은 상태라면 새로 웹 브라우저를 실행한 후 해당 주소로 이동
import webbrowser
webbrowser.open("http://google.com")

# open_new 함수는 이미 웹 브라우저가 실행된 상태이더라도 새로운 창으로 해당 주소가 열리게 함
webbrowser.open_new("http://google.com")
```



### `threading`

* 프로세스(Process): 컴퓨터에서 동작하고 있는 프로그램
* 보통 1개의 프로세스는 한 가지 일만 하지만 스레드(Thread)를 사용하면 한 프로세스 안에서 2가지 또는 그 이상의 일을 동시에 수행할 수 있음

```python
# long_task 함수는 수행하는데 5초의 시간이 걸리는 함수
# 함수를 5번 반복해서 수행: 25초
# thread_test.py
import time

def long_task():                        # 5초의 시간이 걸리는 함수
    for i in range(5):
        time.sleep(1)                   # 1초간 대기
        print("working:%s\n" % i)

print("Start")

for i in range(5): long_task를 5회 수행한다.
    long_task()

print("End")
```

* 스레드 사용

```python
# Start와 End가 먼저 출력되고 그 이후에 스레드의 결과가 출력
# 프로그램이 정상 종료되지 않음
# thread_test.py
import time
import threading                            # 스레드를 생성하기 위해서는 threading 모듈이 필요하다.

def long_task():
    for i in range(5):
        time.sleep(1)
        print("working:%s\n" % i)

print("Start")

threads = []
for i in range(5):
    t = threading.Thread(target=long_task)  # 스레드를 생성한다.
    threads.append(t)

for t in threads:
    t.start()                               # 스레드를 실행한다.

print("End")
```

* 스레드의 `join` 함수

```python
# Start가 출력되고 그 다음에 스레드의 결과가 출력된 후 마지막으로 End가 출력
# thread_test.py
import time
import threading

def long_task():
    for i in range(5):
        time.sleep(1)
        print("working:%s\n" % i)

print("Start")

threads = []
for i in range(5):
    t = threading.Thread(target=long_task)
    threads.append(t)

for t in threads:
    t.start()

for t in threads:
    t.join()                            # join으로 스레드가 종료될때까지 기다린다.

print("End")
```