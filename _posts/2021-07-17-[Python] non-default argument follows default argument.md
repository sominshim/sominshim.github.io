---
layout: single
title:  "[Python] non-default argument follows default argument"
categories: [Python]
tags: [Python, error]

toc: true
toc_sticky: true
toc_label: "목차"
---


다음과 같은 코드를 작성할 때, **SyntaxError: non-default argument follows default argument** 에러 메세지가 나온다.
````
def count(element=1, a):   
    return a + element
````

- non-default argument: default 값이 없는 인자
- default argument: default 값이 있는 인자

즉, 함수를 정의할 때 먼저 default 값이 지정된 인자가 오면 안된다는 에러 메세지이다.

다음과 같이 함수 인자의 위치면 변경해주면 실행이 가능해진다 :)
````
def count(a, element=1):   
    return a + element
````


> Why? 왜일까? - Python 문법상 그렇다고 한다.

### 순서상 default arguement를 앞에 배치하고 싶을 때 방법이 없을까?
다행이도 방법은 있었다.

````
def count(element=1, *args, a):   
    return a + element
````
이와 같이 **Variable Length Positional Arguments**를 주면 된다.

위 소스 코드에서 element는 default지만, Positional한 Parameter의 부분에 있는 것이고, a는 Keyword Argument 방식으로 줘야하는 Parameter 부분에 있기 때문에, 이런 경우에는 가능하다.

참고로, args라는 Parameter는 값을 줘도, 안 줘도 된다.

다시 정리하면, a에만 Keyword Arguement 방식으로 주면 에러가 발생하지 않는다.

앞에 element는 Positional하게 값을 줘도 되고, Keyword 방식으로 줘도 된다.


---
[참고 사이트](https://getkt.com/blog/python-keyword-only-arguments/)
[참고 사이트를 보고 정리한 블로그](https://velog.io/@minho/SyntaxError-non-default-argument-follows-default-argument)
