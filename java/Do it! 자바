인프런 Do it! 자바 프로그래밍 입문 강의를 듣고 정리한 노트

자바를 많이 사용하면서 기본기가 살짝 부족한것같아 다시 다지고자 인강을 듣게 되었다. 아는 부분은 말고 헷갈리는 부분과 잘 사용하지 않은 부분, 모르는 부분 위주로 기록하고 공부하였다.

## 2. 자바의 핵심 - 객체지향 프로그래밍

### 클래스와 객체 - static 변수

static을 사용해 변수와 함수를 정의할 수 있다. 인스턴스는 클래스로 생성한 각각의 객체

static 변수의 정의와 사용 방법 : static 예약어 + 자료형 + 변수이름;

![image-20210228141449657](C:\Users\WorkPC\AppData\Roaming\Typora\typora-user-images\image-20210228141449657.png)

여러 개의 인스턴스가 **같은 메모리의 값을 공유**하기 위해 사용. 인스턴스 생성과 관계없이 메모리에 잡힘

![image-20210228141439054](C:\Users\WorkPC\AppData\Roaming\Typora\typora-user-images\image-20210228141439054.png)

static 변수는 인스턴스가 생성될 때 마다 다르 메모리를 가지는 것이 아니라 프로그램이 메모리에 적재(load) 될때 데이터 영역의 메모리에 생성됨. 따라서 인스턴스의 생성과 관계없이 **클래스 이름으로 직접 참조** 함. 클래스 변수라고도 함

```java
Student.serialNum = 100; // serialNum이 static 변수
```

멤버변수는 다른 말로 인스턴스 변수라고 함

static 변수의 예

여러 인스턴스가 하나의 메모리 값을 공유할 때 필요하다. 학생이 생성될 때마다 학번이 증가해야하는 경우 기준이 되는 값은 static 변수로 생서앟여 유지한다. 각 학생이 생성될 때마다 static 변수 값을 복사해 와서 하나 증가 시킨 값을 생성된 인스턴스의 학번 변수에 저장해 준다.



```java
public Class Student {
    private static int serialNum = 10000;
    
    int studentId;
    String studentName;
    
    public Student() {
        serialNumm++;
        studentId = serialNum;
    }
    
    public static int getSerialNum(){
        int i = 10; // 지역 변수
        studentName = "홍길동"; //멤버 변수(인스턴스 변수) -> 사용할 수 없음
        return serialNum; // static 변수(클래스 변수)
    }    
    
}
```

- 지역변수 - 해당 메서드가 호출될때 생성이 되고 메서드가 끝나면 없어진다.
- 멤버변수(인스턴스변수) - 인스턴스가 new될 때 생성이 된다. 
  - static 메서드는 new하지 않아도 인스턴스를 생성하지 않아도 사용할 수 있다. 따라서 이 메서드 안에서 생성되지도 않은 인스턴스의 멤버변수에 홍길동을 넣게 되면 에러가 발생한다.
  - 따라서 static 메서드 안에서는 인스턴스 변수를 사용할 수 없다.
- static변수(클래스변수)

### Static 메서드

클래스 메서드라고 함. 메서드에 static 키워드를 사용하여 구현. 주로 static 변수를 위한 기능 제공

static 메서드에서 인스턴스 변수를 사용할 수 없다. static 메서드도 인스턴스의 생성과 관계없이 클래스 이름으로 직접 메서드 호출

```java
Student.getSerialNum(); // getSerialNum()이 static 메서드
```

인스턴스의 변수의 경우 꼭 인스턴스가 먼저 생성되어야하므로 static 메서드에서는 생성이 불확실한 인스턴스 변수를 사용할 수 없다.



### 변수의 유효 범위

![image-20210228145235300](C:\Users\WorkPC\AppData\Roaming\Typora\typora-user-images\image-20210228145235300.png)



### static 응용 - singleton 패턴

전 시스템에 단 하나의 인스턴스만 존재하도록 구현한 방식으로 자바에는 글로벌 변수가 없기 때문에 static 변수를 사용한다. 기본적으로 여러개가 생성될 수 있는데 그것을 막아서 단 하나만 생성될 수 있도록 생성자를 private로 만들어서 구현한다. 또 외부에서 생성된 static으로 생성된 객체를 사용할 수 있어야 하기 때문에 public으로 선언된 static 메서드를 제공한다.

```java
public class Company {
    
    //외부에서 생성할 수 없기 때문에 내부에 인스턴스를 생성한다.
    //전체에서 유일하게 사용할 수 있는 객체
    //private - 함부로 null이거나 값이 바뀌면 안돼
    //static - 단하나만 있어야해
    private static Company singleton = new Company(); 
    
    // 생성자를 private로 선언하면 외부에서 생성자를 호출할 수 없다.
    private Company() {}
    
    //외부에서 사용할 수 있도록 메서드를 하나 만들어준다.
    //static - 객체를 생성하지 않고 사용하도록
    public Company getSingleton() {
        // 방어적인 코드를 추가해줄수도 있다.
        if(singleton == null) {
            singleton = new Company();
        }
        return singleton; 
    }
}
```





## ArrayList 클래스

기존 배열은 길이를 정해서 선언하므로 사용 중 부족한 경우 다른 배열로 복사하는 코드를 직접 구현해야함. 중간의 요소가 삭제되거나 삽입되는 경우도 나머지 요소에 대한 조정하는 코드를 구현해야함

ArrayList 클래스는 자바에서 제공되는 객체 배열이 구현된 클래스 여러 메서드와 속성등 사용하여 객체 배열을 편리하게 관리할 수 있다. 가장 많이 사용하는 객체 배열 클래스이다.

```java
ArrayList<E> list = new ArrayList<E>(); //선언
```

타입을 지정하지 않으면 데이터를 저장하고 꺼낼 때 오브젝트로 꺼내오게 되서 타입 변환이 필요하다.

**주요 메소드**

![image-20210305151107304](C:\Users\WorkPC\AppData\Roaming\Typora\typora-user-images\image-20210305151107304.png)

요소를 추가하거나 제거 할 때 각 내부에서 코드가 모두 구현되어 있으므로 배열을 직접 선언하여 사용하는 것보다 편리함. help를 참고해서 API 보는 연습을 많이 하자!



## 상속과 다형성

**상속이란?**

클래스를 정의할 때 이미 구현된 클래스를 상속(inheritance) 받아서 속성이나 기능이 확장되는 클래스를 구현함

- 상속하는 클래스 : 상위 클래스, parent class, base class, super class
- 상속받는 클래스 : 하위 클래스, child class, derived class, sub class

```java
class B extends A {
    // A 클래스가 B 클래스에게 상속한다.
    // B 클래스가 A 클래스를 상속받는다.
    // extneds 뒤에는 단 하나의 class 만 사용할 수 있음
    // 자바는 single inheritance 만을 지원함
}
```

상위 클래스는 하위 클래스 보다 일반적인 의미를 가짐, 하위 클래스는 상위 클래스 보다 구체적인 의미를 가짐

**접근 제한자 가시성**

![image-20210306231704187](C:\Users\WorkPC\AppData\Roaming\Typora\typora-user-images\image-20210306231704187.png)

**상속에서 클래스 생성과정**

하위 클래스가 생성될 때 상위 클래스가 먼저 생성된다. 상위 클래스의 생성자가 호출되고 하위 클래스의 생성자가 호출된다. 하위 클래스의 생성자에서는 무조건 상위 클래스의 생성자가 호출되어야 한다. 아무것도 없는 경우 컴파일러는 상위 클래스의 기본 생성자를 호출하기 위한 `super()`를 코드에 넣어준다. `super()` 호출되는 생성자는 상위 클래스의 기본 생성자이다. 만약 상위 클래스의 기본 생성자가 없는 경우 (매개 변수가 있는 생성자만 존재하는 경우) 하위 클래스는 명시적으로 상위 클래스를 호출해야한다.

**super 예약어**

this가 자기 자신의 인스턴스의 주소를 가지는 것처럼 super는 하위 클래스가 상위 클래스에 대한 주소를 가지게 된다. 하위 클래스가 상위 클래스에 접근 할 때 사용할 수 있다.



## 오버라이딩과 다형성

**다형성**

하나의 코드가 여러가지 자료형으로 구현되어 실행되는 것으로 정보은닉, 상속과 더불어 객체지향 프로그래밍의 가장 큰 특징 중 하나이다. 객체지향 프로그래밍의 유연성, 재활용성, 유지보수성에 기본이 되는 특징임

**상속을 언제 사용할까?**

여러 클래스를 생성하지 않고 하나의 클래스에 공통적인 요소를 모으고 나머지 클래스는 이를 상속받은 다음 각각 필요한 특성과 메서드를 구현하는 방법. 하나의 클래스에 여러 특성을 한꺼번에 구현하는 경우 많은 코드 내에 많은 if문이 생길 수 있다. 

**@Override**

어노테이션을 사용하는이유는 컴파일러에게 재정의된 메소드라는 것을 알려주기 위함



## 추상클래스

- 추상 메서드를 포함한 클래스
- 추상 메서드는 구현코드 없이 메서드의 선언만 잇음
- `abstract` 예약어 사용
- 추상클래스는 new (인스턴스화) 할 수 없음
- 상속받아서 사용하려고 사용함

**final 예약어**

- final 변수는 값이 변경될 수 없는 상수임
- final 변수는 오직 한 번만 값을 할당할 수 있음
- final 메서드는 하위 클래스에서 재정의(overriding) 할 수 없음
- final 클래스는 더이상 상속이 되지 않음 ex) 자바의 String 클래스

**템플릿 메서드**

추상메서드나 구현된 메서드를 활용하여 전체 기능의 흐름(시나리오)을 정의하는 메서드로 final로 선언하면 하위 클래스에서 재정의 할 수 없다. 프레임 워크에서 많이 사용되는 설계 패턴이다. 추상 클래스로 선언된 상위 클래스에 템플릿 메서드를 활용하여 전체적인 흐름을 정의하고 하위 클래스에서 다르게 구현되어야하는 부분은 추상 메서드로 선언해서 하위 클래스가 구현하도록 한다.

**템플릿 메서드 구현 예**

![image-20210307162503547](C:\Users\WorkPC\AppData\Roaming\Typora\typora-user-images\image-20210307162503547.png)

각 PlayLevel 별 가능한 기능은 다르다. 단, 기능의 순서는 run(), jump(), turn() 의 순서임. 기능의 순서와 반복에 대한 구현은 go(int)메서드에서 구현되어있음(템플릿 메서드)

```java
public abstract class PlayerLevel {
    //각 레벨마다 run(), jump(), turn() 기능은 다르게 구현되어야하므로 추상메서드로 선언
    public abstract void run();
    public abstract void jump();
    public abstract void turn();
    public abstract void showLevelMessage();
    
    //템플릿 메서드
    //재정의되면 안되므로 final로 선언
    //go() 메서드에서 각 순서와 반복횟수를 구현
    final public void go(int count) {
        run();
        for (int i = 0; i < count; i++) {
            jump();
        }
        turn();
    }
}
```

```java
public class Player {

  private PlayerLevel level;

  public Player() {
    level = new BeginnerLevel();
    level.showLevelMessage();
  }

  public PlayerLevel getLevel() {
    return level;
  }

  public void upgradeLevel(PlayerLevel level) {
    this.level = level;
    level.showLevelMessage();
  }

  public void play(int count) {
    level.go(count);
  }
}
```

```java
public class BeginnerLevel extends PlayerLevel {

  @Override
  public void run() {
    System.out.println("천천히 달립니다.");
  }

  @Override
  public void jump() {
    System.out.println("점프할줄 몰라!!");
  }

  @Override
  public void turn() {
    System.out.println("턴할 줄 몰라!!");
  }

  @Override
  public void showLevelMessage() {
    System.out.println("###########초보자레벨#########");
  }
}
```

```java
public class AdvancedLevel extends PlayerLevel {
  @Override
  public void run() {
    System.out.println("빨리 달립니다.");
  }

  @Override
  public void jump() {
    System.out.println("높이 점프합니다.");
  }

  @Override
  public void turn() {
    System.out.println("턴할 줄 몰라!!");
  }

  @Override
  public void showLevelMessage() {
    System.out.println("###########중급자레벨#########");
  }
}

```

```java
public class SuperLevel extends PlayerLevel{

  @Override
  public void run() {
    System.out.println("겁나게 빨리 달립니다.");
  }

  @Override
  public void jump() {
    System.out.println("겁나게 높이 점프합니다.");
  }

  @Override
  public void turn() {
    System.out.println("한바퀴 돕니다.");
  }

  @Override
  public void showLevelMessage() {
    System.out.println("###########상급자레벨#########");
  }
}

```

```java
public class MainBoard {

  public static void main(String[] args) {
    Player player = new Player();
    player.play(1);

    AdvancedLevel aLevel = new AdvancedLevel();
    player.upgradeLevel(aLevel);
    player.play(2);

    SuperLevel sLevel = new SuperLevel();
    player.upgradeLevel(sLevel);
    player.play(3);

  }
}
```



## 인터페이스

상수(public static final)와 추상 메서드(public abstract)가 선언된다. -> 키워드를 생략해도됨

- 모든 메서드가 추상 메서드(abstract method)로 이루어진 클래스

- 형식적인 선언만 있고 구현은없음

  ```java
  interface 인터페이스이름 { 
   public static final float PI = 3.14f;
   public void add();
  }
  ```

**왜 인터페이스를 사용하는가?**

![image-20210307180418146](C:\Users\WorkPC\AppData\Roaming\Typora\typora-user-images\image-20210307180418146.png)

 **인터페이스의 요소**

- 상수 : 모든 변수는 상수로 변환됨
- 추상메서드 : 모든 메서드는 추상메서드로 구현됨
- 디폴트 메서드 : 기본 구현을 가지는 메서드, 구현 클래스에서 재정의할 수 있음
- 정적 메서드 : 인스턴스 생성과 상관없이 인터페이스 타입으로 사용할 수 있는 메서드
- private 메서드 : 인터페이스를 구현한 클래스에서 사용하거나 재정의 할 수 잆음. 인터페이스 내부에서만 기능을 제공하기 위해 구현하는 메서드 





# 기본 클래스

기본적으로 자바를 사용하면서 많이 사용하는 클래스들을 소개합니다. 

### Java.lang 패키지

- 프로그래밍시 import 하지 않아도 자동으로 import 됨
- import java,lang.*; 문장이 추가 됨
- 많이 사용하는 기본 클래스들이 속한 패키지
- String, Integer, System 등

#### 1. Object 클래스

- 모든 클래스의 최상위 클래스
- java.lang.Object 클래스
- 모든 클래스는 Object 클래스에서 상속 받음
- 모든 클래스는 Object 클래스의 메서드를 사용할 수 있음
- 모든 클래스는 Object 클래스의 메서드 중 일부는 재정의 할 수 있음(final로 선언된 메서든는 재정의 할 수 없음)
- 컴파일러가 extents Object를 추가함

**Object 클래스 메서드**

![image-20210312162050618](C:\Users\WorkPC\AppData\Roaming\Typora\typora-user-images\image-20210312162050618.png)

- **`toString()` 메서드**

  - Object 클래스의 메서드는 원래 이렇게 표현되어있다.

    ```java
    getClass().getName() + '@' + Integer.toHexString(hashCode())
    ```

    ![image-20210312162526280](C:\Users\WorkPC\AppData\Roaming\Typora\typora-user-images\image-20210312162526280.png)

  - 객체의 정보를 String 으로 바구어 사용할 때 쓰임

  - String이나 Integer 클래스에는 이미 재정의 되어있음 (ArrayList도)

  - String은 문자열을 반환

  - Integer는 정수값 반환

- **`equals()` 메서드**

  - String과 Integer는 재정의가 되어있다.

  - 두 인스턴스가 같다라는 것은 같은 메모리 영역이여야한다.  (== 는 같은 주소를 같고있냐임 물리적) 

  - 두 인스턴스의 주소값을 비교하여 true/false를 반환

  - 재정의 하여 두 인스턴스가 논리적으로 동일함의 여부를 반환

  - 같은 학번의 학생인 경우 여러 인스턴스의 주소 값은 다르지만, 같은 학생으로 처리해야 학점이나 정보 산출에 문제가 생기지 않으므로 이런 경우 equals() 메서드를 재정의함

    ```java
    Student lee = new Student(100, "이상원");
    Student lee2 = lee; //주소 복사
    ```

    ![image-20210312163355919](C:\Users\WorkPC\AppData\Roaming\Typora\typora-user-images\image-20210312163355919.png)

    ```java
    String str1 = new String("test");
    String str2 = new String("test");
    
    System.out.println(str1 == str2);		//false -> 물리적
    System.out.println(Str1.equals(str2));	//true -> 논리적
    ```

    ```java
    //Student 클래스가 있다고 가정
    Student s1 = new Student(1001, "Tomas");
    Student s2 = new Student(1001, "Tomas");
    
    System.out.println(s1 == s2);		//false
    System.out.println(s1.equals(s2));	//false -> 이 equals의 원래는 == 랑 똑같기 때문에 equals를 오버라이딩(재정의) 해주어야한다.
    
    //재정의 방법
    @Override
    public boolean equals(Object obj) {
        
        //Student 객체인지 확인
        if (obj instanceof Student) {
            Student std = (Student)obj; //다운캐스팅
            if (studentId == std.studentId) return true;
            else return false;
        }
        return false;
    }
    ```

- **`hashCode()` 메서드**

  - hash : 정보를 저장, 검색하기 위해서 사용하는 자료구조

  - 자료의 특정 값(키 값) 에 대해 저장위치를 반환해주는 해시함수를 사용함

    ![image-20210312164900611](C:\Users\WorkPC\AppData\Roaming\Typora\typora-user-images\image-20210312164900611.png)

  - 해시 함수는 어떤 정보인가에 따라 다르게 구현 됨

  - hashCode() 메서드는 인스턴스의 저장 주소를 반환함

  - 힙 메모리에 인스턴스가 저장되는 방식이 hash

  - hashCode()의 반환값 : 자바 가상 머신이 저장한 인스턴스의 주소값을 10진수로 나타냄

  - 서로 다른 메모리의 두 인스턴스가 같다면

    - 재정의 된 equals() 메서드 값이 true
    - 동일한 hashCode() 반환값을 가져야함

  - 논리적으로 동일함을 위해 equals() 메서드를 재정의 하였다면 hashCode() 메서드로 재정의 하여 동일한 값이 반환되도록 함

  - String 클래스 : 동일한 문자열 인스턴스에 대해 동일한 정수가 반환됨

  - Integer 클래스 : 동일한 정수값의 인스턴스에 대해 동일한 정수값이 반환됨

    ```java
    String str1 = new String("test");
    String str2 = new String("test");
    
    //Student 클래스가 있다고 가정
    Student s1 = new Student(1001, "Tomas");
    Student s2 = new Student(1001, "Tomas");
    
    //String은 같은 값이 나옴 > 왜?
    //equals() 를 재정의를 했다는 것은 물리적으로 다르지만 논리적으로는 같다라는 것
    //논리적으로 같은 두개의 인스턴스는 동일한 인스턴스의 해시코드를 반환하는게 맞다
    //따라서 equals()를 재정의한다면 hashCode()도 재정의하여 동일하게 반환하여야한다.
    //원래의 값을 알고싶다면 System.identityHashCode()를 사용
    System.out.println(str1.hashCode()); //233882
    System.out.println(str2.hashCode()); //233882
    
    System.out.println(s1.hashCode()); 	//82824829
    System.out.println(s2.hashCode());	//48491938	
    ```

    ```java
    //재정의
    @Override
    public boolean equals(Object obj) {
        
        //Student 객체인지 확인
        if (obj instanceof Student) {
            Student std = (Student)obj; //다운캐스팅
            if (studentId == std.studentId) return true;
            else return false;
        }
        return false;
    }
    
    //equals() 를 재정의한 멤버변수를 가져다가 hashCode() 도 재정의
    public int hashCode() {
        return studentId;
    }
    ```

- **`clone()` 메서드**

  - 객체의 원본 복제하는데 사용하는 메서드

  - 원본을 유지해 놓고 복사본을 사용할 때

  - 기본 틀(prototype)을 두고 복잡한 생성과정을 반복하지 않고 복제

  - clone() 메서드를 사용하면 객체의 정보(멤버변수 값)가 같은 인스턴스가 또 생성되는 것이므로 객체 지향 프로그램의 정보은닉, 객체 보호의 관점에서 위배될 수 있음

  - 객체의 clone() 메서드 사용을 허용한다는 의미로 cloneable 인터페이스를 명시해줌

    ```java
    class Circle implements Cloneable {
        // 객체를 복제해도 된다는 의미로 Cloneable 인터페이스를 함께 선언
    }
    ```

#### 2. String 클래스

- String을 선언하는 두 가지 방버

  ```java
  String str1 = new String("abc");	//생성자의 매개변수로 문자열 생성
  String str2 = "test";				//문자열 상수를 가리키는 방식
  ```

- 힙 메모리에 있는 인스턴스로 생성되는 경우와 상수풀(constant pool)에 있는 주소를 참조하는 방법 두 가지

  ![image-20210312180629725](C:\Users\WorkPC\AppData\Roaming\Typora\typora-user-images\image-20210312180629725.png)

- 상수 풀의 문자열을 참조하면 모든 문자열이 같은 주소를 가리킴

  ```java
  String str1 = new String("abc");
  String str2 = new String("abc");
  
  System.out.println(str1 == str2);	//false
  
  String str3 = "abc";
  String str4 = "abc";
  
  System.out.println(str3 == str4);	//true
  ```

- String 클래스로 문자열 연결

  - 한 번 생성된 String값(문자열)은 불변(immutable)
  - 두 개의 문자열을 연결하면 새로운 인스턴스가 생성됨
  - 문자열 연결을 계속하면 메모리에 gabage가 많이 생길 수 있음

- 문자열 연결 작업 시에는 StringBuilder, StringBuffer 사용하기

  - 내부적으로 가변적인 char[] 배열을 가지고 있는 클래스
  - 문자열을 여러번 연결하거나 변경할 때 사용하면 유용함
  - 매번 새로 생성하지 않고 기존 배열을 변경하므로 gabage가 생기지 않음
  - StringBuffer는 멀티 쓰레드 프로그래밍에서 동기화(sybchronization)을 보장
  - 단일 쓰레드 프로그램에서는 StringBuilder를 사용하기를 권장
  - toString() 메서드로 String을 반환

### 3. Wrapper 클래스

- 기본 자료형(privitive data type) 에 대한 클래스

  ![image-20210312190506996](C:\Users\WorkPC\AppData\Roaming\Typora\typora-user-images\image-20210312190506996.png)

- 오토 박싱과 언박싱

  - Integer 는 객체이고, int 는 4바이트 기본 자료형인데 두 개의 자료를 같이 연산할 떄 자동으로 변환이 일어남

    ```java
    Integer num1 = new Integer(100);
    int num2 = 200;
    
    int sum = num1 + num2; 	// num1.intValue()로 변환 -> 언박싱
    Integer num3 = num2;	// Integer.valueOf(num2)로 변환 -> 오토박싱
    ```

### 4. Class 클래스

- 자바의 모든 클래스와 인터페이스는 컴파일 후 class 파일로 생성됨
- class 파일에는 객체의 정보 (멤버변수, 메서드, 생성자등) 가 포함되어 있음
- Class 클래스는 컴파일된 class 파일에서 객체의 정보를 가져올 수 있음
- 

1. Object 클래스의 getClass() 메서드 사용하기

   ```java
   String s = new String();
   Class c = s.getClass(); //getClass()의 반환형은 Class로 오브젝트의 메소드임
   
   System.out.println(c.getName()); //패키지이름.클래스이름 으로 출력
   ```

2. 클래스 파일 이름을 Class 변수에 직접 대입하기

   ```java
   Class c = String.Class;
   ```

3. Class.forName("클래스이름") 메서드 사용하기 

   클래스 이름을 스트링으로 가져서 클래스를 메모리에 올리는 동적로딩이라고하는 그런역할을 하는 애다. 얘는 기억해두세요

   ```java
   Class c = Class.forName("java.lang.String");
   ```

#### Class.forName() 메서드로 동적 로딩하기

- 동적 로딩이란? 컴파일시에 데이터 타입이 모두 binding 되어 자료형이 로딩되는 것(static loding) 이 아니라 실행 중에 테이터 타입을 알고 binding 되는 방식
- 프로그래밍 할 때는 어떤 클래스를 사용할지 모를 때 변수로 처리하고 실행될 때 해당 변수에 대입된 값의 클래스가 실행될 수 있도록 Class 클래스에서 제공하는 static 메서드
- 실행 시에 로딩되므로 경우에 따라 다른 클래스가 사용될 수 잇어 유용함
- 컴파일 타임에 체크할 수 없으므로 해당 문자열에 대한 클래스가 없는 경우 예외(ClassNotFoundException)이 발생할 수 있음





