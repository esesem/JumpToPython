# 프로그램의 입력과 출력



## 함수



### 함수란 무엇인가?

* 입력값을 가지고 어떤 일을 수행한 다음에 그 결과물을 내어놓는 것.



### 함수를 사용하는 이유는 무엇일까?

* 반복되는 부분이 있을 경우 "반복적으로 사용되는 가치 있는 부분"을 한 뭉치로 묶어서 "어떤 입력값을 주었을 때 어떤 결괏값을 돌려준다"라는 식의 함수로 작성하는 것이 현명
* 자신이 만든 프로그램을 함수화하면 프로그램 흐름을 일목요연하게 볼 수 있기 때문
  - 프로그램 흐름 잘 파악할 수 있고 오류가 어디에서 나는지도 바로 알아차릴 수 있음



### 파이썬 함수의 구조

```python
def 함수명(매개변수):
    수행할 문장1
    수행할 문장2
    ...
```

* 간단한 예제

```python
# 이 함수의 이름(함수 이름)은 add이고 입력으로 개의 값을 받으며 결괏값은 2개의 입력값을 더한 값이다.
def add(a, b):
    return a + b

a = 3
b = 4
c = add(a, b)
print(c)            # 7
```



### 매개변수와 인수

* 매개변수(parameter): 함수에 입력으로 전달된 값을 받는 변수
* 인수(argument): 함수를 호출할 때 전달하는 입력값

```python
def add(a, b):          # a, b는 매개변수
    return a + b

print(add(3, 4))        # 3, 4는 인수
```



### 입력값과 결괏값에 따른 함수의 형태


#### 일반적인 함수

```python
def 함수이름(매개변수):
    수행할 문장
    ...
    return 결과값

# 일반 함수의 전형적인 예
def add(a, b):
    result = a + b
    return result

# 이 함수를 사용하는 방법
a = add(3, 4)
print(a)                # 7

# 입력값과 결괏값이 있는 함수의 사용법
결괏값을 받을 변수 = 함수이름(입력인수1, 입력인수2, ...)
```


#### 입력값이 없는 함수

```python
def say():
    return 'Hi'

# 함수 사용
a = say()
print(a)                            # Hi

# 입력값이 없고 결괏값만 있는 함수 사용
결괏값을 받을 변수 = 함수이름()
```


#### 결괏값이 없는 함수

```python
def add(a, b):
    print("%d, %d의 합은 %d입니다.", % (a, b, a+b))

# 함수 사용
a = add(3, 4)                           # 3, 4의 합은 7입니다.
print(a)                                # None

# 결괏값이 없는 함수 사용
함수이름(입력인수1, 입력인수2, ...)
```


#### 입력값도 결괏값도 없는 함수

```python
def say():
    print('Hi')

# 함수 사용
say()               # Hi

# 입력값도 결괏값도 없는 함수 사용
함수이름()
```



### 매개변수 지정하여 호출하기

* 함수를 호출할 때 매개변수 지정

```python
def add(a, b):
    return a+b

# 매개변수 지정
result = add(a=3, b=7)      # a에 3, b에 7을 전달
print(result)               # 10

# 매개변수 지정하면 순서에 상관없이 사용할 수 있다는 장점
result = add(b=5, a=3)      # b에 5, a에 3을 전달
print(result)               # 8
```



### 입력값이 몇 개가 될지 모를 때는 어떻게 해야 할까?

```python
def 함수이름(*매개변수):
    수행할 문장
    ...
```

* 일반 함수 형태에서 괄호 안의 매개변수 부분이 `*매개변수`로 바뀜


#### 여러 개의 입력값을 받는 함수 만들기

* 매개변수 이름 앞에 `*`을 붙이면 입력값을 전부 모아서 튜플로 만들어 줌

```python
def add_many(*args):
    result = 0
    for i in args:
        result = result + i
    return result

result = add_many(1, 2, 3)      # args = (1, 2, 3)
print(result)                   # 6

result = add_many(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
print(result)                   # 55
```

* 여러 개의 입력 처리

```python
def add_mul(choice, *args):
    if choice == "add":
        result = 0
        for i in args:
            result = result + i
    elif choice == "mul":
        result = 1
        for i in args:
            result = result * i
    return result

# 함수 사용
result = add_mul('add', 1, 2, 3, 4, 5)
print(result)                               # 15

result = add_mul('mul', 1, 2, 3, 4, 5)
print(result)                               # 120
```


#### 키워드 파라미터 `kwargs`

* 키워드 파라미터를 사용할 때는 매개변수 앞에 별 두 개(`**`)
* 매개변수 이름 앞에 `**`를 붙이면 매개변수 `kwargs`는 딕셔너리가 되고 모든 `key=value` 형태의 결괏값이 그 딕셔너리에 저장됨

```python
def print_kwargs(**kwargs):
    print(kwargs)

print_kwargs(a=1)                   # {'a': 1}
print_kwargs(name='foo', age=3)     # {'age': 3, 'name': 'foo'}
```



### 함수의 결괏값은 언제나 하나이다

```python
def add_and_mul(a, b):
    return a+b, a*b

result = add_and_mul(3, 4)                  # result = (7, 12)
# 함수의 결괏값 a+b와 a*b는 튜플값 하나인 (a+b, a*b)로 돌려줌

# 하나의 튜플 값을 2개의 결괏값처럼 받고 싶으면 다음과 같이 함수 호출
result1, result2 = add_and_mul(3, 4)        # result1, result2 = (7, 12)

# return문 2번 사용
def add_and_mul(a, b):
    return a+b
    return a*b

result = add_and_mul(2, 3)
print(result)                               # 5
# 함수는 return문을 만나는 순간 결괏값을 돌려준 다음 함수를 빠져나감
```


#### `return`의 또 다른 쓰임새

* 특별한 상황일 때 함수를 빠져나가고 싶다면 `return`을 단독으로 써서 함수를 즉시 빠져나갈 수 있음

```python
def say_nick(nick):
    if nick == "바보":
        return
    print("나의 별명은 %s 입니다." % nick)

say_nick('야호')            # 나의 별명은 야호입니다.
say_nick('바보')            # 나의 별명은 바보입니다.
```



### 매개변수에 초깃값 미리 설정하기

* `man=True`처럼 매개변수에 미리 값을 넣어 줌
  - 함수의 매개변수 초깃값을 설정하는 방법
* 함수의 매개변수에 들어갈 값이 항상 변하는 것이 아닐 경우에는 이렇게 함수의 초깃값을 미리 설정해 두면 유용

```python
def say_myself(name, old, man=True):
    print("나의 이름은 %s 입니다." % name)
    print("나이는 %d살입니다." % old)
    if man:
        print("남자입니다.")
    else:
        print("여자입니다.")

# 함수 사용
say_myself("박응용", 27)
    # 나의 이름은 박응용입니다.
    # 나이는 27살입니다.
    # 남자입니다.

say_myself("박응용", 27, True )
    # 나의 이름은 박응용입니다.
    # 나이는 27살입니다.
    # 남자입니다.

say_myself("박응선", 27, False)
    # 나의 이름은 박응선입니다.
    # 나이는 27살입니다.
    # 여자입니다.
```

* 함수의 매개변수에 초깃값을 설정할 때 주의할 것
  - 초기화시키고 싶은 매개변수를 항상 뒤쪽에 놓는 것을 잊지 말 것

```python
def say_myself(name, man=True, old):
    print("나의 이름은 %s 입니다." % name)
    print("나이는 %d살입니다." % old)
    if man:
        print("남자입니다.")
    else:
        print("여자입니다.")

say_myself("박응용", 27)                    # SyntaxError
```



### 함수 안에서 선언한 변수의 효력 범위

* 함수 안에서 사용할 변수의 이름을 함수 밖에서도 동일하게 사용한다면 어떻게 될까?

```python
# vartest.py
a = 1
def vartest(a):
    a = a + 1

vartest(a)
print(a)                    # 1
# def vartest(a)에서 입력값을 전달받는 매개변수 a는 함수 안에서만 사용하는 변수이지 함수 밖의 변수 a가 아님

# vartest 함수는 다음처럼 변수 이름을 hello로 한 vartest 함수와 완전히 동일
def vartest(hello):
    hello = hello + 1
```

* 함수 안에서 사용하는 매개변수는 함수 밖의 변수 이름과는 전혀 상관이 없음

```python
# vartest_error.py
def vartest(a):
    a = a + 1

vartest(3)
print(a)            # NameError
# print(a)에서 입력받아야 하는 a 변수를 어디에서도 찾을 수가 없음
# 함수 안에서 선언한 매개변수는 함수 안에서만 사용될 뿐 함수 밖에서는 사용되지 않음
```



### 함수 안에서 함수  밖의 변수를 변경하는 방법


#### 1. `return` 사용하기

* `a`가 `vartest` 함수의 결괏값으로 바뀜
* 여기에서도 `vartest` 함수 안의 `a` 매개변수는 함수 밖의 `a`와는 다름

```python
# vartest_return.py
a = 1
def vartest(a):
    a = a + 1
    return a

a = vartest(a)
print(a)            # 2
```


#### 2. `global` 명령어 사용하기

* `vartest` 함수 안의 `global a` 문장은 함수 안에서 함수 밖의 `a` 변수를 직접 사용하겠다는 뜻
* 하지만 프로그래밍을 할 때 `global` 명령어는 사용하지 않는 것이 좋음
  - 함수는 독립적으로 존재하는 것이 좋기 때문
  - 외부 변수에 종속적인 함수는 그다지 좋은 함수가 아님

```python
# vartest_global.py
a = 1
def vartest():
    global a
    a = a + 1

vartest()
print(a)            # 2
```



### `lambda`

* `lambda`는 함수를 생성할 때 사용하는 예약어로 `def`와 동일한 역할을 함
  - 보통 함수를 한줄로 간결하게 만들 때 사용
  - "람다"라고 읽고 `def`를 사용해야 할 정도로 복잡하지 않거나 `def`를 사용할 수 없는 곳에 주로 쓰임
* 사용법

```python
lambda 매개변수1, 매개변수2, ...: 매개변수를 이용한 표현식

# 두 개의 인수를 받아 서로 더한 값을 돌려주는 lambda 함수
add = lambda a, b: a+b
result = add(3, 4)
print(result)               # 7

# def를 사용한 다음 함수와 하는 일이 완전히 동일
def add(a, b):
    return a+b
result = add(3, 4)
print(result)               # 7
```

> `lambda` 예약어로 만든 함수는 `return` 명령어가 없어도 결괏값을 돌려준다.




## 사용자 입력과 출력



### 사용자 입력

* 사용자가 입력한 값을 어떤 변수에 대입하고 싶을 때


#### `input`의 사용

* `input`은 입력되는 모든 것을 문자열로 취급

```python
a = input()
# Life is too short, you need python
a
    # 'Life is too short, you need python'
```


#### 프롬프트를 띄워서 사용자 입력 받기

```python
input("질문 내용")

# 예제
number = input("숫자를 입력하세요: ")

# 숫자를 입력하세요: 3
print(number)       # 3
```



### `print` 자세히 알기

* 지금껏 `print`문이 수행해 온 일은 우리가 입력한 자료형을 출력하는 것

```python
a = 123
print(a)            # 123
a = "Python"
print(a)            # Python
a = [1, 2, 3]
print(a)            # [1, 2, 3]
```


#### 큰따옴표(")로 둘러싸인 문자열은 `+` 연산과 동일하다

* 따옴표로 둘러싸인 문자열을 연속해서 쓰면 `+` 연산을 한 것과 같음

```python
print("life" "is" "too short")      # lifeistoo short
print("life"+"is"+"too short")      # lifeistoo short
```


#### 문자열 띄어쓰기는 콤마로 한다

* 콤마(`,`)를 사용하면 문자열 사이에 띄어쓰기를 할 수 있음

```python
print("life", "is", "too short")        # life is too short
```


#### 한 줄에 결괏값 출력하기

* 매개변수 `end`를 사용해 끝 문자를 지정

```python
for i in range(10):
    print(i, end=' ')

    # 0 1 2 3 4 5 6 7 8 9
```




## 파일 읽고 쓰기



### 파일 생성하기

* 파이썬 내장 함수 `open`을 사용
* "파일 이름"과 "파일 열기 모드"를 입력값으로 받고 결괏값으로 파일 객체를 돌려줌

```python
파일 객체 = open(파일 이름, 파일 열기 모드)

f = open("새파일.txt", 'w')
f.close()
```

* 파일 열기 모드

| 파일열기모드 | 설명                                                       |
| ------------ | ---------------------------------------------------------- |
| `r`          | 읽기모드 - 파일을 읽기만 할 때 사용                        |
| `w`          | 쓰기모드 - 파일에 내용을 쓸 때 사용                        |
| `a`          | 추가모드 - 파일의 마지막에 새로운 내용을 추가 시킬 때 사용 |

* 파일을 쓰기 모드로 열면 해당 파일이 이미 존재할 경우 원래 있던 내용이 모두 사라지고, 해당 파일이 존재하지 않으면 새로운 파일이 생성
* 새파일.txt 파일을 `C:/doit` 디렉터리에 생성하고 싶다면 다음과 같이 작성
* `f.close()`는 열러 있는 파일 객체를 닫아 주는 역할
  - 생략해도 됨, 프로그램을 종료할 때 파이썬 프로그램이 열려 있는 파일의 객체를 자동으로 닫아주기 때문
    - 하지만 `close()`를 사용해서 열려 있는 파일을 직접 닫아주는 것이 좋음
    - 쓰기모드로 열었던 파일을 닫지 않고 다시 사용하려고 하면 오류가 발생

```python
f = open("C:/doit/새파일.txt", 'w')
f.close()
```



### 파일을 쓰기 모드로 열어 출력값 적기

* 두 프로그램의 다른 점: data를 출력하는 방법

```python
# 모니터 화면 대신에 파일에 결괏값을 적는 방법
# writedata.py
f = open("C:/doit/새파일.txt", 'w')
for i in range(1, 11):
    data = "%d번째 줄입니다.\n" % i
    f.write(data)
f.close()

# 비교: 모니터 화면에 출력하는 방법
for i in range(1, 11):
    data = "%d번째 줄입니다.\n" % i
    print(data)
```

* 새파일.txt

```Text
1번째 줄입니다.
2번째 줄입니다.
3번째 줄입니다.
4번째 줄입니다.
5번째 줄입니다.
6번째 줄입니다.
7번째 줄입니다.
8번째 줄입니다.
9번째 줄입니다.
10번째 줄입니다.
```



### 프로그램의 외부에 저장된 파일을 읽는 여러 가지 방법


#### `readline()` 함수 이용하기

* 파일의 첫 번째 줄을 읽어 출력

```python
# readline_test.py
f = open("C:/doit/새파일.txt", 'r')
line = f.readline()
print(line)                             # 1번째 줄입니다.
f.close
```

* 모든 줄을 읽어서 화면에 출력

```python
# readline_all.py
f =open("C:/doit/새파일.txt", 'r')
while True:
    line = f.readline()
    if not line: break
    print(line)
f.close()
```

* 사용자의 입력을 받아서 그 내용을 출력하는 경우

```python
while 1:
    data = input()
    if not data: break
    print(data)
```


#### `readlines` 함수 사용하기

* `readlines` 함수는 파일의 모든 줄을 읽어서 각각의 줄을 요소로 갖는 리스트로 돌려줌

```python
f = open("C:/doit/새파일.txt", 'r')
data = f.readlines()
for line in lines:
    print(line)
f.close()
```


#### `read` 함수 사용하기

* 파일의 내용 전체를 문자열로 돌려줌

```python
f = open("C:/doit/새파일.txt", 'r')
data = f.read()
print(data)
f.close()
```



### 파일에 새로운 내용 추가하기

* 쓰기 모드('w')로 파일을 열 때 이미 존재하는 파일을 열면 그 파일의 내용이 모두 사라짐.
* 원래 있던 값을 유지하면서 단지 새로운 값만 추가해야 할 경우에는 파일을 추가 모드('a')로 열면 됨

```python
# 추가 모드로 파일을 열었기 때문에 새파일.txt 파일이 원래 가지고 있던 내용 바로 다음부터 결괏값을 적기 시작
# adddata.py
f = opne("C:/doit/새파일.txt", 'a')
for i in range(11, 20):
    data = "%d번째 줄입니다.\n" % i
    f.write(data)
f.close()
```

* 새파일.txt

```Text
1번째 줄입니다.
2번째 줄입니다.
3번째 줄입니다.
4번째 줄입니다.
5번째 줄입니다.
6번째 줄입니다.
7번째 줄입니다.
8번째 줄입니다.
9번째 줄입니다.
10번째 줄입니다.
11번째 줄입니다.
12번째 줄입니다.
13번째 줄입니다.
14번째 줄입니다.
15번째 줄입니다.
16번째 줄입니다.
17번째 줄입니다.
18번째 줄입니다.
19번째 줄입니다.
```



### `with`문과 함께 사용하기

* 파일을 열고 닫는 것을 자동으로 처리
* `with` 블록을 벗어나는 순간 열린 파일 객체 `f`가 자동으로 close되어 편리

```python
# 예제
f = open("foo.txt", "w")
f.write("Life is too short, you need python")
f.close()

# with문 사용
with open("foo.txt", "w") as f:
    f.write("Life is too short, you need python")
```


#### `sys` 모듈로 매개변수 주기

* 파이썬에서는 `sys` 모듈을 사용하여 매개변수를 직접 줄 수 있음

```shell
명령 프롬프트 명령어 [인수1 인수2 ...]
```

* 입력받은 인수를 `for`문을 사용해 차례대로 하나씩 출력하는 예

```python
# sys1.py
import sys

args = sys.argv[1:]
for i in args:
    print(i)
```

```
C:\doit>python sys1.py aaa bbb ccc
aaa
bbb
ccc
```

* 명령 행에 입력된 소문자를 대문자로 바꾸어 주는 프로그램

```python
# sys2.py
import sys
args = sys.argv[1:]
for i in args:
    print(i.upper(), end=' ')
```

```
C:\doit>python sys2.py life is too short, you need python
LIFE IS TOO SHORT, YOU NEED PYTHON
```