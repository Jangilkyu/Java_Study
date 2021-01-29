# 목표
- 자바의 열거형에 대해 학습하세요.

# 학습할 것 (필수)
# enum 정의하는 방법

C언어와 C++에서는 enum 클래스를 사용할 수 있었지만, JDK 1.5 이전의 자바에서는 enum클래스를 사용할 수 없었다.
자바에 enum클래스에서는 변수, 메소드 그리고 생성자를 추가할 수 있다.

- enum의 첫번째 라인에는 상수 리스트가 되어야하고, method, variable, constructor가 올 수 있다.
- 대문자로 상수이름을 짓는것을 추천한다.

## enum의 선언
```java
    public enum Fruit {
        ORANGE, LEMON, BANANA
    }
```
위에 정의된 enum클래스를 아래와 같이 호출하여 사용할 수 있다. 값은 ORANGE가 된다.
```java
    Fruit fruit = Fruit.ORANGE;
```

## enum 상수간의 비교
- 열거형 상수 간의 비교에는 `==`을 사용할 수 있습니다. `equals()가 아닌 ==으로 비교가능한 것은 그만큼 빠르다`는 이야기입니다.
그러나 `비교연산자(<, >)`는 사용할 수 없고 compareTo()는 사용 가능하다.

```java
Direction dir;

if (dir == Direction.WEST) {
	...
} else if (dir > Direction.WEST) {
	// 에러. 열거형 상수에 비교연산자는 사용 불가능
} else if (dir.compareTo(Direction.WEST) > 0) {
	// compareTo()는 가능
}
```

# enum이 제공하는 메소드 (values()와 valueOf())
|메소드|리턴 타입|설명|
|----|----|----|
|values()|	열거 배열|	모든 열거 객체들을 배열로 리턴|
|valueOf(String name)|	열거 타입|	주어진 문자열의 열거 객체를 리턴|
|ordinal()|	int|	열거 객체의 순번(0부터 시작)을 리턴|
|compareTo()|	int|	열거 객체를 비교해서 순번 차이를 리턴|
|name()|	String|	열거 객체의 문자열을 리턴|


## 1. values()

모든 열거 객체들을 배열로 리턴

```java
    enum Weekend{
        MON, TUE, WEN, THUR, FRI, SAT, SUN
    }

    public class UseEnum{
        public static void main(String args[]){
            for(Weekend week : Weekend.values()){
                System.out.println(week);
            }
        }
    }
```

## 2. valueOf()

주어진 문자열의 열거 객체를 리턴

```java
    enum Weekend{
        MON, TUE, WEN, THUR, FRI, SAT, SUN
    }

    public class UseEnum{
        public static void main(String args[]){

            Weekend week = Weekend.valueOf("Mon");
            System.out.println(week); // Mon이 출력이 된다.
        }
    }
```
## 3. ordinal()

열거 객체의 순번(0부터 시작)을 리턴

```java
    enum Weekend{
        MON, TUE, WEN, THUR, FRI, SAT, SUN
    }

    public class UseEnum{
        public static void main(String args[]){

            Weekend week = Weekend.WEN;
            System.out.println(week.ordinal()); 
            // 2가 출력이 된다.
        }
    }
```

## 4.name()
열거 객체의 문자열을 리턴

```java
    enum Weekend{
        MON, TUE, WEN, THUR, FRI, SAT, SUN
    }

    public class UseEnum{
        public static void main(String args[]){

            Weekend week = Weekend.WEN;
            String name = week.name();
            System.out.println(name); 
            // WEN이 출력이 된다.
        }
    }
```

## 5.compareTo()

열거 객체를 비교해서 순번 차이를 리턴
만약 열거 객체가 매개값의 열거 객체보다 순번이 빠르다면 음수가, 순번이 늦다면 양수가 리턴된다.


```java
    enum Weekend{
        MON, TUE, WEN, THUR, FRI, SAT, SUN
    }

    public class UseEnum{
        public static void main(String args[]){

            Weekend week1 = Weekend.WEN;
            Weekend week2 = Weekend.SAT;

            int re1 =  week1.compareTo(week2);
            int re2 =  week1.compareTo(week1);

            System.out.println(re1); 
            System.out.println(re2); 

        }
    }
```
# java.lang.Enum

Enum 클래스는 모든 java 언어 열거타입의 상위 클래스입니다.
따라서 모든 enum들은 내부적으로 java.lang.Enum 클래스에 상속이 됩니다. 위에 enum이 제공하는 메소드들 또한 java.lang.Enum 내부에 존재합니다.

<img src = "https://user-images.githubusercontent.com/69107255/106306493-7d842100-62a1-11eb-902a-aa84952fba58.png">

# EnumSet
EnumSet이란 enum 타입과 Set을 함께 사용하도록 만든 것이다. 

EnumSet에는 아래와 같은 method들이 있다.

**java.util.EnumSet**
<img src ="https://user-images.githubusercontent.com/69107255/106307573-df915600-62a2-11eb-963a-0c528415b8f6.png">