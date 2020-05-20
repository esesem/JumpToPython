# 자료형

**파이썬 프로그래밍의 기초, 자료형**

* 숫자형
* 문자열 자료형
* 리스트 자료형
* 튜플 자료형
* 딕셔너리 자료형
* 집합 자료형
* 불 자료형
* 변수




## 숫자형



### 숫자형이란?

* 숫자 형태로 이루어진 자료형
* 정수, 실수, 8진수, 16진수, ...



### 숫자형은 어떻게 만들고 사용할까?


#### 정수형

```python
a = 123
a = -178
a = 0
```


#### 실수형

```python
a = 1.2
a = -3.45
a = 4.24E10         # e를 써도 무방, 10^10을 의미
a = 4.24e-10        # 10^(-10)을 의미
```

#### 8진수와 16진수

```python
a = 0o177       # 8진수: 0o 또는 0O로 시작하면 된다.
a = 0x8ff       # 16진수: 0x로 시작하면 된다.
b = 0xABC       # 16진수: 대소문자 혼용가능
```



### 숫자형을 활용하기 위한 연산자


#### 사칙연산

```python
a = 3
b = 4
a + b       # 7
a * b       # 12
a / b       # 0.75
```


#### 제곱 연산자

```python
a ** b      # 81
```


#### 나눗셈 나머지 반환 연산자

```python
7 % 3       # 1
3 % 7       # 3
```


#### 나눗셈 몫 반환 연산자

```python
7 / 4       # 1.75  나눗셈 결과값
7 // 4      # 1     몫에 해당하는 정수값만 반환
```




## 문자열 자료형



### 문자열이란?

* 문자, 단어 등으로 구성된 문자들의 집합
* 따옴표로 둘러싸여 있으면 모두 문자열



### 문자열은 어떻게 만들고 사용할까?

```python
### 1. 큰따옴표
"Hello World"

### 2. 작은따옴표
'Python is fun'

### 3. 큰따옴표 3개
"""Life is too short, You need python"""

### 4. 작은따옴표 3개
'''Life is too short, You need python'''
```


#### 문자열 안에 작은따옴표나 큰따옴표를 포함시키고 싶을 때

```python
### 1. 문자열에 작은따옴표 포함시키기
# (큰따옴표 안에 들어있는 작은따옴표는 문자열을 나타내기 위한 기호로 인식되지 않음)
food = "Python's favorite food is perl"
food                                        # "Python's favorite food is perl"
food = 'Python's favorite food is perl'    '# SyntaxError

### 2. 문자열에 큰따옴표 포함시키기
# (문자열을 작은따옴표로 둘러쌈)
say = '"Python is very easy." he says.'

### 3. 백슬래시(\)를 사용해서 작은따옴표와 큰따옴표를 문자열에 포함시키기
food = 'Python\'s favorite food is perl'
say = "\"Python is very easy.\" he says."
```


#### 여러 줄인 문자열을 변수에 대입하고 싶을 때

```python
### 1. 줄을 바꾸기 위한 이스케이프 코드 \n 삽입하기
multiline = "Life is too short\nYou need python"

### 2. 연속된 작은따옴표 3개 또는 큰따옴표 3개 사용하기
# (작은따옴표)
multiline = '''
Life is too short
You need python
'''
# (큰따옴표)
multiline = """
Life is too short
You need python
"""
```


#### 이스케이프 코드란?

| 코드   | 설명                                           |
| ------ | ---------------------------------------------- |
| `\n`   | 줄 바꿈                                        |
| `\t`   | 탭                                             |
| `\\`   | 문자 `\`를 그대로 표현                         |
| `\'`   | 작은따옴표를 그대로 표현                       |
| `\"`   | 큰따옴표를 그대로 표현                         |
| `\r`   | 캐리지 리턴 (줄 바꿈, 현재 커서를 가장 앞으로) |
| `\f`   | 폼 피드 (줄 바꿈, 현재 커서를 다음 줄로)       |
| `\a`   | 벨 소리                                        |
| `\b`   | 백 스페이스                                    |
| `\000` | 널 문자                                        |



### 문자열 연산하기


#### 문자열 더해서 연결하기(Concatenation)

```python
head = "Python"
tail = " is fun!"
head + tail             # 'Python is fun!'
```


#### 문자열 곱하기

```python
a = "python"
a * 2               # 'pythonpython'
```

 

#### 문자열 곱하기 응용

```python
# multistring.py
print("=" * 50)
print("My Program")
print("=" * 50)
```

(결과)

```
C:\doit> python multistring.py
==================================================
My Program
==================================================
```


#### 문자열 길이 구하기

```python
a = "Life is too short"
len(a)                      # 17
```



### 문자열 인덱싱과 슬라이싱

> "파이썬은 0부터 숫자를 센다."

> 인덱싱 기법과 슬라이싱 기법은 뒤에서 배울 자료형인 리스트나 튜플에서도 사용할 수 있다.


#### 문자열 인덱싱이란?

```python
a = "Life is too short, You need Python"

# Life is too short, You need Python
# 0         1         2         3
# 0123456789012345678901234567890123
a[3]                                        # 'e'
```


#### 문자열 인덱싱 활용하기

```python
a[0]        # 'L'
a[12]       # 's'
a[-1]       # 'n'       # 뒤에서 부터 셈
a[-0]       # 'L'       # a[0]과 동일한 결과
a[-5]       # 'y'
```


#### 문자열 슬라이싱이란?

```python
b = a[0] + a[1] + a[2] + a[3]
b                                   # 'Life'
a[0:4]                              # 'Life'        # 끝 번호에 해당하는 것은 포함하지 않음
a[0:3]                              # 'Lif'
```


#### 문자열을 슬라이싱 하는 방법

```python
a[5:7]          # 'is'
a[19:]          # 'You need Python'                         # 시작번호 ~ 끝까지
a[:17]          # 'Life is too short'                       # 처음 ~ 끝번호까지
a[:]            # 'Life is too short, You need Python'      # 전체
a[19:-7]        # 'You need'
```


#### 슬라이싱으로 문자열 나누기

```python
a = "20010331Rainy"
year = a[:4]
day = a[4:8]
weather = a[8:]
year                # '2001'
day                 # '0331'
weather             # 'Rainy'
```


#### "Pithon"이라는 문자열을 "Python"으로 바꾸려면?

```python
a = "Pithon"
a[1] = 'y'
a                       # 'Python'
a[:1] + 'y' + a[2:]     # 'Python'
```



### 문자열 포매팅

* 문자열 안에 어떤 값을 삽입하는 방법


#### 문자열 포매팅 따라하기

```python
### 1. 숫자 바로 대입
"I eat %d apples." % 3          # 'I eat 3 apples.'

### 2. 문자열 바로 대입
"I eat %s apples." % "five"     # 'I eat five apples.'

### 3. 숫자 값을 나타내는 변수로 대입
number = 3
"I eat %d apples." % number     # 'I eat 3 apples.'

### 4. 2개 이상의 값 넣기
number = 10
day = "three"
"I ate %d apples. so I was sick for %s days." % (number, day)
    # 'I ate 10 apples. so I was sick for three days.'
```


#### 문자열 포맷 코드

| 코드 | 설명                      |
| ---- | ------------------------- |
| `%s` | 문자열(string)            |
| `%c` | 문자 1개(character)       |
| `%d` | 정수(integer)             |
| `%f` | 부동소수(floating-point)  |
| `%o` | 8진수                     |
| `%x` | 16진수                    |
| `%%` | Literal % (문자 `%` 자체) |

> `%s`는 어떤 형태의 값이든 변환해 넣을 수 있다. 왜냐하면 `%s`는 자동으로 `%` 뒤에 있는 값을 문자열로 바꾸기 때문이다.


#### 포매팅 연산자 `%d`와 `%`를 같이 쓸 때는 `%%`를 쓴다

```python
"Error is %d%." % 98        # ValueError
"Error is %d%%." % 98       # 'Error is 98%.'
```


#### 포맷 코드와 숫자 함께 사용하기

```python
### 1. 정렬과 공백
"%-10sjane." % 'hi'         # 'hi        jane.'

### 2. 소수점 표현하기
"%0.4f" % 3.42134234        # '3.4213'
"%10.4f" % 3.42134234       # '    3.4213'
```


#### `format` 함수를 사용한 포매팅

```python
### 숫자 바로 대입하기
"I eat {0} apples".format(3)            # 'I eat 3 apples'

### 문자열 바로 대입하기
"I eat {0} apples".format("five")       # 'I eat five apples'

### 숫자 값을 가진 변수로 대입하기
number = 3
"I eat {0} apples".format(number)       # 'I eat 3 apples'

### 2개 이상의 값 넣기
number = 10
day = "three"
"I ate {0} apples. so I was sick for {1} days.".format(number, day)
    # 'I ate 10 apples. so I was sick for three days.'

### 이름으로 넣기
"I ate {number} apples. so I was sick for {day} days.".format(number=10, day=3)
    # 'I ate 10 apples. so I was sick for 3 days.'

### 인덱스와 이름을 혼용해서 넣기
"I ate {0} apples. so I was sick for {day} days.".format(10, day=3)
    # 'I ate 10 apples. so I was sick for 3 days.'

### 왼쪽 정렬
"{0:<10}".format("hi")                  # 'hi        '

### 오른쪽 정렬
"{0:>10}".format("hi")                  # '        hi'

### 가운데 정렬
"{0:^10}".format("hi")                  # '    hi    '

### 공백 채우기
"{0:=^10}".format("hi")                 # '====hi===='
"{0:!<10}".format("hi")                 # 'hi!!!!!!!!'

### 소수점 표현하기
y = 3.42134234
"{0:0.4f}".format(y)                    # '3.4213'
"{0:10.4f}".format(y)                   # '    3.4213'

### { 또는 } 문자 표현하기
"{{ and }}".format()                    # { and }               # 두 개씩 사용
```


#### `f` 문자열 포매팅

* 파이썬 3.6 버전부터 추가
* 문자열 앞에 `f` 접두사를 붙이면 `f` 문자열 포매팅 기능을 사용할 수 있다.
* `f` 문자열 포매팅은 표현식을 지원한다.

```python
name = '홍길동'
age = 30
f'나의 이름은 {name}입니다. 나이는 {age}입니다.'
    # '나의 이름은 홍길동입니다. 나이는 30입니다.'
f'나는 내년이면 {age+1}살이 된다.'
    # '나는 내년이면 31살이 된다.'

### 정렬
f'{"hi":<10}'       # 'hi        '
f'{"hi":>10}'       # '        hi'
f'{"hi":^10}'       # '    hi    '

### 공백 채우기
f'{"hi":=^10}'      # '====hi===='
f'{"hi":!<10}'      # 'hi!!!!!!!!'

### 소수점
y = 3.42134234
f'{y:0.4f}'         # '3.4213'
f'{y:10.4f}'        # '    3.4213

### 중괄호
f'{{ and }}'        # '{ and }'
```



### 문자열 관련 함수들

* 문자열의 내장 함수

```python
### 문자 개수 세기(count)
a = "hobby"
a.count('b')                        # 2

### 위치 알려주기1(find): 문자가 처음 나온 위치 반환, 문자나 문자열이 존재하지 않는다면 -1을 반환
a = "Python is the best choice"
a.find('b')                         # 14
a.find('k')                         # -1

### 위치 알려주기2(index): 문자가 맨 처음으로 나온 위치 반환, 문자나 문자열이 존재하지 않는다면 오류
a = "Life is too short"
a.index('t')                        # 8
a.index('k')                        # ValueError

### 문자열 삽입(join)
",".join('abcd')                    # 'a,b,c,d'
",".join(['a', 'b', 'c', 'd'])      # 'a,b,c,d'

### 소문자를 대문자로 바꾸기(upper)
a = "hi"
a.upper()                           # 'HI'

### 대문자를 소문자로 바꾸기(lower)
a = "HI"
a.lower()                           # 'hi'

### 왼쪽 공백 지우기(lstrip)
a = " hi "
a.lstrip()                          # 'hi '

### 오른쪽 공백 지우기(rstrip)
a = " hi "
a.rstrip()                          # ' hi'

### 양쪽 공백 지우기(strip)
a = " hi "
a.strip()                           # 'hi'

### 문자열 바꾸기(replace)
a = "Life is too short"
a.replace("Life", "Your leg")       # 'Your leg is too short'

### 문자열 나누기(split)
a = "Life is too short"
a.split()                           # ['Life', 'is', 'too', 'short']
b = "a:b:c:d"
b.split(':')                        # ['a', 'b', 'c', 'd']
```


 

## 리스트 자료형



### 리스트는 어떻게 만들고 사용할까?

* 대괄호(`[]`)로 감싸주고 각 요솟값은 쉼표(`,`)로 구분

```python
# 여러 가지 리스트의 생김새
리스트명 = [요소1, 요소2, 요소3, ...]

a = []
b = [1, 2, 3]
c = ['Life', 'is', 'too', 'short']
d = [1, 2, 'Life', 'is']
e = [1, 2, ['Life', 'is']]
a = list()                                  # 비어 있는 리스트 생성
```



### 리스트의 인덱싱과 슬라이싱


#### 리스트의 인덱싱

```python
a = [1, 2, 3]
a                                   # [1, 2, 3]
a[0]                                # 1
a[0] + a[2]                         # 4
a[-1]                               # 3                     # 마지막 요솟값

a = [1, 2, 3, ['a', 'b', 'c']]
a[0]                                # 1
a[-1]                               # ['a', 'b', 'c']
a[3]                                # ['a', 'b', 'c']
a[-1][0]                            # 'a'
a[-1][1]                            # 'b'
a[-1][2]                            # 'c'
```


#### 삼중 리스트에서 인덱싱하기

```python
a = [1, 2, ['a', 'b', ['Life', 'is']]]
a[2][2][0]                                  # 'Life'
```


#### 리스트의 슬라이싱

```python
a = [1, 2, 3, 4, 5]
a[0:2]                  # [1, 2]
# (문자열에서 했던 것과 사용법이 완전히 동일하다)
a = "12345"
a[0:2]                  # '12'

a = [1, 2, 3, 4, 5]
b = a[:2]
c = a[2:]
b                       # [1, 2]
c                       # [3, 4, 5]
```


#### 중첩된 리스트에서 슬라이싱하기

```python
a = [1, 2, 3, ['a', 'b', 'c'], 4, 5]
a[2:5]                                      # [3, ['a', 'b', 'c'], 4]
a[3][:2]                                    # ['a', 'b']
```



### 리스트 연산하기

* `+` 기호를 사용해서 더할 수 있고, `*` 기호를 사용해서 반복


#### 리스트 더하기(`+`)

```python
a = [1, 2, 3]
b = [4, 5, 6]
a + b               # [1, 2, 3, 4, 5, 6]
```


#### 리스트 반복하기(`*`)

```python
a = [1, 2, 3]
a * 3               # [1, 2, 3, 1, 2, 3, 1, 2, 3]
```


#### 리스트 길이구하기

```python
# len 함수 사용: 문자열, 리스트 외에 튜플과 딕셔너리에도 사용할 수 있는 함수
a = [1, 2, 3]
len(a)              # 3
```


#### 초보자가 범하기 쉬운 리스트 연산 오류

```python
a = [1, 2, 3]
a[2] + "hi"             # TypeError
str(a[2]) + "hi"        # '3hi'
```



### 리스트의 수정과 삭제


#### 리스트에서 값 수정하기

```python
a = [1, 2, 3]
a[2] = 4
a                   # [1, 2, 4]
```


#### `del` 함수 사용해 리스트 요소 삭제하기

* `del` 함수는 파이썬이 자체적으로 가지고 있는 삭제 함수이며 `del 객체`와 같이 사용

```python
a = [1, 2, 3]
del a[1]
a                       # [1, 3]

a = [1, 2, 3, 4, 5]
del a[2:]
a                       # [1, 2]
```



### 리스트 관련 함수들


#### 리스트에 요소 추가(`append`)

```python
# append(x)는 리스트의 맨 마지막에 x를 추가하는 함수
a = [1, 2, 3]
a.append(4)
a                       # [1, 2, 3, 4]
a.append([5, 6])
a                       # [1, 2, 3, 4, [5, 6]]
```


#### 리스트 정렬(`sort`)

```python
# sort 함수는 리스트의 요소를 순서대로 정렬
a = [1, 4, 3, 2]
a.sort()
a                       # [1, 2, 3, 4]
a = ['a', 'c', 'b']
a.sort()
a                       # ['a', 'b', 'c']
```


#### 리스트 뒤집기(`reverse`)

```python
# reverse 함수는 리스트를 역순으로 뒤집어 줌
# 그저 현재의 리스트를 그대로 거꾸로 뒤집음
a = ['a', 'c', 'b']
a.reverse()
a                       # ['b', 'c', 'a']
```


#### 위치 반환(`index`)

```python
# index(x) 함수는 리스트에 x 값이 있으면 x의 위치 값을 돌려줌
a = [1, 2, 3]
a.index(3)          # 2
a.index(1)          # 0
a.index(0)          # ValueError
```


#### 리스트에 요소 삽입(`insert`)

```python
# insert(a, b)는 리스트의 a번째 위치에 b를 삽입하는 함수
a = [1, 2, 3]
a.insert(0, 4)
a                   # [4, 1, 2, 3]

a.insert(3, 5)
a                   # [4, 1, 2, 5, 3]
```


#### 리스트 요소 제거(`remove`)

```python
# remove(x)는 리스트에서 첫 번째로 나오는 x를 삭제하는 함수
a = [1, 2, 3, 1, 2, 3]
a.remove(3)
a                           # [1, 2, 1, 2, 3]
a.remove(3)
a                           # [1, 2, 1, 2]
```


#### 리스트 요소 끄집어내기(`pop`)

```python
# pop()은 리스트의 맨 마지막 요소를 돌려주고 그 요소는 삭제
a = [1, 2, 3]
a.pop()             # 3
a                   # [1, 2]

# pop(x)는 리스트의 x번째 요소를 돌려주고 그 요소는 삭제
a = [1, 2, 3]
a.pop(1)            # 2
a                   # [1, 3]
```


#### 리스트에 포함된 요소 x의 개수 세기(`count`)

```python
# count(x)는 리스트 안에 x가 몇 개 있는지 조사하여 그 개수를 돌려주는 함수
a = [1, 2, 3, 1]
a.count(1)              # 2
```


#### 리스트 확장(`extend`)

```python
# extend(x)에서 x에는 리스트만 올 수 있으며 원래의 a 리스트에 x 리스트를 더함
# a.extend([4, 5])는 a += [4, 5]와 동일
a = [1, 2, 3]
a.extend([4, 5])
a                       # [1, 2, 3, 4, 5]
b = [6, 7]
a.extend(b)
a                       # [1, 2, 3, 4, 5, 6, 7]
```




## 튜플 자료형



### 튜플은 어떻게 만들까?

튜플(tuple)은 몇 가지 점을 제외하곤 리스트와 거의 비슷하며 다른 점은;

* 리스트는 `[]`으로 둘러싸지만 튜플은 `()`으로 둘러싼다.
* 리스트는 그 값의 생성, 삭제, 수정이 가능하지만 튜플은 그 값을 바꿀 수 없다.

```python
# 튜플의 모습
t1 = ()
t2 = (1,)
t3 = (1, 2, 3)
t4 = 1, 2, 3
t5 = ('a', 'b', ('ab', 'cd'))
```

* 단지 1개의 요소만을 가질 때는 요소 뒤에 콤마(`,`)를 만드시 붙여야 한다.
* 괄호`()`를 생략해도 무방하다.

> 튜플과 리스트는 비슷한 역할을 하지만 프로그래밍을 할 때 튜플과 리스트는 구별해서 사용하는 것이 유리하다. 튜플과 리스트의 가장 큰 차이는 값을 변화시킬 수 있는가 여부이다. 프로그램이 실행되는 동안 그 값이 항상 변하지 않기를 바란다거나 값이 바뀔까 걱정하고 싶지 않다면 튜플을 사용해야 한다. 반대로 수시로 그 값을 변화시켜야할 경우라면 리스트를 사용해야 한다. 평균적으로 튜플보다는 리스트를 더 많이 사용한다.



### 튜플의 요소값을 지우거나 변경하려고 하면 어떻게 될까?

```python
### 1. 튜플 요솟값을 삭제하려 할 때
t1 = (1, 2, 'a', 'b')
del t1[0]                   # TypeError

### 2. 튜플 요솟값을 변경하려 할 때
t1 = (1, 2, 'a', 'b')
t1[0] = 'c'                 # TypeError
```



### 튜플 다루기


#### 인덱싱하기

```python
t1 = (1, 2, 'a', 'b')
t1[0]                       # 1
t1[3]                       # 'b'
```


#### 슬라이싱하기

```python
t1 = (1, 2, 'a', 'b')
t1[1:]                      # (2, 'a', 'b')
```


#### 튜플 더하기

```python
t1 = (1, 2, 'a', 'b')
t2 = (3, 4)
t1 + t2                     # (1, 2, 'a', 'b', 3, 4)
```


#### 튜플 곱하기

```python
t2 = (3, 4)
t2 * 3          # (3, 4, 3, 4, 3, 4)
```


#### 튜플 길이 구하기

```python
t1 = (1, 2, 'a', 'b')
len(t1)                     # 4
```




## 딕셔너리 자료형



### 딕셔너리란?

* 대응 관계를 나타낼 수 있는 자료형
* 요즘 사용하는 대부분의 언어도 이러한 자료형을 갖고 있는데, 연관 배열(Associative array) 또는 해시(hash)라고 함
* 리스트나 튜플처럼 순차적으로(sequential) 해당 요솟값을 구하지 않고 Key를 통해 Value를 얻음



### 딕셔너리는 어떻게 만들까?

> Key에는 변하지 않는 값을 사용하고, Value에는 변하는 값과 변하지 않는 값 모두 사용할 수 있다.

```python
# 기본 딕셔너리의 모습
{Key1: Value1, Key2: Value2, Key3: Value3, ...}

dic = {'name': 'pey', 'phone': '01199993323', 'birth': '1118'}
a = {1: 'hi'}           # Key로 정수 값 1, Value로 문자열 'hi'
a = {'a': [1,2,3]}      # Value에 리스트
```


#### 딕셔너리 dic의 정보

| key   | value       |
| ----- | ----------- |
| name  | pey         |
| phone | 01199993323 |
| birth | 1118        |



### 딕셔너리 쌍 추가, 삭제하기


#### 딕셔너리 쌍 추가하기

```python
a = {1: 'a'}
a[2] = 'b'
a                       # {1: 'a', 2: 'b'}
a['name'] = 'pey'
a                       # {1: 'a', 2: 'b', 'name': 'pey'}
a[3] = [1, 2, 3]
a
    # {1: 'a', 2: 'b', 'name': 'pey', 3: [1, 2, 3]}
```


#### 딕셔너리 요소 삭제하기

* `del` 함수를 사용해서 `del a[key]`처럼 입력하면 지정한 Key에 해당하는 `{key: value}` 쌍이 삭제

```python
del a[1]
a               # {2: 'b', 'name': 'pey', 3: [1, 2, 3]}
```



### 딕셔너리를 사용하는 방법


#### 딕셔너리에서 Key 사용해 Value 얻기

* 어떤 Key의 Value를 얻기 위해서는 `딕셔너리변수이름[Key]`를 사용

```python
grade = {'pey': 10, 'julliet': 99}
grade['pey']                            # 10
grade['julliet']                        # 99

a = {1: 'a', 2: 'b'}
a[1]                                    # 'a'
a[2]                                    # 'b'

dic = {'name': 'pey', 'phone': '01199993323', 'birth': '1118'}
dic['name']                             # 'pey'
dic['phone']                            # '01199993323'
dic['birth']                            # '1118'
```


#### 딕셔너리 만들 때 주의할 사항

* 딕셔너리에서 Key는 고유한 값이므로 중복되는 Key 값을 설정해 놓으면 하나를 제외한 나머지 것들이 모두 무시됨

```python
a = {1: 'a', 1: 'b'}
a                           # {1: 'b'}
```

* Key에 리스트는 쓸 수 없지만, 튜플은 Key로 쓸 수 있음
* 리스트는 그 값이 변할 수 있기 때문에 Key로 쓸 수 없음

```python
a = {[1, 2]: 'hi'}      # TypeError
```



### 딕셔너리 관련 함수들


#### Key 리스트 만들기(`keys`)

```python
a = {'name': 'pey', 'phone': '01199993323', 'birth': '1118'}
a.keys()        # dict_keys(['name', 'phone', 'birth'])
```

> 파이썬 2.7 버전까지는 `a.keys()` 함수를 호출할 때 반환 값으로 `dict_keys`가 아닌 리스트를 돌려준다. 리스트를 돌려주기 위해서는 메모리 낭비가 발생하는데 파이썬 3.0 이후 버전에서는 이러한 메모리 낭비를 줄이기 위해 `dict_keys` 객체를 돌려준다. 다음에 소개할 `dict_values`, `dict_items` 역시 파이썬 3.0 이후 버전에서 추가된 것들이다. 만약 3.0 이후 버전에서 반환 값으로 리스트가 필요한 경우에는 `list(a.keys())`를 사용하면 된다. `dict_keys`, `dict_values`, `dict_items` 등은 리스트로 변환하지 않더라도 기본적인 반복(iterate) 구문(예:  `for`문)을 실행할 수 있다.

* `dict_keys` 객체는 리스트를 사용하는 것과 차이가 없지만, 리스트 고유의 `append`, `insert`, `pop`, `remove`, `sort` 함수는 수행할 수 없음

```python
for k in a.keys():
    print(k)

    # name
    # phone
    # birth
    
list(a.keys())          # ['name', 'phone', 'birth']
```


#### Value 리스트 만들기(`values`)

```python
# Value만 얻고 싶다면 values 함수를 사용, values 함수를 호출하면 dict_values 객체를 돌려줌
a.values()      # dict_values(['pey', '01199993323', '1118'])
```


#### Key, Value 쌍 얻기(`items`)

```python
# items 함수는 Key와 Value의 쌍을 튜플로 묶은 값을 dict_items 객체로 돌려줌
a.items()
    # dict_items([('name', 'pey'), ('phone', '01199993323'), ('birth', '1118')])
```


#### Key: Value 쌍 모두 지우기(`clear`)

```python
# clear 함수는 딕셔너리 안의 모든 요소를 삭제
a.clear()
a               # {}
```


#### Key로 Value얻기(`get`)

```python
# get(x) 함수는 x라는 Key에 대응되는 Value를 돌려줌
a = {'name': 'pey', 'phone': '01199993323', 'birth': '1118'}
a.get('name')               # 'pey'
a.get('phone')              # '01199993323'

#a.get('name')은 a['name']을 사용했을 때와 동일한 결괏값을 돌려받음
# 다만 a['nokey']처럼 존재하지 않는 키(nokey)로 값을 가져오려고 할 경우 a['nokey']는 Key 오류를 발생시키고 a.get('nokey')는 None을 돌려준다는 차이가 있음
a = {'name': 'pey', 'phone': '01199993323', 'birth': '1118'}
print(a.get('nokey'))       # None
print(a['nokey'])           # KeyError

# 딕셔너리 안에 찾으려는 Key 값이 없을 경우 미리 정해 둔 디폴드 값을 대신 가져오게 하고 싶을 때에는 get(x, '디폴트 값')을 사용
a.get('foo', 'bar')         # 'bar'
```


#### 해당 Key가 딕셔너리 안에 있는지 조사하기(`in`)

```python
a = {'name': 'pey', 'phone': '01199993323', 'birth': '1118'}
'name' in a         # True
'email' in a        # False
```




## 집합 자료형



### 집합 자료형은 어떻게 만들까?

* 집합(set)은 파이썬 2.3부터 지원하기 시작한 자료형으로, 집합에 관련된 것을 쉽게 처리하기 위해 만든 자료형

```python
# set 키워드를 사용해 만듬
s1 = set([1, 2, 3])
s1                      # {1, 2, 3}

# set()의 괄호 안에 리스트를 입력하여 만들거나 문자열을 입력하여 만들 수도 있음
s2 = set("Hello")
s2                      # {'H', 'e', 'l', 'o'}

# 비어 있는 집합 자료형
s = set()
```



### 집합 자료형의 특징

* 중복을 허용하지 않는다.
* 순서가 없다(Unordedred)

리스트나 튜플은 순서가 있기(ordered) 때문에 인덱싱을 통해 자료형의 값을 얻을 수 있지만 set 자료형은 순서가 없기(unordered) 때문에 인덱싱으로 값을 얻을 수 없음; 딕셔너리와 비슷

> 중복을 허용하지 않는 set의 특징은 자료형의 중복을 제거하기 위한 필터 역할로 종종 사용하기도 한다.

```python
s1 = set([1, 2, 3])
l1 = list(s1)
l1                      # [1, 2, 3]
l1[0]                   # 1
t1 = tuple(s1)
t1                      # (1, 2, 3)
t1[0]                   # 1
```



### 교집합, 합집합, 차집합 구하기

```python
s1 = set([1, 2, 3, 4, 5, 6])
s2 = set([4, 5, 6, 7, 8, 9])

### 1. 교집합
s1 & s2                             # {4, 5, 6}
s1.intersection(s2)                 # {4, 5, 6}

### 2. 합집합
s1 | s2                             # {1, 2, 3, 4, 5, 6, 7, 8, 9}
s1.union(s2)                        # {1, 2, 3, 4, 5, 6, 7, 8, 9}

### 3. 차집합
s1 - s2                             # {1, 2, 3}
s2 - s1                             # {8, 9, 7}
s1.difference(s2)                   # {1, 2, 3}
s2.difference(s1)                   # {8, 9, 7}
```



### 집합 자료형 관련 함수들


#### 값 1개 추가하기(`add`)

```python
# 이미 만들어진 set 자료형에 값을 추가
s1 = set([1, 2, 3])
s1.add(4)
s1                      # {1, 2, 3, 4}
```


#### 값 여러 개 추가하기(`update`)

```python
s1 = set([1, 2, 3])
s1.update([4, 5, 6])
s1                          # {1, 2, 3, 4, 5, 6}
```


#### 특정 값 제거하기(`remove`)

```python
s1 = set([1, 2, 3])
s1.remove(2)
s1                      # {1, 3}
```




## 불 자료형



### 불 자료형이란?

* 참(True)과 거짓(False)을 나타내는 자료형

> `True`나 `False`는 파이썬의 예약어로 첫 문자를 항상 대문자로 사용해야 한다.

```python
a = True
b = False
type(a)         # <class 'bool'>
type(b)         # <class 'bool'>

# 조건문의 반환 값으로도 사용
1 == 1          # True
2 > 1           # True
2 < 1           # False
```



### 자료형의 참과 거짓

* 문자열, 리스트, 튜플, 딕셔너리 등의 값이 비어 있으면 거짓, 비어있지 않으면 참
* 숫자는 그 값이 0일 때 거짓
* `None`은 거짓을 뜻함

| 값          | 참 or 거짓 |
| ----------- | ---------- |
| `"python"`  | 참         |
| `""`        | 거짓       |
| `[1, 2, 3]` | 참         |
| `[]`        | 거짓       |
| `()`        | 거짓       |
| `{}`        | 거짓       |
| `1`         | 참         |
| `0`         | 거짓       |
| `None`      | 거짓       |

```python
a = [1, 2, 3, 4]
while a:
    print(a.pop())
    
    # 4
    # 3
    # 2
    # 1

if []:
    print("참")
else:
    print("거짓")

    # 거짓

if [1, 2, 3]:
    print("참")
else:
    print("거짓")

    # 참
```



### 불 연산

```python
bool('python')      # True      # 빈 문자열이 아님
bool('')            # False     # 빈 문자열
bool([1, 2, 3])     # True
bool([])            # False
bool(0)             # False
bool(3)             # True
```




## 자료형의 값을 저장하는 공간, 변수



### 변수는 어떻게 만들까?

* `=`(assignment) 기호 사용
* 파이썬은 변수에 저장된 값을 스스로 판단하여 자료형을 지정

```python
a = 1
b = 'python'
c = [1, 2, 3]
```



### 변수란?

* 객체를 가리키는 것이라고도 말할 수 있음
* `a = [1, 2, 3]`이라고 하면 `[1, 2, 3]` 값을 가지는 리스트 자료형(객체)이 자동으로 메모리에 생성되고 변수 `a`는 `[1, 2, 3]` 리스트가 저장된 메모리의 주소를 가리킴

```python
a = [1, 2, 3]
id(a)               # 1930724084544
```



### 리스트를 복사하고자 할 때

* b와 a와 완전히 동일
* 다만 `[1, 2, 3]` 리스트를 참조하는 변수가 `a` 변수 1개에서 `b` 변수가 추가되어 2개로 늘어났다는 차이만 있을 뿐
* `id(a)`의 값이 `id(b)`의 값과 동일, 즉 `a`가 가리키는 대상과 `b`가 가리키는 대상이 동일하다는 것을 알 수 있음 
* 동일한 객체를 가리키고 있는지에 대해서 판단하는 파이썬 명령어 `is`를 실행해도 참(`True`)을 돌려줌

```python
a = [1, 2, 3]
b = a
id(a)               # 1930724084544
id(b)               # 1930724084544
a is b              # True

a[1] = 4
a                   # [1, 4, 3]
b                   # [1, 4, 3]
```

`b` 변수를 생성할 때 `a` 변수의 값을 가져오면서 `a`와는 다른 주소를 가리키도록 만들수는 없을까?


#### 1. `[:]` 이용

```python
a = [1, 2, 3]
b = a[:]
a[1] = 4
a                   # [1, 4, 3]
b                   # [1, 2, 3]
```


#### 2. `copy` 모듈 이용

```python
from copy import copy
b = copy(a)
b is a                      # False     # b = a[:]과 동일
```



### 변수를 만드는 여러 가지 방법

```python
# 튜플로 a, b에 값 대입 (동일)
a, b = ('python', 'life')
(a, b) = 'python', 'life'

# 리스트로 변수 만들기
[a, b] = ['python', 'life']

# 여러 개의 변수에 같은 값 대입
a = b = 'python'

# 두 변수의 값 바꾸기
a = 3
b = 5
a, b = b, a
a                               # 5
b                               # 3
```