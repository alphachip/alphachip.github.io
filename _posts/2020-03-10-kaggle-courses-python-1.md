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

## calculating
```python
return (int(ketchup) + int(mustard) + int(onion)) == 1 #int() 안 써도 됨
```
위 코드와 아래 코드는 같은 결과가 나온다
```python
return (ketchup + mustard + onion) == 1
```
`True+False+False=1`로 계산

# conditionals
* `if`, `elif`, `else` 이용
* `elif` 는 다른 언어의 `else if` 의 의미와 같음.
* 조건문 내의 명령어를 여러 줄 입력하고 싶으면 줄을 맞추자

## NOT `bool` can use statement
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

# Loops

## using
```python
planets = ['Mercury', 'Venus', 'Earth', 'Mars', 'Jupiter', 'Saturn', 'Uranus', 'Neptune']
for planet in planets:
    print(planet, end=' ')
#Mercury Venus Earth Mars Jupiter Saturn Uranus Neptune
```
tuple도 가능

string 예시
```python
s = 'steganograpHy is the practicE of conceaLing a file, message, image, or video within another fiLe, message, image, Or video.'
msg = ''
# print all the uppercase letters in s, one at a time
for char in s:
    if char.isupper():
        print(char, end='') 
#HELLO
```

## `range()`
```python
for i in range(5): #숫자 순서대로 하나씩 반환
    print("Doing important work. i =", i)
#Doing important work. i = 0
#Doing important work. i = 1
#Doing important work. i = 2
#Doing important work. i = 3
#Doing important work. i = 4
```

## `while`
```python
i = 0
while i < 10: #false 될 때까지 실행
    print(i, end=' ')
    i += 1
```

## + list
```python
squares = [n**2 for n in range(10)]
squares
#[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```
아래는 같은 결과의 코드
```python
squares = []
for n in range(10):
    squares.append(n**2)
squares
#[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

## +if문
```python
short_planets = [planet for planet in planets if len(planet) < 6]
short_planets
#['Venus', 'Earth', 'Mars']
```

## +변형
```python
#개행으로 가독성을 높임.
loud_short_planets =[
    planet.upper() + '!' 
    for planet in planets #SQL에서 SELECT, FROM
    if len(planet) < 6 #WHERE
]
loud_short_planets
#['VENUS!', 'EARTH!', 'MARS!'] #loud_short_planets 부분만 빼도 같은 결과 나옴
```

## `any()`
List에 1이 하나라도 있으면 True를 반환하는 프로그램 짜는 방법

1.
```python
def has_lucky_number(nums):
    return any([num ==1 for num in nums])
```
배열 등 반복 가능 한 곳에  하나라도 `bool()`했을 때 `True`가 나오면 True, 비어있을 땐 False 반환
```

2.
```python
def has_lucky_number(nums):
    for num in nums:
        if num % 7 == 0:
            return True
    # We've exhausted the list without finding a lucky number
    return False
```

3.
```python
def has_number_one(nums):
    return len([True for num in nums if num%7==])>0
```

## **Error**: comparing `list` to `int`
```python
[1,2,3,4]>2 #error
```

## Example: compact coding 1
list `L`의 원소 각각이 int `thresh` 보다 큰지 아닌지 결과를 배열로 출력
```python
def elementwise_greater_than(L, thresh):
    res = []
    for ele in L:
        res.append(ele > thresh)
    return res
```
more compact code below
```python
def elementwise_greater_than(L, thresh):
    return [ele > thresh for ele in L]
```

## Example: compact coding 2
```python
def count_negatives(nums):
    """Return the number of negative numbers in the given list.
    
    >>> count_negatives([5, -1, -2, 0, 3])
    2
    """
    n_negative = 0
    for num in nums:
        if num < 0:
            n_negative = n_negative + 1
    return n_negative
```
이것을 아래와 같이 한 줄로 줄일 수 있다
```python
def count_negatives(nums):
    return len([num for num in nums if num < 0])
```
또한 아래와 같이 더 줄일 수 있다
```python
def count_negatives(nums):
    return sum([num < 0 for num in nums]) # True + True + False + True=3.
```

## compact readable program (readable>compact)
> 짧은 코드가 항상 좋다. 하지만 아래([The Zen of Python](https://en.wikipedia.org/wiki/Zen_of_Python))를 기억할 것
> Readability counts.
> Explicit is better than implicit.
