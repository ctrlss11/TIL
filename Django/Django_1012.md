# 221012

## M:N
* many to many relationships
* 양쪽 모두에서 N:1 관계
* 한 테이블의 0개 이상의 레코드가 다른 테이블의 0개 이상의 레코드와 연관
* Article - User
* User - User

### DB modeling
* target model : 관계 필드를 가지지 않은 모델
* source model : 관계 필드를 가진 모델
* ex) N:1 에서 N이 source, 1이 target

### 중개 모델
* ManyToManyField 사용하여 중개 모델 생성
```python
class Doctor(models.Model):
    name = models.TextField()

class Patient(models.Model):
    doctors = models.ManyToManyField(Doctor)
    name = models.TextField()
```
* patient_doctors 중개 테이블이 자동으로 생성!!
  * ![](./img/2022-10-12-10-00-44.png)
  * Patient -> Doctor 참조
  * Doctor -> Patient 역참조
* ManyToManyField 작성을 patient에 쓰든, doctor에 쓰든 동작에는 차이x
* 명령어로 사용할 때, 참조 역참조 사용 차이만 있고 서로 종속x
* 상황에 맞게 논리적으로 더 편한 참조 관계에 ManyToManyField 작성
* 참조 역참조 방향 주의
* 역참조시 manager name 설정 방법
  ```python
  doctors = models.ManyToManyField(Doctor, related_name='patients')
  ```
  * related_name='patients'
  * 역참조시 patient_set 대신에 설정한 patients로 사용
* add : 관계 추가
* remove : 관계 제거

### through arg
* 중개테이블에 추가 데이터를 사용해 M:N 관계를 지정하려는 경우
* through arg를 사용하여 중개 모델을 직접 작성
```python
class Patient(models.Model):
    doctors = models.ManyToManyField(Doctor, related_name='patients', through='Reservation')
    name = models.TextField()
```
```python
class Reservation(models.Model):
    doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
    patient = models.ForeignKey(Patient, on_delete=models.CASCADE)
    symptom = models.TextField()
    reserved_at = models.DateTimeField(auto_now_add=True)
```
* 관계 추가
```python
patient1.doctors.add(doctor1, through_defaults={'symptom': 'headache'})
```
  * through_defaults 에는 dictionary로 작성

## ManyToManyField
* M:N 관계 설정에 사용하는 모델 필드
* 다대다 관계를 나타내는 중개 테이블 생성

### method
* add
  * 관계 추가
  * 지정된 객체를 관련 객체 집합에 추가
  * 이미 존재하는 관계는 추가x
* remove
  * 관계 제거
  * 관련 객체 집합에서 지정된 모델 객체 제거
  * 내부적으로 QuerySet.delete() 사용
* create 
* clear

### argument
* related_name : 역참조시 manager name 설정
* through : 중개 테이블에 추가 데이터를 사용기위해 중개 테이블 직접 작성
```python
    doctors = models.ManyToManyField(Doctor, related_name='patients', through='Reservation')
```
* symmetrical : 동일한 모델을 참조할 때 (재귀 참조)
```python
    friends = models.ManytoManyField('self')
```
  * True일 때 : 반대쪽 관계도 자동으로 추가
    * 1 -> 2 , 2 -> 1
  * False
    * 1 -> 2
    * follow 기능 구현!

## Like 기능