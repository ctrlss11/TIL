# Java
## 기본 문법 정리
### 삼항 연산자
* 조건?(참이면 실행):(거짓이면 실행)
```java
int x = 3;
int y = 5;
int max = (x > y)?x:y;
```

### 문자열
```java
String s = "Hello World!"

s.length();                     // 길이
s.toUpperCase();                // 대문자로
s.toLowerCase();                // 소문자로
s.contains("H");                // 포함 여부
s.indexOf("H");                 // 문자열 위치 인덱스
s.lastIndexOf("o");             // 문자열의 마지막 위치 인덱스
s.startsWith("Hellow");         // 문자열 시작 여부
s.endsWith(".");                // 문자열 끝나는 여부
s.replace("World", "Java");     // 문자열 교체
s.substring(6);                 // 인덱스 뒷부분만 출력 -> "World!"
s.trim();                       // 앞뒤 공백 제거
s.concat("?");                  // 문자열 결합
```

```java
// 문자열 비교
// == : 참조를 비교
String s1 = "Java";
String s2 = "Java";
System.out.println(s1==s2);         // True -> s1, s2 가 같은 메모리를 참조


String s3 = new String("Java");
String s4 = new String("Java");
System.out.println(s3==s4);         // False -> s3, s4 가 다른 메모리 참조

// equals : 문자열의 값을 비교
String s5 = "Java";
String s6 = "Java";
System.out.println(s5.equals(s6));  // True -> 문자열의 값을 비교
```

```java
\n : 줄바꿈
\t : 탭
\\ : 역슬래시
\" : 큰따옴표
\' : 작은따옴표
```

### 배열
* 자료형[] 변수명 = new 자료형[크기];
  * int[] numbers = new int[5];
* 자료형[] 변수명 = new 자료형[] {값1, 값2};
  * int[] numbers = new int[] {1, 2, 3};
  * int[] numbers = {1, 2, 3};
* 자료형[][] 변수명 = new 자료형[row][col];
  * int[][] numbers = new int[2][3];
  * int[][] numbers = new int[][] { {1, 2, 3}, {4, 5, 6} };

### ASCII
* **48 : 0**
* **65 : A**
* **97 : a**

### 메소드
```java
접근제어자 반환형 메소드명 (전달값) {
    명령문

    return 반환값
}

public static void printNumber(int num) {
    System.out.println(num)
}
```

### 메소드 오버로딩
* 같은 이름의 메소드이면서, 매개변수의 갯수나 자료형을 다르게 하는등으로 여러개의 메소드 작성
```java
public static int add (int a, int b) {
    return a + b;
}

public static int add (int a, int b, int c) {
    return a + b + c;
}

public static double add (double a, double b) {
    return a + b;
}
```

### 변수의 범위
* 변수가 선언된 영역 내에서만 사용 가능
* 간단하게 보면 변수가 선언된 {} 범위안에서만 사용
```java
public static void main(String[] args) {
    int a = 10;
    if (a > 0) {
        int b = 20;
        System.out.println(b);
    }
    System.out.println(b);      // 변수 b 사용 불가
}

```

### 클래스
* 데이터와 기능을 포함하는 코드 묶음
* 클래스를 통해 객체들을 생성하여 사용
* 인스턴스 변수 : 클래스 내에 선언된 변수, 객체마다 다른 값을 가질 수 있음
* 클래스 변수 : 클래스 내에 static 으로 선언된 변수, 모든 객체가 공유하는 변수
* 인스턴스 메소드 : 클래스 내에 정의된 메소드
* 클래스 메소드 : 클래스 내에 static 으로 정의된 메소드
* this : 자기자신, 클래스내에서 인스턴스 변수와 지역 변수를 구분할 때 사용
* 생성자 : 객체가 생성될 때 호출되는 메소드
* Getter : 인스턴스 변수의 값 반환
* Setter : 인스턴스 변수의 값 설정
```java
// 선언
class Person {
    String name;                    // 인스턴스 변수
    int age;

    Person (String name, int age) { // 생성자
        this.name = name;
        this.age = age;
    }

    public int getAge() {           // Getter
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }



    static int personCnt = 0;       // 클래스 변수

    public void introduce() {       // 인스턴스 메소드
        System.out.println("이름 : " + name);
    }

    public static void printPersonCnt() {   // 클래스 메소드
        System.out.println(personCnt);
    }

    public void setName (String name) {
        this.name = name;           // this를 사용해 인스턴스 변수 name과 전달받은 변수 name을 구분 
    }
}
```
```java
// 사용
public static void main (String[] args) {
    // 클래스명 객체명 = new 클래스
    Person personA = new Person();
    personA.name = "nameA";
    personA.age = "10";

    personA.introduce();            // 객체명으로 인스턴스 메소드 접근

    Person.personCnt = 1;           // 클래스 변수는 객체가 아니라 클래스명으로 바로 접근
    Person.printPerson Cnt          // 클래스 메소드는 클래스명으로 접근

    personA.setName("nameAA");

    Person personB = new Person("nameB", 20);

    Person personC = new Person();
    personC.setAge(20);

}
```

#### 접근 제어자
* 접근 권한 지정
* pirvate : 해당 클래스 내에서만 접근
* public : 모든 클래스에서 접근
* default : 같은 패키지 내에서만 접근 (아무것도 안적었을 때)
* protected : 같은 패키지 내에서 접근, 다른 패키지인 경우라면 자식 클래스에서만 접근

### 패키지
* 관련 클래스들을 그룹화 (폴더)
* package 패키지명;
* import 패키지명.클래스명;
```java
import java.util.Random;

public class MyClass {
    public static void main (String[] args) {
        Random random = new Random();
        int num = random.nextInt();
    }
}
```

### 상속
* 특정 클래스의 기능을 재사용 및 확장
* 부모 클래스를 상속하여 자식 클래스를 작성
* 자식 클래스에서 부모 클래스의 기능을 재사용 가능
```java
class Student extends Person {
    String school;
}
```

### 메소드 오버라이딩
* 부모 클래스의 메소드 재정의 (덮어쓰기)
```java
class Person {

    public void introduce() {
        System.out.println("이름입니다.");
    }
}

class Student extends Person {
    
    public void introduce() {
        System.out.println("학생입니다.")
    }
}
```

### 다형성
* 여러 형태로 동작할 수 있는 성질
* 메소드오버라이딩 등을 통해 부모 클래스를 공유하는 객체들이 서로 다른 동작을 할 수 있음 -> 다형성
```java
public static void main (String[] args) {
    Person person = new Person();
    Person student = new Student();

    person.introduce();         // 이름입니다.
    student.introduce();        // 학생입니다. -> 부모 클래스를 참조하여 자식 클래스의 메소드 실행
}
```

### super
* 부모 클래스 접근
```java
class Person {
    int age;

    Person (int age) {
        this.age = age;
    }
}

class Student extends Person {
    String school;
    Student (int age, String school) {
        super(age);     // super을 통해 부모 클래스에서 정의된 생성자 호출
        this.school = school;
    }
}
```

### 참조
* 객체의 메모리 주소를 가리킴
```java
String s1 = "A";
String s2 = "B";

s1 = s2;    // s2의 참조를 s1에 복사, s1은 s2와 같은 메모리주소 참조
```

### final
* 변경할 수 없도록 하는 키워드
* 초기값 설정 필요
```java
class Person {
    final String name = "이름";             // 변수값 변경 불가
    public final void introduce() {         // 메소드 오버라이딩 불가
        System.out.println("이름입니다.")
    }
}
```

### enum
* 상수들의 묶음
* 열거형
```java
enum Gender {
    MALE,
    FEMALE
}

class Person {
    Gender gender;
    public void setGender(Gender gender) {
        this.gender = gender;
    }
}

public static void main (String[] args) {
    Person person = new Person();
    person.setGender(Gender.MALE);      // 열거형 사용

    switch (person.gender) {
        case MALE: System.out.println("남자"); break;
        case FEMALE: System.out.println("남자"); break;
    }
}
```

### 추상 클래스
* 아직 완성되지 않은 클래스
* 클래스 또는 메서드가 완전하지 않음을 나타내고, 서브클래스에서 이를 완성해야 한다는 의미를 전달
* 이를 통해 공통된 인터페이스를 만들고, 코드의 재사용성을 높임
* 추상 클래스 자체는 불완전한 클래스이기 때문에 인스턴스화할 수 없어서,
* 추상 클래스를 상속받은 하위 클래스만 인스턴스화가 가능
```java
abstract class Shape {
    abstract double calculateArea();
}

class Square extends Shape {
    private double s;
    
    public Square (double s) {
        this.s = s;
    }

    double calculateArea() {
        return s*s;
    }
}

class Circle extends Shape {
    private double r;
    
    public Circle (double r) {
        this.r = r;
    }

    double calculateArea() {
        return Math.PI*r*r;
    }
}
```

### 인터페이스
* 클래스를 작성할 때 기본이 되는 뼈대
```java
interface Shape {
    double calculateArea();
}

class Square implements Shape {         // implements 를 통해 interface 사용
    private double s;
    
    public Square (double s) {
        this.s = s;
    }

    double calculateArea() {
        return s*s;
    }
}

class Circle implements Shape {
    private double r;
    
    public Circle (double r) {
        this.r = r;
    }

    double calculateArea() {
        return Math.PI*r*r;
    }
}
```

### abstract vs interface
#### 다중 상속
* Interface 
  * 자바에서는 클래스가 여러 개의 인터페이스를 구현할 수 있음 
  * 이는 다중 상속을 허용하지 않는 자바에서 다중 상속과 유사한 기능을 제공
* Abstract Class 
  * 클래스는 하나의 추상 클래스만 상속받을 수 있음
  * 다중 상속이 불가능

#### 구현 여부
* Interface
  * 인터페이스는 기본적으로 메서드의 선언만 포함하며, 자바 8 이후부터는 default 메서드와 static 메서드를 통해 메서드 본체를 가질 수 있음
* Abstract Class
  * 추상 클래스는 추상 메서드뿐만 아니라 구현된 메서드도 포함할 수 있음

#### 멤버 변수
* Interface
  * 인터페이스는 기본적으로 상수(public, static, final)만 가질 수 있음
  * 일반 변수는 가질 수 없음
* Abstract Class
  * 추상 클래스는 일반 변수와 상수를 모두 가질 수 있음

#### 사용 목적
* Interface
  * 인터페이스는 클래스가 따라야 할 규칙을 정의
  * 특정 기능을 구현하도록 강제하며, 클래스가 어떤 기능을 수행할 수 있는지를 나타냄
* Abstract Class
  * 추상 클래스는 공통된 코드와 기본 동작을 제공
  * 하위 클래스가 이를 상속받아 구체적인 구현을 제공

#### 상속 관계
* Interface
  * 클래스는 여러 인터페이스를 구현할 수 있어 다양한 기능을 조합 가능
* Abstract Class
  * 클래스는 단 하나의 추상 클래스만 상속받을 수 있으며, 추상 클래스는 상속을 통해 코드 재사용과 계층적 구조를 만듬

### 제네릭스
* 다양한 형태의 데이터를 일반화하여 다룰 수 있도록 함
* 코드의 재사용성을 높이고, 타입 안정성을 확보
* T 변수명
```java
public static <T> void printValue (T value) {
    System.out.println(value);
}
```

### 제네릭 클래스
* 제네릭 기반 클래스
* 다양한 데이터 유형을 처리할 수 있도록 설계된 클래스
* class 클래스명 <T> {}
```java
class Box <T> {
    T data;
    
    public void setData (T data) {
        this.data = data;
    }
}

public static void main (String[] args) {
    Box<Integer> intBox = new Box<>();
    intBox.setData(3);

    BOx<String> stringBox = new Box<>();
    stringBox.setData("박스");
}
```

### Wrapper 클래스
* 기본 자료형을 객체로 wrapping하여 추가 기능을 제공하는 클래스
* 예시 : Integer, Double, Charcter
```java
public static void main (String[] args) {

    // int i = 1;
    // double d = 1.0;
    // char c = 'a';

    // 기본 자료형 대신 wrapper 클래스 사용
    Integer i = 1;
    Double d = 1.0;
    Charcter c = 'a';

    // 추가 기능들 사용 가능
    System.out.println(i.intValue());
    System.out.println(d.intValue());
    System.out.println(c.charValue());
}
```

### ArrayList
* 배열 기반 리스트
* 빠른 접근, 순차적으로 저장 가능
* ArrayList<T>
```java
public static void main (String[] args) {
    ArrayList<String> list = new ArrayList<>();
    list.add("aa");
    list.add("bb");

    for (String s : list) {
        System.out.println(s);
    }
}
```
```java
list.add("a");                  // 추가
list.get(0);                    // 해당 인덱스의 값 가져오기
list.size();                    // 크기
list.set(0, "b");               // 해당 인덱스의 값 수정
list.contains("b");             // 포함 여부 확인
list.remove("b");               // 삭제
list.clear();                   // 전체 삭제
```

### LinkedList
* 연결 리스트
* 데이터 요소들이 노드로 연결되어 있어서 데이터의 빠른 삽입과 삭제 가능
* LinkedList<T>
```java
public static void main (String[] args) {
    LinkedList<String> list = new LinkedList<>();
    list.add("aa");
    list.add("bb");

    for (String s : list) {
        System.out.println(s);
    }
}
```
```java
list.add("a");                  // 추가
list.get(0);                    // 해당 인덱스의 값 가져오기
list.getFirst();                // 첫번째 요소 가져오기
list.getLast();                 // 마지막 요소 가져오기
list.addFirst("first");         // 맨 앞에 추가
list.addLast("last");           // 맨 뒤에 추가
list.clear();                   // 전체 삭제
```

### HashSet
* 순서, 중복을 허용하지 않는 데이터 집합
* HashSet<T>
```java
public static void main (String[] args) {
    HashSet<String> set = new HashSet<>();
    set.add("aa");
    set.add("bb");
    set.add("aa");              // 중복되지 않아 2개만 존재
}
```
```java
set.add("cc");                  // 추가
set.contains("aa");             // 포함 여부
set.size();                     // 크기
set.remove("bb");               // 삭제
set.clear();                    // 전체 삭제
```

### HashMap
* Key, Value 로 저장하는 자료구조, 순서 중복 허용하지 않음
* HashMap<K, V>
```java
public static void main (String[] args) {
    HashMap<String, Integer> map = new HashMap<>();
    map.put("user1", 100);
    map.put("user2", 90);
}
```
```java
map.put("user3", 80);           // 추가
map.size();                     // 크기
map.get("user1");               // key에 해당하는 value 가져오기
map.containsKey("user1");       // key 포함 여부 확인
map.remove("user1");            // key에 해당하는 key-value 삭제
map.clear();                    // 전체 삭제
```

### Iterator
* 컬렉션의 모든 데이터 순회
* Iterator<T>
```java
public static void main (String[] args) {
    ArrayList<String> list = new ArrayList<>();
    list.add("aa");
    list.add("bb");

    Iterator<String> it = list.iterator();
    while (it.hashNext()) {
        System.out.println(it.next());
    }

    // 출력 결과
    // aa
    // bb
}
```
```java
it.hasNext();                   // 다음 요소가 있는지 확인 -> ture, false
it.next();                      // 다음 요소 가져오기
it.remove();                    // 삭제
```

### 익명 클래스
* 한 번만 사용되는 이름 없는 클래스
```java
public static void main (String[] args) {
    Person person = new Person() {
        // 익명 클래스
        @Override
        public void introduce() {
            System.out.println("익명 클래스 예제");
        }
    };
    
    person.introduce();
}
```

### 람다식
* 간결한 형태의 코드 묶음
* (전달값1, 전달값2, ... ) -> {코드}
```java
// 예제
public int add (int x, int y) {
    return x + y;
}
```
```java
// 예제 람다식 표현
(x, y) -> x + y
```

### 함수형 인터페이스
* 람다식을 위한 인터페이스
* 딱 하나의 추상 메소드를 가져야 함
```java
@FunctionalInterface
interface 인터페이스 {
    // 하나의 추상 메소드
}
```
```java
@FunctionalInterface
interface Calculator {
    int calculate (int x, int y);               // 하나의 추상 메소드 
}

public static void main (String[] args) {
    Calculator add = (x, y) -> x + y;           // 람다식
    int result = add.calculate(2, 3);
    System.out.println("2 + 3 = " + result);
}
```

### 스트림
* 배열, 컬렉션 데이터를 효과적으로 처리하기 위해 사용
```java
public static void main (String[] args) {
    List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
    numbers.stream()
        .filter(n -> n % 2 == 0)                // 짝수인 수들만 선택해서 필터링
        .map(n -> n * 2)                        // 각 요소들을 2배씩 곱하기
        .forEach(System.out::println);          // 각 요소들을 출력
}

// 출력 결과
// 4
// 8
```

### 예외처리
* 프로그램에서 발생가는한 문제 상황 처리
* catch
  * 예외의 종류에 따른 처리를 하기위해 사용
* throw
  * 의도적으로 예외 상황 발생시키기위해 사용
  * throw new 예외();
* finally
  * 예외가 발상하든 아니든 항상 실행되는 코드
  * 코드에서 사용된 리소스를 해제하거나 정리작업을 하기위해 사용
```java
try {
    명령문
} catch (변수1) {
    예외처리1
} catch (변수2) {
    예외처리2
} finally {
    명령문
}
```
```java
public static void main (String[] args) {
    int[] numbers = {1, 2, 3};
    int index = 5;

    try {
        int result = numbers[index];
        System.out.println("결과 : " + result);
    } catch (ArrayIndexOutOfBoundsException e) {        // 인덱스 범위 에러의 경우만 catch
        System.out.println("인덱스 에러 발생");
    } catch (Exception e) {
        System.out.println("에러 발생");
    } finally {
        System.out.println("실행 종료");
    }
}
```
```java
public static void main (String[] args) {
    try {
        int age = -1;
        if (age < 0) {
            throw new Exception("음수가 불가능합니다.");
        }
    } catch (Exception e) {
        System.out.println(e.getMessage());
    }
}
```

### Try With Resources
* 리소스 관리를 편하게 하는 방법
* 할당시킨 자원을 자동으로 해제함
```java
try (자원할당) {
    명령문
} catch (변수) {
    예외처리
}
```
```java
public static void main (String[] args) {
    try (FileWriter writer = new FileWriter("file.txt")) {
        writer.write("쓰기");
    } catch (Exception e) {
        System.out.println("에러 발생");
    }
}
```

### 사용자 정의 예외
* 개발자가 직접 정의한 예외
* 특정 상황에서 예외를 발생시키고 싶을 때
```java
class MyException extends Exception {
    public MyException (String message) {
        super(message);
    }
}
```

### 예외처리 미루고
* 문제가 발생했을 때, 메소드를 호출한 곳에서 예외처리
* 반환형 메소드명() throws 예외 { 명령문 }
```java
public static int divide (int a, int b) throws Exception {
    return a / b;
}

public static void main (String[] args) {
    try {
        divide(3, 0);           // throws를 통해 예외발생 후
    } catch (Exception e) {     // catch에서 예외 처리
        System.out.println("0으로 나눌 수 없습니다.")
    }
}
```

### Thread
* 여러 작업을 동시에 하기위해서 사용
```java
class 클래스명 extends Thread {
    public void run() {

    }
}
```
```java
class MyThread extends Thread {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Thread : " + i);
        }
    }
}

public static void main (String[] args) {
    MyThread thread = new MyThread();
    thread.start();     // 새로운 쓰레드를 만들어서 run() 동작 수행
}
```

### Runnable
* 여러 작업을 동시에 하기위해서 사용
```java
class 클래스명 implements Runnable {
    public void run() {
        
    }
}
```
```java
// thread로 구현하면 java에서 다중상속이 불가능하지만,
// interface로 구현하면 다른 클래스를 상속할 수 있다는 장점이 있음
class MyRunnable implements Runnable {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Runnable : " + i);
        }
    }
}

public static void main (String[] args) {
    MyRunnable runnable = new MyRunnable();
    Thread thread = new Thread(runnable);
    thread.start();
}
```

### Join
* 쓰레드 실행을 마칠 때까지 대기
```java
public static void main (String[] args) throws InterruptedException {

    thread.start();
    thread.join();          // 앞의 thread 실행을 마칠 때까지 대기 후,
    method();               // 뒤의 method 실행

}
```

### 다중 쓰레드
* 여러 쓰레드를 동시에 수행
```java
public static void main (String[] args) {
    Thread thread1 = new Thread(() -> {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Thread1 : " + i);
        }
    });

    Thread thread2 = new Thread(() -> {
        for (int i = 1; i <= 5; i++) {
            System.out.println("Thread2 : " + i);
        }
    });


    thread1.start();
    thread2.start();

}
```

### 동기화
* 여러 쓰레드가 공유된 자원에 동시에 접근하지 못하게 막는 것
```java
synchronized 메소드명 () {

}

synchronized (변수) {

}
```
```java
class SharedData {
    public int data = 0;

    // 각각의 쓰레드가 동시에 사용 불가
    synchronized public void increment() {  
        data++;
    }
}

public static void main (String[] args) throws InterruptedException {
    SharedData sharedData = new SharedData();
    Thread thread1 = new Thread(() -> {
        for (int i = 0; i < 1000; i++) {
            sharedData.increment();
        }
    });

    Thread thread2 = new Thread(() -> {
        for (int i = 0; i < 1000; i++) {
            sharedData.increment();
        }
    });

    thread1.start();
    thread2.start();

    thread1.join();
    thread2.join();

    System.out.println("SharedData : " + sharedData.data);    


    // 출력 결과
    // 2000

}
```

### 입력
* 프로그램에 데이터 입력 받기
```java
Scanner sc = new Scanner(System.in);

String word = sc.next();            // 문자열을 단어 단위로 입력 받기
int i = sc.nextInt();               // 정수 입력 받기
double d = sc.nextDouble();         // 실수 입력 받기
String line = sc.nextLine();        // 문장을 줄 단위로 입력 받기
```

### 출력
* 프로그램에서 결과 출력
* printf
  * %d : 정수
  * %f : 실수
  * %s : 문자열
  * %n : 줄바꿈
  * \- : 왼쪽 정렬
  * \+ : 부호 표시 (양수, 음수)
  * 0 : 빈공간 0으로 채우기
  * , : 세자리마다 콤마로 구분
  * . : 소수점 자리수
    * ("%.2f", 1.234) 이면 1.23 으로 출력
```java
System.out.print();
System.out.println();
System.out.printf();

String name = "A";
int age = 10;

System.out.printf("이름 : %s, 나이 : %d", name, age);
```

### 파일, 폴더
```java
file.createNewFile();               // 새 파일 생성
if (file.exists()) {}               // 파일 또는 폴더 존재 여부
file.getName();                     // 이름 정보
file.getAbsolutePath();             // 절대 경로 정보
file.length();                      // 파일 크기 (Byte)

file.mkdir();                       // 폴더 생성
file.mkdires();                     // 폴더들 생성
for (File file : file.listFiles())  // 파일 및 폴더 목록 조회
if(file.isFile())                   // 파일인지 여부
if(file.isDirectory())              // 폴더인지 여부
file.delete();                      // 파일 또는 폴더 삭제
```

### 파일 읽고 쓰기
* BufferedWriter
* BufferedReader