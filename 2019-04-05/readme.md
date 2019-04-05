# Tutoring #03

Lecturer : Auejin Ham (201711200, [Github](https://github.com/auejin))



## Sequence 

mutable(list) and immutable(tuple, str) sequences

indexing과 slicing을 지원한다.

indexing을 지원하므로 `len(list)`를 지원한다.

value별 비교우위 가능하면 `min(list)`, `max(list)`도 지원한다.



### list

```python
list.insert(i,x)

list.append(x)
list.insert(len(a),x)

list.remove(x)
i = list.index(x)
list = list[:i]+list[i+1]

list.clear()
list = []

list.sort(key=None, reverse=False)
# key=비교우위를 정하는 함수
# reverse=True세 크기 큰 순서대로 정렬
list = sorted(list, key=None, reverse=False)

list.reverse()
list = reversed(list)
list = list[::-1]
```



**중요 : Assigning by Reference or Value**

```python
l1 = [10,20,30,40]
l2 = l1
# list의 assignment는 list의 reference를 보냄
# class의 복사와 유사

l3 = l1.copy()
l4 = l1[:]
l5 = list(l1)
# copy는 각 element의 value를 assign하므로 독립적

l1[0]=1
print(l1,l2,l3,l4,l5,sep='\n')
# [1, 20, 30, 40]
# [1, 20, 30, 40]
# [10, 20, 30, 40]
# [10, 20, 30, 40]
# [10, 20, 30, 40]

for l in l1 :
    l = 0
print(l1) # [1, 20, 30, 40]

for i in range(len(l1)) :
    l1[i] = 0
print(l1) # [0, 0, 0, 0]

# arguments are also passed by assignment
def f(var):
    # var = var[:]
    # can be modified in-place
    var[1] = 100
    var.append(100)
    # assignment does not work
    var = [1,2,3,4]

f(l1)
print(l1) # [0, 100, 0, 0, 100]
```



### tuple

sequence이므로 indexing과 slicing, len, min, max을 지원하지만

*immutable* sequence이므로 원소의 추가, 값 변경, 삭제 불가능.

```python
a = 10
a = (10,) # single element tuple
a = (10,20,30)
a = 10,20,30 # () can be omitted

a.append(40) # error
a[0] = 1 # error
```



#### Sequence Packing / Unpacking

sequence인 list, str, tuple 모두 지원하지만

assigning으로 이루어지므로 굳이 mutable할 필요가 없어서 tuple에서 자주 씀

```python
t = 10,20,30
a,b,c = t
print(a,b,c) # 10 20 30

l = 40,50,60
a,b,c = l
print(a,b,c) # 40 50 60

s = 'qwe'
a,b,c = s
print(a,b,c) # q w e
```



#### Swap by Assigning Tuple

tuple끼리 assign하면 tuple packing과 unpacking이 동시에 일어남

```python
a,b = 10,20
print(a,b) # 10 20

t = b,a # packing
a,b = t # unpacking

print(a,b) # 20 10

a,b = b,a

print(a,b) # 10 20
```



#### Returning Tuple

return value가 tuple이면 함수 실행 결과를 assign시 tuple unpacking 가능

```python
def double_triple(a):
    return 2*a, 3*a
q,w = double_triple(q,w)
```



### Nested Sequences

```python
students = [
    ('Alice', ['Programming', 'Classic Mechanics']),
    ('Bob', ['Programming', 'Linear Algebra']),
    ('Carol', ['Analytical Mechanics', 'Linear Algebra', 'Programming'])]
for student_name, courses in students:
    print('Name :', student_name)
    print('Courses :', courses)
```

list와 tuple이 번갈아 사용될경우 mutability를 검사하는 것이 매우 중요해질 수 있다.



## Techniques for loop statements

#### for vs. while

for : 정해진 sequence나 횟수 동안 loop 해야 하는 경우

while : 특정 조건을 만족할 때 까지 무기한 loop 해야 하는 경우



counter variable를 써야 하는 경우 while은 loop 밖에서 정의를 해야 하기 때문에 편의성 때문에 for를 더 선호함.

### enumerate

useful to use index and value at the same time

```python
l = [10,20,30,40,50]
for index, value in enumerate(l):
    print(index,value)
    l[index] *= 10
print(l)
```



#### Nested loops

useful for indexing multi-dimensional data

```python
l = [[1,2,3,4],[10,20,30,40],[100,200,300,400]]

for row in l:
    for v in row:
        print(v)

for row in l:
    for i in range(len(row)):
        row[i] *= -1
print(l)

for j in range(len(l)):
    for i in range(len(l[j])):
        row[j][i] *= -1
print(l)
```



#### break, continue, pass

```python
def foo() :
    pass # placeholder : useful while testing

for c in 'qwertyuiop' :
    if c in 'qr' :
        continue # 바로 다음 iteration 진행
	if c == 'y' :
        break # 가장 안쪽의 loop를 종료
    print(c, end='')
print()
```



자주 묻는거 : `if __name__ == '__main__'` 왜 쓰는거에요?

`__name__` : 다른 파일에서 import 될땐 파일 이름이 할당되고 아니면 `'__main__'`

결론 : 편집하고있는 *.py를 직접 실행할때만 작동되고 외부에서 import해서 작업 (elice에선 채점)할때는 실행이 되지 않게 하려고 쓰는거. 시험에는 안나옴.



## String Formatting

문자열을 특정 양식에 맞추어 저장하자.

input / output control에 매우 유용하게 사용될 수 있다.

native python programmer는 f-string이 가장 편하다.

### % operator

Printf-style formatting을 지원하므로 c언어에 익숙하다면 유용하다.

`format % values` 형태로 사용한다.

conversion specifier

- mapping key: () 안의 문자들로 주어지고 values를 참조

- conversion flag : '0'-남는 공간이 0으로 채워짐, '-'-왼쪽정렬
- 최소 문자 폭
- 정확도 : '.'와 숫자로 소수 부분의 자리수를 명시

```python
pi = 3.14159265358979

print('%f'% pi)      #3.141593
print('%.2f'% pi)    #3.14
print('%.10f'% pi)   #3.1415926536

print('%10.2f'% pi,end='_')    	#      3.14_
print('%010.2f'% pi,end='_')   	#0000003.14_
print('%-10.2f'% pi,end='_') 	#3.14      _

print('%g %g %g' % (10,20,30) )
print('%(name)s %(age)g' % ('Alice',20) )
```



### str.format(args)

위의 % operator를 좀 더 파이썬 스타일의 형태로 만들어 사용하기 편하게 만들었다.

indexing을 지원하므로 순서를 바꾸거나 변수 재사용이 가능하다.

`'{format}'.format(args)` 형태로 사용한다.

```python
print('{} {} {}'.format(10,20,30))
print('{2} {1} {0}'.format(10,20,30)) # 순서 바꾸기
print('{1} {1} {1}'.format(10,20,30)) # 변수 재사용

print('{:10d}'.format(42),end='_') 	#        42_
print('{:>10d}'.format(42),end='_')     #        42_
print('{:^10d}'.format(42),end='_')     #    42    _
print('{:<10d}'.format(42),end='_')     #42        _
print('{:10.10f}'.format(333.333))	#333.3330000000
print('{:2.2f}'.format(333.333))	#333.33
```



### f-String

Literal string interpolation가 정식 명칭이다.

string 안에서 파이썬 코드로 사용할 부분만 {}로 싸주면 되므로 매우 편하다.

{}안의 임의의 expression이 연산되어 자동으로 string으로 변환된다.

`f'string mixed with {format} is supported'` 형태로 사용한다.

```python
def sq(x):
    return x**2

for i in range(10):
    print(f'{i}의 제곱은 {sq(i)}이다.')
```

