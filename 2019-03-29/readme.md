# 프로그래밍 튜터링 002 (전)

##### 19.03.29 (금)

* 오늘의 강의 내용 (lec 03 && 04 해당)

1. 자료구조 (list)
2. 반복문 (while/for)
3. 함수

------------------------------------------

* 강의 방식

1. 간단한 이론 설명
2. (기본 or 헷갈리기 쉬운) 예제
3. 실습

------------

### 1. List

- 정의와 개념

  ```python
  # defining lists
  t1 = [42, 1024, 34] # a list with 3 elements
  print(t1)
  
  t2 = [] # empty list
  print(t2)
  ```

  ```
  [42, 1024, 34]
  []
  ```

  * mutable sequences: 원소의 추가/삭제/변경 가능 (<-> tuple/string)

  - 원소의 자료형: 임의의 자료형의 원소를 저장할 수 있음
  - 인덱스(index): 0부터 시작하는 정수로 원소의 순서 나타냄, 음수일 경우 마지막 원소부터 역순으로 접근

  

- 여러가지 연산

  ```python
  # in/not in
  a = ['python','is']
  print('python' in a) 
  print('cool' not in a)
  
  # list의 덧셈
  b = ['DGIST']
  c = a + b
  print(c)
  
  # 곱셈
  d = b * 3
  print(d)
  ```

  ```
  True # 1
  True
  ['python','is','DGIST'] # 2
  ['DGIST','DGIST','DGIST'] # 3
  ```



*  리스트에 원소 추가하기

  ```python
  # append : 원소를 추가
  a = [1, 2, 3]
  a.append(4)
  print(a)
  
  a.append([5])
  print(a)
  
  # extend : 다른 리스트의 원소를 추가
  b = [3, 6, 9]
  b.extend([12])
  print(b)
  
  b.extend([[15, 18]])
  print(b)
  ```

  ```
  [1, 2, 3, 4]
  [1, 2, 3, 4, [5]]
  [3, 6, 9, 12]
  [3, 6, 9, [15, 18]]
  ```



* 리스트에서 원소 삭제하기

  ```python
  # delete : 특정 인덱스의 원소 삭제
  a = ['red', 'orange', 'yellow', 'green']
  del a[3]
  print(a)
  
  # remove : 특정 원소 삭제
  a.remove('red')
  print(a)
  ```

  ```
  ['red', 'orange', 'yellow']
  ['orange', 'yellow']
  ```

  

* 리스트에서 원소 / 원소의 개수 찾기

  ```python
  # index : 특정 원소의 index 찾기 (문자열에서도 사용 가능)
  a = ['Hi', 'I', 'am', 'happy']
  print(a.index('happy'))
  
  # count : 특정 원소의 갯수 세기
  b = ['apple', 'apple', 'banana', 'banana', 'banana']
  print(b.count('apple'))
  print(b.count('banana'))
  ```

  ```
  2
  2
  3
  ```

  

* 리스트 슬라이싱

  * name_of_list[start:end]
    - name_of_list의 [start, end)에 위치한 원소들을 갖는 리스트 생성
    - start: 생략되면 첫 원소부터
    - end: 생략되면마지막원소까지

  ```python
  # [start:end)
  # start는 포함하고 end는 포함하지 않음
  
  t = [0, 1, 2, 3, 4, 5]
  print(t)
  print(t[1:4])
  print(t[3:])
  print(t[:2])
  print(t[-3]) # 음수는 리스트의 마지막 원소부터 접근
  print(t[:]) # t의 모든 원소를 copy
  ```

  ```
  [0, 1, 2, 3, 4, 5]
  [1, 2, 3]
  [3, 4, 5]
  [0, 1]
  [0, 1, 2, 3, 4, 5]
  ```

  * 리스트 인덱싱

  ```python
  a = ['I', 'like', ['what','I','can','do']]
  grade = ['A',['B','C',['D']],'F']
  
  print(a[0])
  print(a[2][2])
  print(a[2][3])
  
  print(grade[1])
  print(grade[1][2])
  print(grade[1][2][0])
  print('Don\'t get',grade[2])
  ```

  ```
  I
  can
  do
  
  ['B','C',['D']]
  ['D']
  D
  Don't get F
  ```

  


### 2. 반복문

* while

  * 어떤 조건이 만족 되는 동안 반복
  * 주로 반복 횟수를 모를 때 사용

  ```python
  while <condition>: # condition이 True인 동안
  	<statement1>   # statement 반복 수행
      <statement2>
      <statement3>
      ...
  else:			   # condition이 False가 되면
      <statement4>   # else절 수행 후 종료 (생략 가능)
      <statement5>   
  ```

  * 간단한 예시

  ```python
  n = 3
  
  while n > 0:
  	print('n is', n)
  	n -= 1
  ```

  ```
  n is 3
  n is 2
  n is 1
  ```



* 이런 것도 가능하다 !

```python
while True:
    bully = input()
    
    if bully == "STOP!!!":
        break
    
    print(bully)

# input으로 "STOP!!!"이 들어올 때까지
# input으로 들어온 값을 출력함

# 단, 반드시 break 로 해제해 주어야 함
```



* for

  * 시퀀스의 모든 원소에 대해서 반복을 수행

  * 주로 얼마나 반복을 해야 되는 지 알 경우에 사용

  ```python
  for variable in sequence: # sequence 안의 원소를 순서대로 variable 대입 후
  	<statement1>		  # statement 수행
  	<statement2>
  	....
  else:					  # 모든 원소에 대한 연산 수행 후 else 절 수행 (생략 가능)
  	<statement3>
  	<statement4>
  ```

  

* range(), len()

  * range() : 특정 횟수나 특정 범위에 대한 반복 연산 수행하기 위해 사용
  * range(len()) : 리스트의 인덱스를 이용한 반복을 하기 위해서 자주 사용



* 리스트 입력받는 여러가지 방법

```python
a = input() # [1, 2, 3, 4, 5]
print(a)
print(type(a))
```

```
[1, 2, 3, 4, 5]
<class 'str'> 
```

input 으로 값을 입력 받으면 자료형이 str이 된다.  ( a = '[1, 2, 3, 4, 5]' )

아래의 방법들을 참고해보자.

```python
# str to list
a = list(input()) # '12345'
print('a:', a,', a의 타입:',type(a))

# split
c = list(map(int,input().split())) # '1 3 5 9 10'
print('c:', c,', c의 타입:',type(c))

# for문
d = [int(input()) for i in range(5)]
```

```
a: ['1', '2', '3', '4', '5'], a의 타입: <class 'list'>
c: [1, 3, 5, 9, 10], c의 타입: <class 'list'>
```



### 3. 함수

```python
# 함수의 정의
def function_name(parameters):
	<statement1>
	<statement2>
	...
	return return_value

# 함수의 사용 (실행)
function_name(argements)
```

* return

  * 함수 내부에서 명령문 중 리턴문을 수행하면, 반환값을 돌려주고 함수의 실행 종료

  * 반환값 없을 시 ```None```

    ```python
    def fake_elice():
    	a = 'elice'
    
    print(fake_elice())
    
    def real_elice():
        return 'elice'
    
    print(real_elice())
    
    def print_elice():
        print('elice')
        
    print(print_elice())
    ```

    ```
    None
    elice
    elice
    None
    ```

  * 이런 것도 가능하다.

    ```python
    # a, b, c를 내림차순으로 정렬한 리스트를 반환하는 함수
    
    def sorting(a, b, c):
        if a > b:
            if a > c:
                if b > c:
                    return [a, b, c]
                return [a, c, b]
            return [c, a, b]
        else:
            if a < c:
                if b > c:
                    return [b, c, a]
                return [c, b, a]
            return [b, a, c]
     
    # return을 만나면 함수가 바로 종료되므로
    # else를 쓰지 않아도 잘 작동은 된다.
    ```



* 파이썬 내장 함수 ```input```과 ```print```

  * ```input``` : 기본적으로 ```str``` 자료형으로 입력을 받는다.

    ```python
    a = input() # 3
    b = input() # 5
    
    print(a + b)
    ```

    ```
    35 
    ```

  * ```print``` : print는 반환값이 없으므로 겹쳐 사용 시 유의해야 한다.

    ```python
    # ???????
    print(None, print(print())) 
    ```

    괜찮다. 차근 차근 짚어보자.

    ```python
    print()
    print(None)
    print(print())
    ```

    ```
    
    None
    
    None
    ```

    생각보다 (???) 복잡하지 않다.

    ```python
    print(None, print(print()))
    ```

    ```
    
    None
    None None
    ```

    

* 네임 스페이스와 전역/지역 변수

  * 네임스페이스 : 변수, 함수 등이 정의 되어있는 공간

  * 전역  네임 스페이스: 프로그램이 실행될 때 생성

  * 지역  네임 스페이스 : 함수가 호출될 때 생성되고, 함수의  실행이 끝나면 소멸

    ```python
    a = 3
    b = 5
    
    def ato10():
    	a = 10
        
    def bto3():
        b = 3
        
    print(a)
    print(b)
    ```

    ```
    3
    5
    ```

    

    ```python
    # 결과를 예측해보자 1
    def make_a():
        a = 3
    
    make_a()
    print(a)
    ```

    ```python
    # 결과를 예측해보자 2
    a = 3
    
    def ato10():
    	a = 10
        
    print(ato10())
    ```

    

##### 실습

1. max 함수 구현해보기

   * python의 내장 함수 max는 리스트의 최대값을 반환해준다.

   * 이러한 기능을 하는 함수를 직접 구현해보자.

     ```python
     def myMax(a):
     	pass
     	
     a = [1, 4, 0, -3, 10]
     print(myMax(a))
     ```

     ```
     10
     ```

     

2. count 함수 구현해보기

   * python의 내장 함수 count는 리스트(혹은 문자열) 내에 특정 원소가 등장한 횟수를 반환해준다.

   * 이러한 기능을 하는 함수를 직접 구현해보자.

     ```python
     def myCount(a, elem):
     	pass
     	
     a = [1, 2, 2, 3, 4, 4, 4, 5]
     print(myCount(a, 1))
     print(myCount(a, 4))
     ```

     ```
     1
     3
     ```

     

3. 리스트의 원소를 3개씩 출력하는 함수

   - 주어진 리스트의 원소들에 대해 인덱스순으로 세 개의 원소씩 슬라이싱해 한 줄씩 출력한다. 

     길이가 3의 배수가 아닌 경우, 마지막 줄에는 3개 미만의 원소를 갖는 리스트를 출력할 수도 있다.

     ```python
     def ele3_print(a):
     	pass
     
     a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
     b = ['a', 'b', 'c', 'd']
     
     print('ele3_print(a)')
     ele3_print(a)
     
     print('ele3_print(b)')
     ele3_print(b)
     ```

     ```
     ele3_print(a)
     [1, 2, 3]
     [4, 5, 6]
     [7, 8, 9]
     [10]
     ele3_print(b)
     ['a', 'b', 'c']
     ['d']
     ```





     

### 4. 마치며

공부할 때 참고하기 좋은 사이트 소개

- 파이썬 튜터 <http://www.pythontutor.com/>

- 스택 오버플로우 <https://stackoverflow.com/>

  

문제 푸는 연습을 해 볼 수 있는 사이트

- 알고스팟 <https://algospot.com/>
- 백준 온라인저지 https://www.acmicpc.net/ 등등
