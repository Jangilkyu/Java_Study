# 목표
- 자바의 제네릭에 대해 학습하세요.

학습할 것 (필수)

## 제네릭 사용법
제네릭(Generic)은 클래스 내부에서 사용하는 데이터의 타입(Type)을 클래스의 인스턴스를 생성할 때 결정하는 것을 의미합니다.
String,Integer,Character등과 같은 타입을 메소드, 클래스 및 인터페이스의 매개변수가 되도록 허용하는 것입니다.
제네릭은 클래스나 메소드에서 사용할 내부 데이터 타입을 컴파일 시에 미리 지정함으로 써 미리 타입 검사(type check)를 수행하면 
클래스나 메소드 내부에서 사용되는 객체의 타입 안정성을 높일 수있고, 반환값에 대한 타입 변환 및 타입 검사에 들어가는 노력을 줄일 수 있습니다.

제네릭은 <>사이에 개발자가 사용하고자 하는 Type을 선언해준다.
T는 타입변수(type variable)이고, 임의의 참조형 타입을 의미한다. 
```java
    public class 클래스명<T> {...}
    public interface 인터페이스명<T> {...}
```
```java
class Student<T> {
    public T name;
    private String hakbun;
    
    public String getHakbun() {
        return getHakbun;
    }
    
    public void seHakbun(String hakbun) {
        this.hakbun = hakbun;
    }
    
    public T getName() {
        
        return name;
    }
    
    public void setName(T name) {
        this.name = name;
    }
}
```

```java
    public class GenericTest {
        public static void main(String[] args) {
            Student<String> s1 = new Student<String>();
            s1.setName("홍길동");
            
            //Person<StringBuilder> s2 = new Person<>(); <>에는 타입추론이 되어서 명시를 안해줘도 된다.
            Person<StringBuilder> s2 = new Person<>();
            s2.setName(new StringBuilder("유관순"));
            
            System.out.println(s1.getName());
            System.out.println(s2.getName());
        }
    }
```



## 제네릭 주요 개념 (바운디드 타입, 와일드 카드)

- Bounded type
제네릭 타입의 범위를 제한 할 수 있습니다.

- Wildcard
제네릭 타입을 매개변수나 리턴타입으로 사용할 때 타입 파라미터를 제한할 목적
 <T extends 상위 또는 인터페이스>는 제네릭 타입과 제네릭 메소드를 선언할 때 제한을 한다.

- `제네릭타입<?>` : Unbounded Wildcards (제한없음)
    - 타입 파라미터를 대치하는 구체적인 타입으로 모든 클래스나 인터페이스 타입이 올 수 있다.

- `제네릭타입<? extends 상위타입>` : Upper Bounded Wildcards (상위 클래스 제한)
    - 타입 파라미터를 대치하는 구체적인 타입으로 상위 타입이나, 그 상위 타입의 하위 타입만 올 수 있다. 따라서, 상위 클래스 제한 이라고 한다.
- 즉, 상위 타입이 해당 자리에 들어갈 수 있는 가장 상위 타입이다.

- `제네릭타입<? super 하위타입>` : Lower Bounded Wildcards (하위 클래스 제한)
- 타입 파라미터를 대치하는 구체적인 타입으로 하위 타입이나, 그 하위 타입의 상위 타입이 올 수 있다. 따라서, 하위 클래스 제한 이라고 한다.
- 즉, 하위 타입이 해당 자리에 들어갈 수 있는 가장 하위 타입이다.

## 제네릭 메소드 만들기

-  제네릭 메소드를 선언하는 방법은 리턴 타입 앞에 <> 기호를 추가하고 타입 파라미터를 기술한 다음, 
 리턴 타입과 매개 타입으로 타입 파라미터를 사용하면 된다.
- static 변수에는 제네릭을 사용할 수 없지만 static 메소드에는 제네릭 메소드를 활용할 수 있다.

```java
    public <타입 파라미터, ...> 리턴 타입 메소드명(매개변수, ...) { ... }
```

```java
    public <T> Student<T> study(T t) { ... }
```

## Erasure
제네릭은 타입의 안정성을 보장하며 실행시간에 오버헤드가 발생하지 않도록 하기 위해 추가 되었다. 컴파일러는 컴파일 시점에 제네릭에 대하여 "type erasure(타입 이레이저)"라고 부르는 프로세스를 적용한다.

타입 이레이저는 모든 타입 파라미터들을 제거하고나서 그 자리를 제한하고 있는 타입으로 변경하거나 타입 파라미터의 제한 타입이 지정되지 않았을 경우에는 Object 로 대체한다. 따라서 컴파일 후에 바이트 코드는 새로운 타입이 생기지 않도록 보장하는 일반 클래스들과 인터페이스, 메소드들만 포함한다. Object 타입도 컴파일 시점에 적절한 캐스팅이 적용된다.

<T>인 경우 T는 Object로 대체된다.
```java
public <T> List<T> genericMethod(List<T> list) { 
	return list.stream().collect(Collectors.toList()); 
}

// for illustration
public List<Object> withErasure(List<Object> list) { 
	return list.stream().collect(Collectors.toList()); 
}

// which in practice results in
public List withErasure(List list) {
    return list.stream().collect(Collectors.toList());
}
```