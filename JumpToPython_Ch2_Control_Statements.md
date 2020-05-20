# 제어문




## `if`문



### `if`문은 왜 필요할까?

* 조건을 판단하여 해당 조건에 맞는 상황을 수행하는데 쓰임

```python
money = True
if money:
    print("택시를 타고 가라")
else:
    print("걸어 가라")

# 택시를 타고 가라
```



### `if`문의 기본 구조

* 조건문을 테스트해서 참이면 `if`문 바로 다음 문장(`if` 블록)들을 수행하고, 조건문이 거짓이면 `else`문 다음 문장(`else` 블록)

```python
if 조건문:
    수행할 문장1
    수행할 문장2
    ...
else:
    수행할 문장A
    수행할 문장B
    ...
```



### 들여쓰기

* `if`문을 만들 때는 `if 조건문`: 바로 아래 문장부터 `if`문에 속하는 모든 문장에 들여쓰기(indentation)

> 요즘 파이썬 커뮤니티에서는 들여쓰기를 할 때 공백(Spacebar) 4개를 사용하는 것을 권장한다.

> `if` 조건문 뒤에는 반드시 콜론(`:`)이 붙는다. 어떤 특별한 의미가 있다기보다는 파이썬의 문법 구조이다. 왜 하필 콜론(`:`)인지 궁금하다면 파이썬을 만든 귀도에게 직접 물어보아야 할 것이다. 앞으로 배울 `while`이나 `for`, `def`, `class`문에도 역시 문장의 끝에 콜론(`:`)이 항상 들어간다. 초보자들은 이 콜론(`:`)을 빠뜨리는 경우가 많으니 특히 주의하자.
>
> 파이썬이 다른 언어보다 보기 쉽고 소스 코드가 간결한 이유는 바로 콜론(`:`)을 사용하여 들여쓰기(indentation)를 하도록 만들었기 때문이다. 하지만 이는 숙련된 프로그래머들이 파이썬을 처음 접할 때 가장 혼란스러워하는 부분이기도 하다. 다른 언어에서는 `if`문을 `{}` 기호로 감싸지만 파이썬에서는 들여쓰기로 해결한다는 점을 기억하자.

```python
if 조건문:
    수행할 문장1
    수행할 문장2
    수행할 문장3

# 오류 발생
if 조건문:
    수행할 문장1
수행할 문장2                # 들여쓰기
    수행할 문장3

# 오류 발생: 들여쓰기는 언제나 같은 너비로 해야 한다.
if 조건문:
    수행할 문장1
    수행할 문장2
        수행할 문장3        # 들여쓰기
```



### 조건문이란 무엇인가?

* 참과 거짓을 판단하는 문장

```python
# 조건문: money
money = True
if money:
```


#### 비교연산자

| 비교연산자 | 설명                  |
| ---------- | --------------------- |
| x < y      | x가 y보다 작다        |
| x > y      | x가 y보다 크다        |
| x == y     | x와 y가 같다          |
| x != y     | x와 y가 같지 않다     |
| x >= y     | x가 y보다 크거나 같다 |
| x <= y     | x가 y보다 작거나 같다 |

```python
x = 3
x = 2
x > y       # True
x < y       # False
x == y      # False
x != y      # True

# 만약 3000원 이상의 돈을 가지고 있으면 택시를 타고 그렇지 않으면 걸어 가라.
money = 2000
if money >= 3000:
    print("택시를 타고 가라")
else:
    print("걸어가라")

    # 걸어가라
```


#### `and`, `or`, `not`

| 연산자  | 설명                                |
| ------- | ----------------------------------- |
| x or y  | x와 y 둘중에 하나만 참이어도 참이다 |
| x and y | x와 y 모두 참이어야 참이다          |
| not x   | x가 거짓이면 참이다                 |

```python
# 돈이 3000원 이상 있거나 카드가 있다면 택시를 타고 그렇지 않으면 걸어 가라.
money = 2000
card = True
if money >= 3000 or card:
    print("택시를 타고 가라")
else:
    print("걸어가라")

    # 택시를 타고 가라
```


#### `x in s`, `x not in s`

| `in`          | `not in`          |
| ------------- | ----------------- |
| `x in 리스트` | `x not in 리스트` |
| `x in 튜플`   | `x not in 튜플`   |
| `x in 문자열` | `x not in 문자열` |

```python
1 in [1, 2, 3]              # True
1 not in [1, 2, 3]          # False
'a' in ('a', 'b', 'c')      # True
'j' not in 'python'         # True

# 만약 주머니에 돈이 있으면 택시를 타고, 없으면 걸어 가라.
pocket = ['paper', 'cellphone', 'money']
if 'money' in pocket:
    print("택시를 타고 가라")
else:
    print("걸어가라")

    # 택시를 타고 가라
```


#### 조건문에서 아무 일도 하지 않게 설정하고 싶다면?

```python
# 주머니에 돈이 있으면 가만히 있고 주머니에 돈이 없으면 카드를 꺼내라.
pocket = ['paper', 'money', 'cellphone']
if 'money' in pocket:
    pass
else:
    print("카드를 꺼내라")

    # 아무 결괏값도 보여주지 않음
```



### 다양한 조건을 판단하는 `elif`

```python
# 주머니에 돈이 있으면 택시를 타고,
# 주머니에 돈은 없지만 카드가 있으면 택시를 타고,
# 돈도 없고 카드도 없으면 걸어 가라.
pocket = ['paper', 'handphone']
card = True
if 'money' in pocket:
    print("택시를 타고가라")
else:
    if card:
        print("택시를 타고가라")
    else:
        print("걸어가라")

    # 택시를 타고가라

# elif 사용
if 'money' in pocket:
    print("택시를 타고가라")
elif card:
    print("택시를 타고가라")
else:
    print("걸어가라")

    # 택시를 타고가라
```

* `elif`는 이전 조건문이 거짓일 때 수행
* `if`, `elif`, `else`를 모두 사용할 때 기본 구조
* `elif`는 개수에 제한 없이 사용할 수 있음

```python
if 조건문:
    수행할 문장1
    수행할 문장2
    ...
elif 조건문:
    수행할 문장1
    수행할 문장2
    ...
elif 조건문:
    수행할 문장1
    수행할 문장2
    ...
...
else:
    수행할 문장1
    수행할 문장2
    ...
```


#### `if`문을 한 줄로 작성하기

```python
if 'money' in pocket:
    pass
else:
    print("카드를 꺼내라")

pocket = ['paper', 'money', 'cellphone']
if 'money' in pocket: pass
else: print("카드를 꺼내라")
```



### 조건부 표현식

```python
if score >= 60:
    message = "success"
else:
    message = "failure"

# 파이썬의 조건부 표현식(conditional expression)
message = "success" if score >= 60 else "failure"
```

```python
# 조건부 표현식 정의
조건문이 참인 경우 if 조건문 else 조건문이 거짓인 경우
```




## `while`문



### `while`문의 기본 구조

* 반복해서 문장을 수행해야 할 경우

```python
while 조건문:
    수행할 문장1
    수행할 문장2
    수행할 문장3
    ...
```

* `while`문은 조건문에 참인 동안에 `while`문 아래의 문장이 반복해서 수행

```python
treeHit = 0
while treeHit < 10:
    treeHit = treeHit + 1
    print("나무를 %d번 찍었습니다." % treeHit)
    if treeHit == 10:
        print("나무 넘어갑니다.")

    # 나무를 1번 찍었습니다.
    # 나무를 2번 찍었습니다.
    # 나무를 3번 찍었습니다.
    # 나무를 4번 찍었습니다.
    # 나무를 5번 찍었습니다.
    # 나무를 6번 찍었습니다.
    # 나무를 7번 찍었습니다.
    # 나무를 8번 찍었습니다.
    # 나무를 9번 찍었습니다.
    # 나무를 10번 찍었습니다.
    # 나무 넘어갑니다.

# while문의 조건문: treeHit < 10; treeHit가 10보다 작은 동안에 while문 안의 문장을 계속 수행
# while문 안의 문장
#     treeHit = treeHit + 1로 treeHit 값이 계속 1씩 증가
#     나무를 treeHit번만큼 찍었음을 알리는 문장 출력
#     treeHit가 10이 되면 "나무 넘어갑니다."라는 문장을 출력
#     treeHit < 10 조건문이 거짓이 되므로 while을 빠져나감
```



### `while`문 만들기

```python
prompt = """
1. Add
2. Del
3. List
4. Quit
"""
number = 0
while number != 4:
    print(prompt)
    number = int(input())
```

* `number`가 4가 아닌 동안 `prompt`를 출력하고 사용자로부터 번호를 입력받음
* 사용자가 값 4를 입력하지 않으면 계속해서 `prompt`를 출력
* 4를 입력하면 조건문이 거짓이 되어 `while`문을 빠져나감



### `while`문 강제로 빠져나가기

```python
coffee = 10
money = 300
while money:
    print("돈을 받았으니 커피를 줍니다.")
    coffee = coffee - 1
    print("남은 커피의 양은 %d개입니다." % coffee)
    if coffee == 0:
        print("커피가 다 떨어졌습니다. 판매를 중지합니다.")
        break
```

* `break`문이 호출되어 `while`문을 빠져나감

```python
# coffee.py

coffee = 10
while True:
    money = int(input("돈을 넣어 주세요: "))
    if money == 300:
        print("커피를 줍니다.")
        coffee = coffee - 1
    elif money > 300:
        print("거스름돈 %d를 주고 커피를 줍니다." % (money-300))
        coffee = coffee - 1
    else:
        print("돈을 다시 돌려주고 커피를 주지 않습니다.")
        print("남은 커피의 양은 %d개 입니다." % coffee)
    if coffee == 0:
        print("커피가 다 떨어졌습니다. 판매를 중지 합니다.")
        break
```



### `while`문의 맨 처음으로 돌아가기

* `while`문을 빠져나가지 않고 `while`문의 맨 처음(조건문)으로 다시 돌아가게 만들고 싶은 경우
* 이때 사용하는 것이 `continue`문

```python
a = 0
while a < 10:
    a = a + 1
    if a % 2 == 0: continue
    print(a)

    # 1
    # 3
    # 5
    # 7
    # 9
```



### 무한 루프

* 무한 루프의 기본 형태

```python
while True:
    수행할 문장1
    수행할 문장2
    ...
```

* 무한 루프의 예

```python
while True:
    print("Ctrl+C를 눌러야 while문을 빠져나갈 수 있습니다.")

    ...
    # Ctrl+C를 눌러야 while문을 빠져나갈 수 있습니다.
    # Ctrl+C를 눌러야 while문을 빠져나갈 수 있습니다.
    # Ctrl+C를 눌러야 while문을 빠져나갈 수 있습니다.
    ...
```




## `for`문



### `for`문의 기본 구조

```python
for 변수 in 리스트(또는 튜플, 문자열):
    수행할 문장1
    수행할 문장2
    ...
```



### 예제를 통해 `for`문 이해하기


#### 1. 전형적인 `for`문

```python
test_list = ['one', 'two', 'three']
for i in test_list:
    print(i)

    # one
    # two
    # three
```


#### 2. 다양한 `for`문의 사용

```python
a = [(1, 2), (3, 4), (5, 6)]
for (first, last) in a:
    print(first + last)

    # 3
    # 7
    # 11
```



#### 3. `for`문의 응용

```python
# 총 5명의 학생이 시험을 보았는데 시험 점수가 60점이 넘으면 합격이고 그렇지 않으면 불합격이다.
# 합격인지 불합격인지 결과를 보여 주시오.
# marks1.py
marks = [90, 2, 67, 45, 80]
number = 0
for mark in marks:
    number = number + 1
    if mark >= 60:
        print("%d번 학생은 합격입니다." % number)
    else:
        print("%d번 학생은 불합격입니다." % number)

    # 1번 학생은 합격입니다.
    # 2번 학생은 불합격입니다.
    # 3번 학생은 합격입니다.
    # 4번 학생은 불합격입니다.
    # 5번 학생은 합격입니다.
```



### `for`문과 `continue`

```python
# marks2.py
marks = [90, 2, 67, 45, 80]
number = 0
for mark in marks:
    number = number + 1
    if mark < 60:
        continue
    print("%d번 학생 축하합니다. 합격입니다." % number)

    # 1번 학생 축하합니다. 합격입니다.
    # 3번 학생 축하합니다. 합격입니다.
    # 5번 학생 축하합니다. 합격입니다.
```



### `for`문과 함께 자주 사용하는 `range` 함수

* `range(10)`은 0부터 10 미만의 숫자를 포함하는 `range` 객체를 만들어 줌
* 시작 숫자와 끝 숫자를 지정하려면 `range(시작 숫자, 끝 숫자)` 형태를 사용하는데, 이때 끝 숫자는 포함되지 않음


#### `range` 함수의 예시 살펴보기

```python
add = 0
for i in range(1, 11):
    add = add + i
print(add)                  # 55
```

* 60점 이상이면 합격 예제

```python
# marks3.py
marks = [90, 25, 67, 45, 80]
for number in range(len(marks)):
    if marks[number] < 60:
        continue
    print("%d번 학생 축하합니다. 합격입니다." % (number+1))
```


#### `for`와 `range`를 이용한 구구단

```python
for i in range(2, 10):
    for j in range(1, 10):
        print(i*j, end=" ")
    print('')

    # 2 4 6 8 10 12 14 16 18
    # 3 6 9 12 15 18 21 24 27
    # 4 8 12 16 20 24 28 32 36
    # 5 10 15 20 25 30 35 40 45
    # 6 12 18 24 30 36 42 48 54
    # 7 14 21 28 35 42 49 56 63
    # 8 16 24 32 40 48 56 64 72
    # 9 18 27 36 45 54 63 72 81
```

> 앞의 예제에서 `print(i*j, end=" ")`와 같이 매개변수 `end`를 넣어준 이유는 해당 결괏값을 출력할 때 다음줄로 넘기지 않고 그 줄에서 계속해서 출력하기 위해서이다. 그다음에 이어지는 `print(' ')`는 2단, 3단 등을 구분하기 위해 두 번째 `for`문이 끝나면 결괏값을 다음 줄부터 출력하게 해주는 문장이다.



### 리스트 내포 사용하기

* 리스트 안에 `for`문을 포함하는 리스트 내포(List comprehension)를 사용하면 좀 더 편리하고 직관적인 프로그램을 만들 수 있음

```python
a = [1, 2, 3, 4]
result = []
for num in a:
    result.append(num*3)
print(result)                       # [3, 6, 9, 12]

# 리스트 내포 사용
a = [1, 2, 3, 4]
result = [num * 3 for num in a]
print(result)                       # [3, 6, 9, 12]

# 리스트 내포 안에 "if 조건" 사용
a = [1, 2, 3, 4]
result = [num * 3 for num in a if num % 2 == 0]
print(result)                       # [6, 12]
```

* 리스트 내포의 일반 문법

```python
[표현식 for 항목 in 반복가능객체 if 조건문]

# for문을 2개 이상 사용 가능
[표현식 for 항목1 in 반복가능객체1 if 조건문1
        for 항목2 in 반복가능객체2 if 조건문2
        ...
        for 항목n in 반복가능객체n if 조건문n]
```

* 리스트 내포를 사용하여 구구단 구현

```python
result = [x*y for x in range(2, 10)
              for y in range(1, 10)]
print(result)

    # [2, 4, 6, 8, 10, 12, 14, 16, 18, 3, 6, 9, 12, 15, 18, 21, 24, 27, 4, 8, 12, 16, 20, 24, 28, 32, 36, 5, 10, 15, 20, 25, 30, 35, 40, 45, 6, 12, 18, 24, 30, 36, 42, 48, 54, 7, 14, 21, 28, 35, 42, 49, 56, 63, 8, 16, 24, 32, 40, 48, 56, 64, 72, 9, 18, 27, 36, 45, 54, 63, 72, 81]
```