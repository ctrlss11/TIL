# Python
## 220718 variable, datatype
### 목표
* 기초적인 python문법 정리
* python의 변수와 자료형에 대해 정리

### variable
* 변수
  * 데이터를 저장하기 위해 사용
  * <u>**추상화**</u>를 통해 복잡한 값들을 쉽게 사용

* 추상화
  * 의미단위로 작성하여 코드의 가독성 증가
  * 코드 수정 쉬움

* 변수 이름 규칙
  * 식별자는 영문 알파벳, _, 숫자로 작성
  * 첫 글자에 숫자는 불가
  * 대소문자 구별
  * keywords, reversed words, 내장 함수, 모듈 등의 이름 사용 불가
  ```python
  import keyword
  print(keyword.kwlist)

  # keyword 목록
  ['False', 'None', 'True', '__peg_parser__', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 
  'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']
  ```

* 변수의 값을 바꿔서 저장하기
    >Pythonic한 방법!
    ```python
    x, y = 10, 20
    x, y = y, x
    
    # 다른 언어의 경우 temp변수를 사용하겠지만 python은 다르다!
    ```

### 연산자
* 산술 연산자

  |연산자|의미|
  |:---:|:---:|
  |+|덧셈|
  |-|뺼셈|
  |*|곱셈|
  |/|나눗셈|
  |//|몫|
  |**|거듭제곱|

### 자료형
* numeric
  * int
  * float
  * complex
* string
* boolean
* None

* 진수표현
  * binary 2진수 : 0b
    * 0b10 : 2
  * octal 8진수 : 0o
    * 0o30 : 24
  * hexadecimal 16진수 : 0x
    * 0x10 : 16

* floating point 부동 소수점
  * 10진수 0.1은 2진수로 0.0001100110011...
  * 컴퓨터로 표현하기위해서 round하여 근사값으로 표현
  * 0.1을 컴퓨터로 표현하면 3602879701896397 / 2 * 55
  * 0.1에 근사한 값이지 정확한 값은 아니다
  * floating point rounding error 발생 가능
  * 수치해석 자료 찾아보기
  ```python
  print(3.2 - 3.1) # 0.100000
  print(1.2 - 1.1) # 0.099999
  
  # 컴퓨터에게 3.2 - 3.2 == 1.2 - 1.1 이냐고 물어보면 False
  ```

* 해결 방법
  * epsilon(매우 작은수) 혹은 math 모듈 사용하기
  ```python
  a = 3.2 - 3.1 # 0.100000
  b = 1.2 - 1.1 # 0.099999
  epsilon = 1e-10                 # 10^(-10) 을 의미
  print(abs(a - b) <= epsilon)    # True
  import math
  print(math.isclose(a, b))       # True
  ```

* string 문자열
  *  ' '나 " " 둘 다 가능
  *  소스코드 내에서 둘 중 하나로 통일해서 사용할 것
  *  string에 ' ' 혹은 " "을 사용하려면
  ```python
  print('큰따옴표 : "큰따옴표" ')
  print("작은따옴표 : '작은따옴표' ")
  print('''삼중 따옴표는 
  문자열 안에 '작은따옴표'나 
  "큰따옴표"를 사용할 수 있고 
  여러 줄을 사용할 수도 있다''')    
  # triple quotes 삼중 따옴표 , 줄바꿈되서 출력됨
  # \' \" 도 가능
  ```
* escape sequence

  |reversed words|의미|
  |:---:|:---:|
  |\n|줄 바꿈|
  |\t|탭|
  |\r|캐리지 리턴|
  |\o|Null|
  |\ \ | \ |
  |\'|'|
  |\"|"|

* string interpolation
  * %-formatting
  * str.format()
  * f-string
    * python 3.6 이후만
    * 가장 많이 사용
  ```python
  var = "변수"
  num = 15
  print(f"{var}값은 {num} 입니다.")               # f-string
  print("{}값은 {} 입니다.".format(var, num))     # str.format()
  print("%s값은 %d입니다." % (var, num))          # %-formatting
  ```

* None
  * 값이 없음을 표현하기 위한 파이썬의 자료형 중 하나
  * 반환 값이 없는 함수에서 사용

* boolean
  * True False 를 표현하는 자료형
  * 비교, 논리 연산 사용

* 비교 연산자
  * is : 객체 아이덴티티
  * is not : 객체 아이덴티티가 아닌 경우

* 논리 연산자
  * and
    * A 와 B 모두 True 이면 True
    * A 와 B 둘 중 하나라도 False 면 False
  * or
    * A 와 B 모두 False 이면 False
    * A 와 B 둘 중 하나라도 True 면 True
  * not
  * Falsy
    * False는 아니지만 False로 취급되는 다양한 값
    * 0, 0.0, (), [], {}, " " 
  * not $\rightarrow$ and $\rightarrow$ or 순서로 연산

* Falsy가 아닌 값들은 True로 반환
  ```python
  print(3 and 5)    # 5
  print(3 and 0)    # 0
  print(0 and 3)    # 0
  print(0 and 0)    # 0

  # print(3 and 5) 이면 print(True and True) : and 연산이라 끝까지 판단 => 5 출력
  # print(0 and 3) 이면 print(False and ...) : and 연산이라 무조건 False, 단축평가 => 0 출력

  print(5 or 3)     # 5
  print(3 or 0)     # 3
  print(0 or 3)     # 3
  print(0 or 0)     # 0

  # print(5 or 3) 이면 print(True and ...) : or 연산이라 무조건 True, 단축평가 => 5 출력
  # print(0 or 3) 이면 print(False and True) : or 연산이라 끝까지 판단 => 3 출력
  ```

### 컨테이너
* 컨테이너
  * 데이터를 담을 수 있는 객체
  * 서로 다른 자료형을 저장 가능
  * ordered vs unorderd 구분
  * sequence vs nonsequence

#### list
* [] 혹은 list()
* 파이썬에서는 어떤 자료형도 저장 가능
* 가변 자료형
* 유연성이 좋아서 가장 많이 사용
* index 접근 : list[index]
  ```python
  boxes = ["A", "b", ["apple", "banana", "cherry"]]
  print(len(boxes))           # 3
  print(boxes[2])             # ["apple", "banana", "cherry"]
  print(boxes[2][-1])         # cherry
  print(boxes[-1][2][0])      # c
  ```

#### tuple
* () 혹은 tuple()
* 수정 불가능한 불변 자료형
* index 접근 가능
* 튜플 생성시 값 뒤에 쉼표 붙이기
  ```python
  # 뒤에 쉼표 붙이기!
  tuple_a = (1,)
  tuple_b = (1, 2, 3,)
  
  a = 1,
  b = 1, 2, 3
  print(type(a), type(b))     # <class 'tuple'>
  ```

#### range
* range(n이상, m미만, s스텝)
```python
print(list(range(8, 1, -2)))    # [8, 6, 4, 2]
print(list(range(8, 1, 1)))     # []
```

#### slicing 연산자
* [n이상:m미만] 으로 사용
* 'abcdefghi'의 index 예시

  |a|b|c|d|e|f|g|h|i|
  |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
  |0|1|2|3|4|5|6|7|8|
  |-9|-8|-7|-6|-5|-4|-3|-2|-1|  

  ```python
  # slicing 예제
  s = 'abcdefghi'

  print(s[2:5])           # 'cde'
  print(s[2:5:2])         # 'ce'
  print(s[5:2])           # []
  print(s[5:2:-1])        # 'fed'
  print(s[:3])            # 'abc'
  print(s[5:])            # 'fghi'
  print(s[::])            # 'abcdefghi'  s[0:lens(s):1] 과 동일
  print(s[::-1])          # 'ihgfedcba'  s[-1:-(len(s) + 1):-1] 과 동일
  ```

#### set
* {} 혹은 set()
* 가변 자료형
* 순서 x, index 접근 불가
* 중복 허용 x, 중복되는 원소가 있다면 하나만 저장
* 수학에서의 집합과 동일
* 집합 연산 가능

  |set 연산|의미|
  |:---:|:---:|
  | \| |합집합|
  |&|교집합|
  |-|차집합|
  |^|대칭차집합|
  
* 빈set을 만들려면 반드시 set()을 사용, dict랑 구별!
```python
set1 = {}
set2 = set()
print(type(set1))       # <class 'dict>
print(type(set2))       # <class 'set>
```

#### dictionary
* {} 혹은 dict()
* key: value 로 구성
* 3.7 버전부터는 ordered

* key는 변경 불가능한 데이터(immutable)만 활용 가능
  * string, int, float, bool, tuple, range
* value는 상관없음
* key를 통해 value에 접근

#### 형변환
* 파이썬에서는 데이터 형태를 서로 변환할 수 있다!

* explicit 명시적 형 변환: 사용자가 의도적으로 변환
  * str(), float(), int()
  ```python
  print('3' + 4)                # TypeError
  print(int('3') + 4)           # 7
  print(int('3.5') + 5)         # ValueError  3.5는 float이므로 int변환 불가
  print('3' + str(4))           # 34    <class 'str'>

  print(float(3))               # 3.0
  print(float('3/4') + 5.3)     # ValueError  3/4를 명백한 실수 0.75로 바꿔야 변환가능
  ```

* implicit 암시적 형 변환: 파이썬 내부적으로 변환
  * bool, inf, float
  ```python
  print(True + 3)   # 4     : bool -> int
  print(3 + 5.0)    # 8.0   : int -> float
  ```

* input()으로 받으면 항상 str
* 그래서 정수가 필요한 경우 int(input())으로 받기
* map(int, input().split())
  * str으로 받고, 빈칸을 제거하고, int로 형 변환
  * map은 input으로 받은 list를 int로 형 변환

* 컨테이너 간의 형 변환 range 제외 가능, dict은 key만




---
## 추가하기
* 추상화란 정확하게 무엇인가? 개념 설명가능하게
* float('3/4')가 안되는 이유