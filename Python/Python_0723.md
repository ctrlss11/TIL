# Python
## 0723 class
### 목표
* 게임으로 비유하여 class 쉽게 이해하기
* python에서의 class 사용 방법 익히기
* 객체지향 프로그래밍


### 왜 class를  사용하는가?
* 여러가지 변수들을 생성하여 관리하여야 할 때, 코드가 복잡해 질수록 관리가 어렵다
* 이 때 class를 사용하여 객체지향 프로그래밍을 하면 개발과 유지보수가 편리!
* 대규모 프로그램을 개발할 때 자주 사용
* class는 붕어빵틀, 객체는 붕어빵
* 비슷한 기능을하는 변수 함수를 모아서 객체를 만들었다!

* 객체지향 프로그래밍
  * 데이터와 데이터에 관련된 함수를 묶어서 객체를 만들고, 객체를 사용해 프로그래밍 하는 방식

* 절차지향 로그래밍
  * 데이터와 데이터를 처리하는 함수가 분리되어 있고, 함수를 순차적으로 호출하여 조작 하는 방식


### \_\_init\_\_
```python
class Unit:
    def __init__(self, name, hp, damage):           
        self.name = name
        self.hp = hp
        self.damage = damage
        print(f'{name} 유닛이 생성 되었습니다.')
        print(f'체력 {hp}, 공격력 {1}')

# 마린, 탱크 유닛을 Unit class를 사용하여 만들어보자
m1 = Unit('마린', 40, 5)
m2 = Unit('마린', 40, 5)
t1 = Unit('탱크', 150, 35)
t2 = Unit('탱크', 150, 35)
```
* \_\_init\_\_ 은 생성자라고 한다
* 객체가 만들어질 때 자동으로 호출되는 부분
* 객체가 생성될 때는 init함수에 맞게 입력해야함 (self는 제외!)
* self.변수 = 변수 로 멤버 변수를 생성
    
* class로 만들어내는 것을 instance라고 한다
* class는 빵틀, instance는 붕어빵
* m1, t1은 Unit class의 instance


### 멤버 변수
```python
class Unit:
    def __init__(self, name, hp, damage):           
        self.name = name
        self.hp = hp
        self.damage = damage
        print(f'{name} 유닛이 생성 되었습니다.')
        print(f'체력 {hp}, 공격력 {1}')

# 외부에서 멤버 변수를 사용해보자
w1 = Unit('레이스', 80, 5)
print(f'유닛 이름: {w1.name}, 공격력 {w1.damage}')

# 외부에서 멤버 변수를 새롭게 추가해보자
# 확장한 객체에 대해서만 추가된 멤버 변수 사용가능
# w1. clocking은 불가능
w2 = Unit('레이스', 80, 5)
w2.clocking = True
# w1.clocking = True

if w2.clocking == True:
    print(f'{w2.name} 는 현재 클로킹 상태입니다.')
```
* class에서 전달 받아 생성되는 변수들을 멤버 변수라고 한다
* 앞에 self.을 붙여서 멤버 변수에 접근 가능
  * w1.name, w1.hp, w1.damage
* class 외부에서 새로운 멤버 변수 추가가능!!
  * w2.clocking = True
* 단 확장된 객체에 한해서만 사용 가능


### 메소드
```python
# 공격 기능을 가진 유닛 class를 만들어보자
class AttackUnit:
    def __init__(self, name, hp, damage):           
        self.name = name
        self.hp = hp
        self.damage = damage

    # 공격 메소드를 만들어보자
    # 멤버 변수는 self.name, 없으면 파라미터 location
    def attack(self, location):
        print(f'{self.name} : {location} 방향으로 적군을 공격 합니다. [공격력 {self.damage}')

    # 공격 받는 메소드를 만들어보자
    def damaged(self, damage):
        print(f'{self.name} : {damage} 데미지를 입었습니다.')
        self.hp -= damage
        print(f'{self.name} : 현재 체력은 {self.hp} 입니다.')
        if self.hp <= 0:
            print(f'{self.name} : 파괴되었습니다.')

f1 = AttackUnit('파이어뱃', 50, 16)
f1.attack('5시')

f1.damaged(25)
f1.damaged(25)
```
* class에 정의된 함수(class의 기능)들을 메소드라고 한다
* 멤버 변수를 사용할 때는 self.변수 로 사용 : self.name
* self. 없을시 함수로 전달받는 parameter를 사용 : location

* 메소드의 첫 번째 인자로 self를 적는다
  * self를 적지 않으면?
  * 정의 하는데는 문제가 없지만
  * 호출할 때는 전달받는 인자의 갯수 에러가 발생
* 메소드의 첫 번째 인자로 인스턴스가 항상 자동으로 전달되기 때문에 발생하는 문제!
  ```python
  class Unit:
      def unit1(self):
          print('unit1')

      def unit2():
          print('unit2')
  
  u = Unit()
  
  u.unit1()
  u.unit2()         # 에러 발생!
  ```


### 상속
```python
# 일반 유닛
class Unit:
    def __init__(self, name, hp):           
        self.name = name
        self.hp = hp

# 공격 유닛
class AttackUnit:
    def __init__(self, name, hp, damage):           
        self.name = name
        self.hp = hp
        self.damage = damage
```
* 두 class간 겹치는 부분이 많다
* Unit으로부터 **상속**을 받아서 AttackUnit class를 만들어보자

```python
# 부모 클래스
class Unit:
    def __init__(self, name, hp):           
        self.name = name
        self.hp = hp

# 상속 받아 AttackUnit 클래스 생성
# 자식 클래스
class AttackUnit(Unit):
    def __init__(self, name, hp, damage):
        Unit.__init__(self, name, hp)           # Unit 클래스의 생성자를 호출하여 멤버 변수 생성  
        self.damage = damage
```
* 상속 받으려는 클래스를 ()안에 작성
* Unit 클래스의 메소드 사용 가능!
* Unit의 생성자를 호출하여 AttackUnit의 생성자를 만들 수 있다.


### 다중 상속
```python
# 부모 클래스
class AttackUnit(Unit):
    def __init__(self, name, hp, damage):
        Unit.__init__(self, name, hp)           
        self.damage = damage

# 부모 클래스
class Flyable:
    def __init__(self, flying_speed):
        self.flying_speed = flying_speed

    def fly(self, name, location):
        print(f'{name} : {location} 방향으로 날아갑니다. [속도 {self.flying_speed}]')

# 부모 클래스 2개를 상속 받아 보자
class FlyableAttackUnit(AttackUnit, Flyable):
    def __init__(self, name, hp, damage, flying_speed):
        # super함수로도 부모 클래스의 인자 호출 가능
        # (1)
        super().__init__(name, hp, damage)              
        Flyable.__init__(self, flying_speed)

val1 = FlyableAttackUnit('레이스', 120, 20, 5)
val1.fly(v1.name, '3시')
```
* 부모 클래스를 두 개 이상 상속받아보자
* 자식 클래스의 인스턴스로 부모 클래스의 메소드 사용 가능!

(1) super()
* 상속을 받을 때 super함수를 사용해 \_\_init\_\_ 호출 가능
* super().\_\_init\_\_() 이고 self는 뺴야함!!
* 다만 다중상속일 경우 첫 번째로 상속받는 부모 클래스만 호출하니 주의할것
* 여러 부모 클래스를 초기화 해야하는 경우 직접 작성하기
```python
class Unit1():
    def __init__(self):
        print('Unit1')

class Unit2():
    def __init__(self):
        print('Unit2')

class childUnit(Unit1, Unit2):
    def __init__(self):
        # super().__init__()        # 첫 번째로 상속받는 부모 클래스 Unit1에 대해서만 호출
        # 그래서 다중 상속을 받을 때, 여러변 생성자를 사용해야한다면 직접 호출하는 것을 추천 
        Unit1.__init__(self)
        Unit2.__init__(self)
```


### 오버라이딩
```python
class Unit:
    def __init__(self, name, hp, speed):           
        self.name = name
        self.hp = hp
        self.speed = speed

    def move(self, location):
        print('[지상 유닛 이동]')
        print(f'{self.name} : {location} 방향으로 이동합니다. [속도 {self.speed}]')

class AttackUnit(Unit):
    def __init__(self, name, hp, speed, damage):
        Unit.__init__(self, name, hp, speed)           
        self.damage = damage

class Flyable:
    def __init__(self, flying_speed):
        self.flying_speed = flying_speed

    def fly(self, name, location):
        print(f'{name} : {location} 방향으로 날아갑니다. [속도 {self.flying_speed}]')

class FlyableAttackUnit(AttackUnit, Flyable):
    def __init__(self, name, hp, damage, flying_speed):
        super().__init__(name, hp, 0, damage)      
        Flyable.__init__(self, flying_speed)

    # method overriding
    # (2)
    def move(self, location):
        print('[공중 유닛 이동]')
        self.fly(self.name, location)

vul1 = AttackUnit('벌처', 80, 10 , 20)
bat1 = FlyableAttackUnit('배틀쿠르저', 500, 25, 3)

# (1)
vul1.move('11시')
bat1.fly(bat1.name, '9시')

# (2)
bat1.move('9시')
```
(1)
* Unit의 move메소드를 사용하면 location만 입력하면 된다
* Flable의 fly메소드를 사용하면 name과 location 두 개를 입력해야 한다
* 이러면 같은 기능임에도 매번 다르게 호출을 해야하므로 귀찮고 복잡하다.

(2)
* **자식 클래스**에서 메소드 오버라이딩을 통해 fly메소드 에서도 move를 사용할 수 있게 해보자
* FlableAttackUnit에서 move()를 재정의
* 그러면 bat1.move로 동일하게 사용 가능!


#### isinstance()
* isinstance(변수, 클래스)
  * 클래스의 인스턴스(변수)가 맞나 확인

---
### 참조
* [python 기초 영상](https://www.youtube.com/watch?v=kWiCuklohdY)
* [python class 설명](https://wikidocs.net/774)