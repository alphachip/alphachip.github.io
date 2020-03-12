---
layout: article
title: Python 기본 문법
tags: [python,kaggle-courses]
author: alphachip
aside:
  toc: true
---

# 변수, 숫자

## assigning variable
* 선언 안해도 됨
* 타입명 기입 안해도 됨
* 대입하는 종류에 따라 자동으로 타입 변경됨 => 타입 아무거나 넣어도 된다

## `type()`
```python
a=1;
type(a) #int
a=1.1;
type(a) #float
```

## `float()`, `int()` : chainging type
```python
print(float(1)) #1.0
print(int(1.11)) #1
print(int('1')+1) #2
```

## `/`, ``//`` 
```python
print(5/2) #2.5
print(6/2) #3.0

print(5//2) #2
print(6//2) #3
```

## 숫자를 이용한 String 반복 출력
```python
song="La"*3
print(song)
```

## `min()`, `max()`, `abs()`
* `min()`, `max()`, `abs()` don't need to import library
```python
print(min(1,2,3)) #1
print(max(1,2,3)) #3

print(abs(2)) #2
print(abs(-2)) #2
```

## 주석
```python
#어쩌구
```


# functions

## `help()` : 어떤 함수인지 궁금할 때.
```python
help(round)
```

*주의*
* *함수에 대한 이름만 쓸 것.*
* *함수를 사용하지 말 것.*
* *잘못된 예: `help(round(-2.01))` -> int가 반환되어 int에 대한 설명을 볼 수 있음.;*

## `print()`
```python
print(1, 2, 3) #1 2 3 #default: 공백
print(1, 2, 3, sep=' < ') #1<2<3
```

## defining and using
```python
def least_difference(a, b, c):
    """Return the smallest difference between any two numbers
    among a, b and c.
    
    >>> least_difference(1, 5, -5)
    4
    """
    diff1 = abs(a - b)
    diff2 = abs(b - c)
    diff3 = abs(a - c)
    return min(diff1, diff2, diff3)

print(
    least_difference(1, 10, 100), #9
    least_difference(1, 10, 10), #0
    least_difference(5, 6, 7), #1 #여기서 `,` 가능
)
```
`””” “””`로 묶어준 것은 help함수를 썼을 때 사용자 정의 함수에 대한 설명을 해준다

`>>>`이거는 배시를 뜻하는 걸로, 예시를 표현할 때 사용

## params
```python
def greet(who="Colin"): #default:Colin
    print("Hello,", who)
    
greet() #Colin
greet(who="Kaggle") #Kaggle
greet("world") #world
```
다양한 매개변수 입력 방법.

## `None` : return nothing
`null`혹은 `NULL`과 같은 의미
```python
mystery = print()
print(mystery) #None
```

## 함수 중첩
```python
def mult_by_five(x):
    return 5 * x

def call(fn, arg):
    """Call fn on arg"""
    return fn(arg)

def squared_call(fn, arg):
    """Call fn on the result of calling fn on arg"""
    return fn(fn(arg))

print(
    call(mult_by_five, 1),
    squared_call(mult_by_five, 1),
    sep='\n', # '\n' is the newline character - it starts a new line
)
#5
#25
```

## 함수 일괄 적용
```python
def mod_5(x):
    """Return the remainder of x after dividing by 5"""
    return x % 5

print(
    'Which number is biggest?',
    max(100, 51, 14),
    'Which number is the biggest modulo 5?',
    max(100, 51, 14, key=mod_5),
    sep='\n',
)
```
`’Which number is the biggest modulo 5?’`에서
`100%5`,`51%5`,`14%5`의 결과는 각각

`0`,`1`,`4`이다. 이 중 가장 큰 결과값을 가진 것은 `4`, 즉 `14`가 반환.


# bool
## `int` 형과 `float` 형 비교 가능
```python
3.0 == 3 #True
```

## `string` 과 `int` 비교 불가
```python
‘3’ == 3 #False
```

## result using `bool()`
```python
print(bool(1)) #True # all numbers are treated as true, except 0
print(bool(0)) #False
print(bool("asf")) # True # all strings are treated as true, except the empty string ""
print(bool("")) #False
```


## `and` `or` `not`

* Don't using `&&` or `||` or `!`

```python
def can_run_for_president(age, is_natural_born_citizen):
    """Can someone of the given age and citizenship status run for president in the US?"""
    # The US Constitution says you must be a natural born citizen *and* at least 35 years old
    return is_natural_born_citizen and (age >= 35)

print(can_run_for_president(19, True)) #False
print(can_run_for_president(55, False)) #False
print(can_run_for_president(55, True)) #True
```

```python
True or True and False #True
```

`and` 가 `or` 보다 우선 순위가 높다.

가독성을 위해서는 `()`를 쓰자. 길다면 개행을 하여 여러줄로 쓰는 것도 좋다.

## cf. return value
```python
return (int(ketchup) + int(mustard) + int(onion)) == 1
```
이것을
```python
return (ketchup + mustard + onion) == 1
```
이렇게 해도 `bool` 형태로 반환

# conditionals
* `if`, `elif`, `else` 이용
* `elif` 는 다른 언어의 `else if` 의 의미와 같음.
* 조건문 내의 명령어를 여러 줄 입력하고 싶으면 줄을 맞추자

## bool  형식이 아닌 것을 조건문으로
`if 0` 이나 `if "a"`이런 식으로 bool 함수 쓰지 않고도 조건문으로 쓸 수 있음

## 삼항 조건 연산자<sup>ternary</sup>
```python
if grade < 50:
        outcome = 'failed'
    else:
        outcome = 'passed'
```
이것을

```python
outcome = 'failed' if grade < 50 else 'passed'
```
 이렇게 변환 가능

```python
print("Splitting", total_candies, "candy" if total_candies == 1 else "candies")
```

# List
* 순서 있는 배열
* 다양한 종류 한 배열에 가능
* 변경 가능

## creating
```python
hi = [“hihi”,1, help]
hands = [
    ['J', 'Q', 'K'],
    ['2', '2', '2'],
    ['6', 'A', 'K'], # (Comma after the last element is optional)
]
```

## indexing
```python
hi[0]
hi[-1]
```
`-1` 은 뒤에서 첫번째를 가르킴

## slicing
```python
hi[0:1] #0포함~1이전
hi[:1] #처음부터 1이전까지
hi[1:] #1부터 끝까지
hi[1:-1] #1~마지막이전
hi[-2:] #마지막 2개1
```

## changing
바로 위의 indexing과 slicing을 이용해 선언하듯 바로 대입해 변경 가능(반복문 불필요)

## `len()`
```python
len(hi) #배열 길이 출력
a = [1, 2, 3] #길이 3
b = [1, [2, 3]] #[2,3]은 1개 취급
c = [] #0
d = [1, 2, 3][1:] #[2,3]과 같음
```

## `sorted()`
```python
sorted(alphabet_array) #알파벳 순 정렬
```

## `sum()`
```python
sum(int_array) #배열 안의 숫자들 합계 반환
```

## `max()`
```python
max(int_array) #배열 중 가장 큰 값 반환
```

## `append()`
```python
hi.append('yo') #리스트 끝에 추가됨
```
`append()` 는 list 내에서 쓰이는 함수

## `pop()`
```python
hi.pop() # it removes and returns the last element of a list
```

## searching
```python
hi.index('yo') #없는 원소를 입력하면 오류 발생
"aaaa" in hi #To avoid error. it returns True/False
```

## swap
```python
a=[1,2,3]
b=[3,2,1]
a,b=b,a #a는 b의 배열, b는 a의 배열로 swap됨
```

# Tuples
* List와의 차이점 1. `()`사용. 심지어 선언할 때 사용 안해도 됨
* 차이점 2. 변경 불가

## 선언
```python
t=(1,2,3)
a=1,2,3 #위와 동일
```

## `as_integer_ratio()`
```python
x=0.125
numerator, denominator = x.as_integer_ratio() #분수의 분자와 분모를 반환. (1, 8)
#numerator=1, denominator=8 대입
```

