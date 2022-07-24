# Python
## 0724 예외처리
### 목표
* 예외처리를 통해 코드에서의 에러를 처리하기
* 사용자 정의 에러를 만들어 사용해보기
  

### 에러를 일부러 발생?
* 입력 인자의 갯수 에러, 입력 값의 에러, 문법 에러 등등 많은 종류의 에러가 있을 수 있다.
* 내가 프로그램을 만들면서 실행되면 안되는 상황들에 대해서 일부러 에러를 발생시켜야 한다.
* 기타 상황에서 에러 핸들링을 어떻게 할 것인가?


### try , except
```python
try :
    # 정상적으로 실행될 때의 코드
except 에러 종류:
    # 에러가 발생했을 때 실행되는 코드
```
* try 아래의 코드가 잘 실행되다가, 만약 에러가 발생했을 때
* 발생한 에러의 종류가 except에서 선언한 에러라면 excetp아래의 코드를 실행

```python
try:
    print("나누기 전용 계산기입니다.")
    nums = []
    nums.append(int(input("첫 번쨰 숫자를 입력하세요 : ")))
    nums.append(int(input("두 번쨰 숫자를 입력하세요 : ")))
    # nums.append(int(nums[0] / nums[1]))
    print(f'{nums[0]} / {nums[1]} = {nums[2]}')

except ValueError:
    print("에러! 잘못된 값을 입력하였습니다.")
# 예를들어 int 대신에 str이 들어갔을 때처럼 입력이 잘못되었을 때의 에러

except ZeroDivisionError as err:
    print(err)
# 0으로 나눗셈을 하였을 때 발생하는 에러
# as err로 하면 err로 변수받는 느낌
# err로 ZeroDivisionError(에러의 종류)를 출력 가능

# except:
except Exception as err:
    print("알 수 없는 에러가 발생하였습니다.")
    print(err)
# 위에서 명시한 에러 이외의 모든 에러를 처리
# else 느낌
```
* except 뒤에는 에러의 종류를 적어서 종류별로 다르게 관리 가능
* as 변수 : 를 사용하여 에러의 종류를 출력할 수도 있다.

* 명시된 에러 이외의 모든 것들을 포함할 때는 except: 혹은 except Excetpion:
* Exceptoin은 나머지 에러 모두를 뜻 (else 느낌)
* 이 때에도 에러 메세지를 출력하고 싶다면 as 를 활용


### raise
```python
# 프로그램상 필요한 에러를 강제로 발생시키기
# raise 에러종류 
try:
    print("한 자리 숫자 나누기 전용 계산기입니다.")
    num1 = int(input("첫 번쨰 숫자를 입력하세요 : "))
    num2 = int(input("두 번쨰 숫자를 입력하세요 : "))

    if num1 >= 10 or num2 >= 10:
    # 강제로 에러를 발생시키기
        raise ValueError
    print("{0} / {1} = {2}".format(num1, num2, int(num1 / num2)))

# 에러가 발생했을 때, 아래 코드 실행
except ValueError:
    print("잘못된 값을 입력하였습니다. 한 자리 숫자만 입력하세요.")
```
* raise를 통해 에러를 발생 시킬 수 있음


### 사용자 정의 예외처리 , finally
```python
# python에 내장된 에러 말고, 사용자 정의 에러를 만들어보자
# 만들려는 에러 class 생성
class BigNumberError(Exception):
    def __init__(self, msg):
        self.msg = msg

    def __str__(self):
        return self.msg

try:
    print("한 자리 숫자 나누기 전용 계산기입니다.")
    num1 = int(input("첫 번쨰 숫자를 입력하세요 : "))
    num2 = int(input("두 번쨰 숫자를 입력하세요 : "))

    if num1 >= 10 or num2 >= 10:
    # 강제로 사용자 정의 에러 발생!!
    # BigNumberError에 입력값 전달
        raise BigNumberError("입력값 : {0}, {1}".format(num1, num2))
    print("{0} / {1} = {2}".format(num1, num2, int(num1 / num2)))

except ValueError:
    print("잘못된 값을 입력하였습니다. 한 자리 숫자만 입력하세요.")
except BigNumberError as err:
    print("에러가 발생하였습니다. 한 자리 숫자만 입력하세요.")
    # class 에서 return sel.msg로 반환했기 때문에 print 해줘야 한다!
    print(err)

# try/except 구문 실행 후 finally아래 구문 실행
finally:
    print('계산기를 이용해 주셔서 감사합니다.')
```
* 사용자 정의 에러 class를 생성, Exception 상속받기
* raise로 사용자 정의 애러 발생
* except로 에러발생시 실행되어야하는 내용 작성

* finally를 사용하면 try/except 구문 후에 실행되는 코드 작성 가능
* try로 제대로 실행되든, except로 에러가 발생되든 관계없이
* 모든 코드가 실행된 뒤에 무조건 finally 아래 구문이 실행 가능



---
### 참조
* [python 기초 영상](https://www.youtube.com/watch?v=kWiCuklohdY)
