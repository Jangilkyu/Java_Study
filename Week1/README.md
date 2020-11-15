# 1주차 과제: JVM은 무엇이며 자바 코드는 어떻게 실행하는 것인가.

## 목표
자바 소스 파일(.java)을 JVM으로 실행하는 과정 이해하기.

## 학습할 것
- JVM이란 무엇인가
- 컴파일 하는 방법
- 실행하는 방법
- 바이트코드란 무엇인가
- JIT 컴파일러란 무엇이며 어떻게 동작하는지
- JVM 구성 요소
- JDK와 JRE의 차이
---

## JVM이란 무엇인가
`JVM`은 `Java virtual machine`을 줄인 것으로 직역하면 `자바를 실행하기 위한 가상기계`라고 할 수 있다<br>
자바로 작성된 애플리케이션은 모두 이 가상 컴퓨터(JVM)에서만 실행되기 때문에, 자바 애플리케이션이 실행되기 위해서는 반드시 JVM이 필요하다.

`Write once, run anywhere(한 번 작성하면 어디서든 실행된다.`

<img src = "https://user-images.githubusercontent.com/69107255/99010080-9e838280-258c-11eb-8a2d-c66aec795f8a.png" width="400">

**출처** [javatutorial](https://javatutorial.net/jvm-explained)

## 컴파일 하는 방법

1. **source code 작성**

    - 파일명.java로 저장한다. `파일명`과`class명`은 동일하게 설정한다. 
    - 대,소문자를 구분한다.

<img src = "https://user-images.githubusercontent.com/69107255/99038592-15d70780-25c9-11eb-908e-57364c232289.JPG" width="600">

2. **저장**

`파일명.java`

3. **컴파일**
> javac -옵션 소스파일명.java

- java.exe를 통하여 컴파일을 수행한다.
- 사람의 언어를 컴퓨터 언어로 번역
- DOS창을 열고 `Hello.java`가 있는 위치에서 수행
- 컴파일 성공 시 `Hello.class` `바이트코드`가 생성
<img src="https://user-images.githubusercontent.com/69107255/99179976-a0546e00-2765-11eb-9a3e-484720ebfbc7.jpg">

<img src="https://user-images.githubusercontent.com/69107255/99179812-5919ad80-2764-11eb-96df-279ff74eada3.jpg">

## 실행하는 방법 

4. **실행**
> java -옵션 bytecode명
- java.exe.실행 시 JVM이 만들어진다.
- JVM이 실행되고 class가 적재(load)되어 클래스에 내용이 실행됨
<img src="https://user-images.githubusercontent.com/69107255/99180075-9c751b80-2766-11eb-933e-7bd85b0cdaa1.png">

## 바이트코드란 무엇인가
- `바이트코드`란 `JVM(자바가상기계)`이 이해 할 수 있는 언어로 변환 된 `자바 소스코드`이다.

<img src= "https://user-images.githubusercontent.com/69107255/99180297-69cc2280-2768-11eb-9355-60b3f296a831.jpg">

- `.class`확장자를 가진다.
- `자바 바이트코드`는 `JVM(자바가상기계)`만 설치가 되어있으면, 어떤 OS(운영체제)에서도 실행이 가능하다.

## JIT 컴파일러란 무엇이며 어떻게 동작하는지
> JIT 컴파일러는 `Just-In-Time`의 약자이다.
 
- 소스코드를 `Compile`하면 `ByteCode`로 변환이 된다. 
- `.class`로 만들어진 `ByteCode`는 기계가 바로 읽을 수 없는 형태이다.
- 바이트 코드는 실제 실행될 때 다시 한번 `기계가 읽을 수 있는 형태(native code)`로 `interpreter`를 통해 해석 되어야한다.
- JVM이 bytecode를 기계어로 interpret할때 `반복되는 내용은 컴파일`을 해서 사용한다.
- JIT컴파일링은 실행될 때 최초 실행되기 때문에, 최초실행에서는 느릴 수 있다.

**참고 사이트**[https://aroundck.tistory.com/1949](https://aroundck.tistory.com/1949)

## JVM 구성 요소
1. **Class Loader**
- `.java`파일을 javac로 컴파일하면 `바이트코드(.class)`가 나오는데 이 파일을 런타임에(동적으로)메모리로 올려서 실행하는 부분이다.

2. **Execution Engine**
- Class Loader에 의해 메모리에 적재된 바이트코드를 기계어로 변경해 `명령어 단위(operation code)`로 실행하는 것을 말한다.
  - 인터프리터: 명령어를 하나씩 수행
  - JIT(Just In Time): 전체 바이트 코드를 네이티브 코드로 변환하고 그 이후에는 인터프리팅하지 않고 네이티브 코드 상태로 실행

1. **Garbage Collector**
- Heap 메모리 영역에 생성된 객체들 중에 참조되지 않은 객체들을 제거하는 역할을 한다.

4. **Runtime Date Area**
- JVM의 메모리 영역으로 자바 애플리케이션 실행 시 사용되는 데이터를 적재하는 영역이다.
  - 크게 `Method Area` `Heap Area` `Stack Area` `PC register` `Native Method Stack` 5가지 영역으로 구분된다. 

<img src= "https://user-images.githubusercontent.com/69107255/99182260-4a88c180-2777-11eb-9c1f-7d50c61761c8.png" width="500">

**출처:**[JVM의 구조](https://velog.io/@hono2030/JVM%EC%9D%98-%EA%B5%AC%EC%A1%B0)

## JDK와 JRE의 차이
- JDK(Java Development Kit): **자바개발도구**는 JRE + 개발을 위해  필요한 도구(javac,java)등을 포함한다.
- JRE(Java Runtime Environment): **자바 실행환경**은  JVM이 자바 프로그램을 동작시킬 때 필요한 라이브러리 파일들과 기타 파일들을 가지고 있다.