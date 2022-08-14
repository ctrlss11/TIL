# Algorithm
## 0812 string
### 목표
* 알고리즘 문제 풀이 방법 익히기
* string 관련 문제 풀이
* 문자열 탐색 알고리즘 개념 공부 및 구현


### ASCII
* 문자를 나타내기 위한 문자 인코딩 표준
* 7bit : 256 = 128(문자) + 33(제어문자) + 95(출력가능한 문자)
* 알파벳 범위 정도는 알아두자!!
  * **A ~ Z : 65 ~ 90**
  * **a ~ z : 97 ~ 122**

* 확장 아스키 : 특수 문자 등을 표현하기 위한 코드
* 조합형, 완성형 : 한글 코드체계

### 유니코드
* 다국어 처리를 위한 표준
* character set으로 분류
  * UCS-2
  * UCS-4
* 바이트 순서에 대한 이슈
  * little-endian
    * 낮은 주소의 데이터에 낮은 바이트저장(LSB)
  * big-endian
    * 낮은 주소의 데이터에 높은 바이트 저장(MSB)

### UTF 유니코드 인코딩
* Unicode Transformation Format
* UTF-8
  * 웹에서 사용하는 표준
  * python
* UTF-16
  * window, java
* UTF-32
  * unix

### python의 문자열
* [string 정리 내용]()
* char 자료형이 없다
* sequential container 
  * index 
  * slicing
  * method
* immutable

#### 문자열 뒤집기
```python
# 1
lst = lst[::-1]

# 2
lst.reverse()
s = ''.join(lst)

# 3
for i in range(len(lst)//2):
    lst[i], lst[len(lst)-1-i] = lst[len(lst)-1-i], lst[i]
s = ''.join(lst)

# 4
rev = ''
for i in range(len(lst)-1, -1, -1):
    rev += lst[i]
```

#### 문자열 비교
* ==
  * \_\_eq\_\_() 메서드 호출
* is
  * 메모리 참조를 비교

#### 문자 변환
* ord : 문자를 ascii 숫자로
* char : ascii숫자에 해당하는 문자로

#### str $\rightarrow$ int 변환
```python
def itoa(num):
    flag = True # 양수는 True, 음수는 False
    if num < 0:
        flag = False
        num = -num

    result = ''
    while num:
        num, num_char = num//10, num%10
        result = chr(ord('0') + num_char) + result
    
    if flag:
        return result
    else:
        return '-' + result
```

### 패턴 매칭 알고리즘
* brute force
* Karp-Rabin
* KMP
* Boyer-Moore

#### [visualization](http://whocouldthat.be/visualizing-string-matching/)

### brute force
* 완전 탐색
* 모든 문자열이 같은지 일일이 확인
```python
# 문자열 탐색
# target t 에서 pattern p 찾기
def bf(p, t):
    M = len(p)
    M = len(t)

    for i in range(N - M + 1):
        for j in range(M):
            if p[j] != t[i]:
                break
        else:
            return i
    else:
        return -1
```
* O(NM) 최악

### KMP Knuth-Morris-Pratt
* 검색하려는 내용이 반복되는 부분이 있다면, 중간부분 탐색을 skip
* 검색하려는 내용 중, 처음부터 반복되는 패턴이 있는지 table 작성 (전처리)
  * ex) abcdabce : -1 0 0 0 0 1 2 3
  * ex) abcdebcd : -1 0 0 0 0 0 0 0
* 탐색 중 실패한 지점에서의 table 값을 확인하고, 그 값의 패턴 index부터 다시 비교
```python
def preProcess(p):
    # LPS : 전처리를 위한 테이블 
    lps = [0]*len(p)
    
    j = 0 # 반복의 시작점
    for i in range(1, len(p)):
        if p[i] == p[j]:
            lps[i] = j + 1
            j += 1
        else:
            j = 0
            # abaab 방지
            if p[i] == p[j]:
                lps[i] = j + 1
                j += 1
    return lps

def KMP(p, t):
    lps = preProcess(p)

    i = 0 # t_idx
    j = 0 # p_idx
    while i < len(t):
        if p[j] == t[i]:
            i += 1
            j += 1
        else:
            if j != 0:
                j = lps[j-1]
            else:
                i +=  1
        
        if j == len(p): return i - j
    return -1

t = 'ABC ABCDAB ABCDABCDABDE'
p = 'ABCDABDE'
print(KMP(p, t))
```

### Boyer-Moore
1. 오른쪽 $\rightarrow$ 왼쪽으로 비교
2. 문자열 뒤집은 skip table 작성
3. 불일치하면, 
  * 타겟이 패턴안에 있는지 확인
    * 있다면 해당 idx와 위치를 맞추고, 다시 1부터
    * 없다면 패턴의 길이만큼 skip, 다시 1부터

* 보편적으로 사용하는 알고리즘
* 시간복잡도 
* 최선
* 평균
* 최악
```python
# boyer-moore
def preProcess(p):
    M = len(p)

    skip_table = dict()
    # 문자를 key, 문자의 뒤에서부터의 idx를 value 로 저장
    for i in range(M):
        skip_table[p[i]] = M - i - 1

    return skip_table

def bm(p, t):
    skip_table = preProcess(p)
    M = len(p)

    i = 0 # t_idx
    while i <= len(t) - M:
        j = M-1         # p_idx 뒤에서부터 비교
        k = i + (M-1)   # t_idx 비교를 시작할 위치

        # p와 t를 비교
        # 같은 문자가 있거나, 비교가 끝나면 탈출
        while j >= 0 and p[j] == t[k]:
            j -= 1
            k -= 1

        # idx가 -1 이면, 비교가 끝난 상황이므로 idx 반환
        if j == -1:
            return i
        
        # 같은 문자가 있다면, 그 문자의 idx로 이동, 없다면 M(문자열 길이) 만큼 skip
        else:
            i += skip_table.get(t[i+M-1], M)
    
    return -1

print(bm('rithm', 'hello algo algorithm'))
```

## 추가
* boyer-moore 시간 복잡도 기호 (특수문자) 표시방법 찾아보기