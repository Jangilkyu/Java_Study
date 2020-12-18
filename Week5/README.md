# 목표
- 자바의 Class에 대해 학습하세요.

# 학습할 것 (필수)
- 클래스 정의하는 방법
- 객체 만드는 방법 (new 키워드 이해하기)
- 메소드 정의하는 방법
- 생성자 정의하는 방법
- this 키워드 이해하기

# **클래스 정의하는 방법**

## **OOP(Object Oriented Programming)**
> 객체 지향 언어

## **정의**
> `실생활에 존재하는 
모든 사물` 을 `객체` 로 보고, 그 `사물`을 `컴퓨터 언어로 구현`하여 사용하기 적합한 언어

## **CLASS란?**
> 대상을 구현하기 위한 **설계도**

## **클래스의 3대 특징**
- 상속
- 다형성
- 캡슐화

## **클래스 작성 문법**

```java
        접근지정자 class 클래스명 extends 부모클래스명 implements 부모인터페이스명
```

## **class 접근지정자**
|한정자|같은 클래스|같은 패키지|하위 클래스|전체|
|:----:|:----:|:----:|:----:|:----:|
|public|Yes|Yes|Yes|Yes|
|protected|Yes|Yes|Yes||
|default|Yes|Yes||||
|private|Yes|||||||

## **class 작성 순서**
1. **대상선정**
   - **대상**: 보드마카펜
   - 검은색 보드마카펜 / 파란색 보드마카펜 / 빨간색 보드마카펜 
2. **객체모델링(추상화 작업)**
    > 대상의 공통 특징을 추출
    - **명사적인 특징(눈에 보이는 특징)**: 뚜껑, 몸체, 색
    - **동사적인 특징(동작 특징)**: 쓴다. 
3. **클래스작성**
    > 설계도 작성 - 마카펜
    - 클래스명(설계도 이름) / 변수(값 저장) / method(업무 처리)
      - 클래스명: 마카펜
      - **변수**: 뚜껑, 몸체, 색
      - **메소드**: 쓴다. 
4. **객체생성**
    > 클래스를 가지고 객체(구현체) 생성
    - **instance화(객체화, Object화)**: memory에 저장(class, stack, heap)
    ```java
        클래스명 객체명 = new 클래스명();
    ```
5. **생성된 객체 사용**
    ```java
        객체명.변수명;
        객체명.method명();
    ```

# 객체 만드는 방법 (new 키워드 이해하기)

## 참조형 데이터형
> 값은 메모리에 힙영역에 생성되고, 그 시작 주소를 저장하는 데이터형

- 힙 영역에 생성할려면 ?
    - new가 필요
- new가 사용되어 값을 생성 하는 것을 객체화라고 한다.

```java
public class Person{

    public Person(){

    }


    public static void main(String[] args){
            Person p = new Person();
    }
}
```

# **메소드 정의하는 방법**

## **method**
> 업무를 구분하여 작성할 때 사용

## **method 특징**

- 중복코드를 최소화 할 수 있다.
- `instance method`와 `static method` 2가지를 만들 수 있다.
- polymorphism을 지원(method Overload, method Override)

## **method 문법**

```java
method 문법

  접근지정자 반환형 method명(매개변수){
    
    업무 구현

  }
```

## **instance method**
> 클래스의 인스턴스 변수를 사용하여 일을 처리하는 method
- 객체화를 하여 객체명.method명( ) 으로 호출하여 사용

## **static method**
> 객체가 가지고 있는 값을 사용하여 일을 처리하는 것이 아닌, 입력된 값을 가지고 일시적인 연산을 할 때 사용
- 객체화를 하지 않고 클래스명.method명( ) 으로 호출하여 사용.

## **method의 접근지정자**

| 폴더개념의 접근지정자|(1개 사용 가능) |
|:----|:----|
|public|클래스 외부에서 호출 가능|
|protected| 같은 패키지의 다른 클래스에서 호출 가능 / 패키지가 다르면 상속관계의 자식클래스에서만 호출 가능
|private| 클래스안에서만 호출 가능
|default| 같은 패키지의 다른 클래스에서 호출 가능 / 패키지가 다르면 호출 불가능

|메모리개념의 접근지정자|(N개 사용 가능)|
|:----|:-----|
|static| static method로 만들 때
|final| Override를 막을 때
|synchronized| multi thread에서 동시 호출을 막을 때

## **반환형(return type)**
> method안에서 업무처리한 결과를 밖으로 내보낼 때 사용

## **매개변수(parameter)**
- method외부에 존재하는 값(arguments)을 method 내부로 전달하기 위한 변수
- method를 호출 할때 매개변수의 개수와 형에 대해 일치하여 호출 

## **return**
- method가 반환형을 가지고 있다면 method의 가장 마지막 줄에 반드시 return을 정의해야한다.
- return은 값을 반환할 때 사용

**return의 문법**
```java
  return 값;
        //값의 종류: 상수, 변수, 연산식,
```

## method의 4가지 형태
**1. 반환형 없고, 매개변수 없는 형. - 고정적인 일**
  ```java
      public void typeA(){

      }// 닫힘괄호의 의미는 호출한 곳으로 돌아가라

      호출) 객체명.typeA();
  ```
**2. 반환형 없고, 매개변수 있는 형 - 동적인 일**
```java
      public void typeB(int i, char c){

      }
      호출) 객체명.typeB(1,'C');
      //호출할 때에는 method의 매개변수 개수와 데이터형을 일치시켜야함
```

**3. 반환형 있고, 매개변수 없는 형 - 고정 값**
```java
      public int typeC(){

        return 30; // 값을 반환해
      }
      호출) int i = 객체명.typeC();
      //변수에 할당하거나, 연산에 참여 시킬 수 있다.
```
**4. 반환형 있고, 매개변수 있는 형 - 가변 값**
```java
      public int typeD(char c){

          return (int)c;
      }
      호출)int value = 객체명.typeD('C');
      //데이터형 변수명 = 객체명.method명(값);
      //변수에 할당하거나, 연산에 참여 시킬 수 있다.
```
## Variable Argumetns (가변인자형)
> method 호출할 때 입력하는 값을 동적으로 넣어줄 때
- JavaSE JDK 1.5에서부터 지원되는 문법
- parameter를 정의할 때 **"데이터형 ... 매개변수명"** 의 형식을 가진다
-  method안에서는 배열로 처리된다.
  - 대표: System.out.printf();, System.out.format();
- method가 여러 개의 parameter를 정의할 때 가변인자형은 가장 마지막에만 사용할 수있다.

**형식**
```java
    접근지정자 반환형 method명(데이터형 ... 매개변수명)
```
**호출**
```java
    method명();
    method명(값);
    method명(값,값,,,);
```

```java
public void va(int ... parami){
  // ...parami 매개변수는 배열로 처리된다.
  // (반복문을 사용하여 처음부터 끝까지 모든 값을 얻을 수 있다.)

  for(int value : parami){
    value // 입력된 모든 arguments를 사용 할 수 있다.
  }

   - 호출) va();    // arguments 없이 호출가능.
          va(10); // argumetns 하나를 넣어 호출 가능
          va(10,20,30,40); //arguments 여러개를 넣어 호출 가능
  
}
```


# 생성자 정의하는 방법

## Constructor(생성자)
> 객체가 생성 될 때 가지고 있어야 할 초기화 값, 코드를 정의하는 method의 일종

- 생성자는 `상속되지 않는다.`
- 생성자는 `직접 호출 할 수 없다.`
- 생성자는 `클래스의 이름과 동일`하게 `작성`한다.
- 생성자안에서 다른 생성자를 `this( )` 나 `super( )`로 호출 할 수 있다. 
- `new 키워드로만 호출 가능`.
    -(객체 생성시에만 호출 가능)
- 개발자가 생성자를 하나도 정의하지 않으면 Compiler가 매개변수 없는 `기본 생성자(Default Constructor)`를 `생성`해준다. 
    - 개발자가 생성자를 하나라도 정의하면 Compiler는 기본 생성자를 만들지 않는다.

**Constructor(생성자) 작성법**
```
    접근지정자 클래스명(매개변수){
        객체가 가져야할 초기화 값
        객체가 생성되면서 실행 되어야할 코드
    }
```
**Constructor(생성자) 접근 지정자**
|Constructor(생성자)|접근지정자|
|:----|:----|
|public|클래스 외부에서 객체 생성가능|
|protected|같은 패키지의 다른 클래스에서는 객체 생성가능 / 다른 패키지에서는 상속관계의 자식 클래스에서만 객체생성 가능?|
|private|클래스안에서만 객체생성가능(Singleton Pattern으로 객체를 생성 할때)|
|default|같은 패키지의 다른 클래스에서 객체 생성 가능 / 다른 패키지에서는 객체생성 불가능|

# **this 키워드 이해하기**

## **this**
> 자신클래스와 관련된 일만 수행
- **keyword형식** , **method형식** 두 가지로 사용할 수 있다.

- method 형식: 자신 클래스의 생성자를 호출 할 때 사용
  - this(); - 기본 생성자를 호출 할때 사용
  - this(값); - 매개변수 있는 생성자를 호출 할 때 사용
**주의**
- **생성자의 첫 줄에서만 사용 할 수 있다.**
- 아래 코드와 같이 재귀호출되는 상황이라면 에러발생

## **this keyword사용**
```java
    class Test{
        int i;
        
        public void setI(int i){
                this.i=i; // heap에 i에  stack에 i를 할당
                //this는 method를 호출한 객체의 주소로 바뀐다.
        }

        public static void main(String[] args){
                Test t = new Test();
                t.setI(1000);
        }//main
    }//class
```
  
## **잘못된 this() 재귀호출 오류 상황1**
```java
    public Test(){
      this();
    //재귀호출되는 상황이라면 에러발생
    }
```
## **잘못된 this()오류 상황2**
```java
    class Test{
        public Test() {
            this(10);
        }
        
        public Test(int i) {
            this();
        }
    }
    /*오류 설명
        Test(int i)의 i를 통해 매개변수 값이 들어 왔다고 가정했을 때
        this()를 실행 즉 Test()생성자를 실행하고 this(10)은 다시 Test(int i)를 실행
        계속 상황이 반복 한쪽은 탈출구가 있어야한다.
```