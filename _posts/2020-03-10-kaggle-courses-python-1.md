---
layout: article
title: Python 기본 문법 중 특이한 점
tags: python,kaggle-courses
author: alphachip
aside:
  toc: true
---
## 변수, 숫자

### 변수<sup>dd</sup>
* 선언 안해도 됨
* 타입명 기입 안해도 됨
* 대입하는 종류에 따라 자동으로 타입 변경됨 => 타입 아무거나 넣어도 된다

### 변수 타입 확인
```python
a=1;
type(a)
a=1.1;
type(a)
```

### 형변환
{% highlight python %}
print(float(1))
print(int(1.11))
print(int(‘1’)+1)
{% endhighlight %}

### swap
{% highlight python %}
a=[1,2,3]
b=[3,2,1]
a,b=b,a
#a는 b의 배열, b는 a의 배열로 swap됨
{% endhighlight %}

### 연산
{% highlight python %}
print(5/2)
print(6/2)

print(5//2)
print(6//2)
{% endhighlight %}

### 반복문
{% highlight python %}
a=2
if a>0:
  print("over")
print(song)
{% endhighlight %}

### 숫자를 이용한 String 반복 출력
{% highlight python %}
song="La"*3
print(song)
{% endhighlight %}

### 숫자 관련 함수
`min`,`max`,`abs`함수를 라이브러리 import 필요 없이 사용 가능
{% highlight python %}
print(min(1,2,3))
print(max(1,2,3))

print(abs(2))
print(abs(-2))
{% endhighlight %}

### 주석
{% highlight python %}
#어쩌구
{% endhighlight %}


## 함수

### help : 어떤 함수인지 궁금할 때.
{% highlight python %}
help(round)
{% endhighlight %}
round 함수에 대한 설명을 볼 수 있다.

*주의*
* *함수에 대한 이름만 쓸 것.*
* *함수를 사용하지 말 것.*
* *잘못된 예: `help(round(-2.01))`*
* *int가 반환되어 int에 대한 설명을 볼 수 있음.;*

### print 함수
{% highlight python %}
print(1, 2, 3, sep=' < ')
{% endhighlight %}
값들 사이에 `<`가 추가

기본 값은 공백

### 함수 선언과 사용
{% highlight python %}
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
    least_difference(1, 10, 100),
    least_difference(1, 10, 10),
    least_difference(5, 6, 7), #여기서 쉼표 가능
)
{% endhighlight %}
`””” “””`로 묶어준 것은 help함수를 썼을 때 사용자 정의 함수에 대한 설명을 해준다

`>>>`이거는 배시를 뜻하는 걸로, 예시를 표현할 때 사용

### 함수 인자
{% highlight python %}
def greet(who="Colin"):
    print("Hello,", who)
    
greet()
greet(who="Kaggle")
greet("world")
{% endhighlight %}
다양한 매개변수 입력 방법. 디폴트 값을 지정할 수 있다.

### 반환 값이 없을 때
`None`을 반환한다. (`null`혹은 `NULL`과 같은 의미)
{% highlight python %}
mystery = print()
print(mystery)
{% endhighlight %}

### 함수 중첩
{% highlight python %}
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
{% endhighlight %}

### 함수 일괄 적용
{% highlight python %}
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
{% endhighlight %}
`’Which number is the biggest modulo 5?’`에서
`100%5`,`51%5`,`14%5`의 결과는 각각

`0`,`1`,`4`이다. 이 중 가장 큰 결과값을 가진 것은 `4`, 즉 `14`가 반환.


##
