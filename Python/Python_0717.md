# Python
## 220720 class
### 목표
* python으로 class개념 공부 및 연습



### 예제로 연습
>작성 코드
```python
from random import *

# 일반 유닛 class
class Unit:
    # code

# 공격 유닛 class
class AttackUnit(Unit):

# 마린 class
class Marine(AttackUnit):
    # code

# 탱크 class
class Tank(AttackUnit):
    # 시즈모드 : 탱크를 지상에 고정시켜, 더 강력한 공격을 함, 이동 불가
    # 시즈모드 개발여부 x
    # code

        # 시즈모드가 개발되지 않았을 때에는 아무동작 x, 그냥 return 
        # code

        # 현재 시즈모드가 아닐 때 => 시즈모드
        # code
        # 현재 시즈모드일 때 => 시즈모드 해제
        # code

# 공중 유닛 class
class Flyable:
    # code

# 공중 공격 유닛 class
class FlyableAttackUnit(AttackUnit, Flyable):
    # code

# 레이스
class Wraith(FlyableAttackUnit):
    # 클로킹 : 유닛 투명화
    # 클로킹 개발여부 x
    # code

        # 클로킹 해제가 디폴트라고 하자
        # code 


        # 클로킹 => 클로킹 해제
        # code
        # 클로킹 모드 해제 => 모드 설정
        # code
        
def game_start():
    print("[알림] 새로운 게임을 시작합니다.")

def game_over():
    print("Player : gg")
    print("[Player] 님이 게임에서 퇴장하셨습니다.")

# main 함수 실행!!

# 실제 게임 진행
# 게임 시작
game_start()

# 유닛 생성
m1 = Marine()
m2 = Marine()
m3 = Marine()

t1 = Tank()
t2 = Tank()

w1 = Wraith()

# 유닛 일괄 관리    (생성된 모든 유닛 list에 append해서 관리)
attack_units = []
attack_units.append(m1)
attack_units.append(m2)
attack_units.append(m3)
attack_units.append(t1)
attack_units.append(t2)
attack_units.append(w1)

# 전군 이동
for unit in attack_units:
    unit.move("1시")

# 탱크 시즈모드 개발
Tank.seize_developed = True
print("[알림] 탱크 시즈 모드 개발이 완료되었습니다.")

# 공격 모드 준비 (마린 : 스팀팩, 탱크 : 시즈모드, 레이스 : 클로킹)
for unit in attack_units:
    # 지금 만들어진 객체가 어떤 class의 instance 인지 확인
    # Marine class이면 stimpack, Tank class이면 seize mode, Wraith class 이면 clocking을 진행
    if isinstance(unit, Marine):
        unit.stimpack()
    elif isinstance(unit, Tank):
        unit.set_seize_mode()
    elif isinstance(unit, Wraith):
        unit.clocking()

# 전군 공격
for unit in attack_units:
    unit.attack("1시")

# 전군 피해
for unit in attack_units:
    unit.damaged(randint(5, 21))    # 공격은 5~20 사이에서 랜덤값으로 받음

# 게임 종료
game_over()
```

>output
```python
[알림] 새로운 게임을 시작합니다.                                # 게임 시작 알림
마린 유닛이 생성되었습니다.                                     # 마린 3기 생성
마린 유닛이 생성되었습니다.
마린 유닛이 생성되었습니다.
탱크 유닛이 생성되었습니다.                                     # 탱크 2기 생성
탱크 유닛이 생성되었습니다.
레이스 유닛이 생성되었습니다.                                   # 레이스 1기 생성
마린 : 1시 방향으로 이동합니다. [속도 1]                        # 유닛 전체 이동
마린 : 1시 방향으로 이동합니다. [속도 1]
마린 : 1시 방향으로 이동합니다. [속도 1]
탱크 : 1시 방향으로 이동합니다. [속도 1]
탱크 : 1시 방향으로 이동합니다. [속도 1]
레이스 : 1시 방향으로 날아갑니다. [속도 5]
[알림] 탱크 시즈 모드 개발이 완료되었습니다.                    # 개발 완료 알림
마린 : 스팀팩을 사용합니다. (HP 10 감소)                        # 유닛 특수 능력 사용
마린 : 스팀팩을 사용합니다. (HP 10 감소)
마린 : 스팀팩을 사용합니다. (HP 10 감소)
탱크 : 시즈모드로 전환합니다.
탱크 : 시즈모드로 전환합니다.
레이스 : 클로킹 모드 설정합니다.
마린 : 1시 방향으로 적군을 공격 합니다. [공격력 5]              # 유닛 공격 명령
마린 : 1시 방향으로 적군을 공격 합니다. [공격력 5]
마린 : 1시 방향으로 적군을 공격 합니다. [공격력 5]
탱크 : 1시 방향으로 적군을 공격 합니다. [공격력 70]
탱크 : 1시 방향으로 적군을 공격 합니다. [공격력 70]
레이스 : 1시 방향으로 적군을 공격 합니다. [공격력 20]
마린 : 8 데미지를 입었습니다.                                   # 유닛 피해
마린 : 현재 체력은 22 입니다.
마린 : 12 데미지를 입었습니다.
마린 : 현재 체력은 18 입니다.
마린 : 8 데미지를 입었습니다.
마린 : 현재 체력은 22 입니다.
탱크 : 20 데미지를 입었습니다.
탱크 : 현재 체력은 130 입니다.
탱크 : 10 데미지를 입었습니다.
탱크 : 현재 체력은 140 입니다.
레이스 : 16 데미지를 입었습니다.
레이스 : 현재 체력은 64 입니다.
Player : gg                                                     # 게임 종료 알림
[Player] 님이 게임에서 퇴장하셨습니다.
```

###
>

![class 상속 예제](./img/2022-07-17-21-51-58.png)




### 참고
* [python class 예제](https://www.youtube.com/watch?v=kWiCuklohdY)