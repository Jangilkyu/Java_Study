# 목표
자바가 제공하는 다양한 연산자를 학습하세요.

# 학습할 것
- 산술 연산자
- 비트 연산자
- 관계 연산자
- 논리 연산자
- instanceof
- assignment(=) operator
- 화살표(->) 연산자
- 3항 연산자
- 연산자 우선 순위
- (optional) Java 13. switch 연산자

# 연산자
 연산자는 **연산을 수행하는 기호**를 말한다.
 - **+** : 덧셈연산자
 - **-** : 뺄셈연산자
 - **/** : 나눗셈연산자
 -  *: 곱셈연산자

# 산술 연산자
산술 연산자는 수학적인 계산을 하기 위해 쓰는 기호이다.

|산술연산자|연산자|의미|
|----|----|----|
||+|더하기|
||-|빼기|
||*|곱하기|
||/|나누기|
||%|나눈 나머지 값|

```java
public class Operator {
    public static void main(String[] args) {

        int num1 = 10;
        int num2 = 6;

        System.out.println(num1 + "+" + num2 + "=" + (num1+num2));
        System.out.println(num1 + "-" + num2 + "=" + (num1-num2));
        System.out.println(num1 + "*" + num2 + "=" + (num1*num2));
        System.out.println(num1 + "/" + num2 + "=" + (num1/num2));
        System.out.println(num1 + "%" + num2 + "=" + (num1%num2));
    }//main
}//class
```

**결과**

<img src ="https://user-images.githubusercontent.com/69107255/100467269-875c9d00-3115-11eb-828e-1991d836e035.png">

# 비트 연산자
## | (OR연산자)
> 피연산자 중 한쪽의 값이 1이면, 1을 결과로 얻고, 그 외에는 0을 얻는다.

|x|y|result|
|:-:|:-:|:-:|
|1|1|1|
|1|0|1|
|0|1|1|
|0|0|0|

```java
		i = 17;
		j = 13;
		
		System.out.println(i + "|" + j + "=" + (i|j));
		// 0001 0001 | 0000 1101 = 0001 1101
```
**결과**

<img src ="https://user-images.githubusercontent.com/69107255/100476222-5e91d300-3128-11eb-8429-8894de015939.png">

---

## & (AND연산자)
> 피연산자 양 쪽이 모두 1이어야만 1을 결과로 얻고, 그 외에는 0을 얻는다.

|x|y|result|
|:-:|:-:|:-:|
|1|1|1|
|1|0|0|
|0|1|0|
|0|0|0|

```java
		int i = 20;
		int j = 19;
		System.out.println(i + "&" + "=" + (i & j));
		// 0001 0100 & 0001 0011 = 0001 0000
```
**결과**

<img src = "https://user-images.githubusercontent.com/69107255/100476182-47eb7c00-3128-11eb-90bf-1a8333076ba9.png">

---

## ^ (XOR연산자)
> 피연산자의 값이 서로 다를 때만 1을 결과로 얻고, 같을 때는 0을 얻는다.

|x|y|result|
|:-:|:-:|:-:|
|1|1|0|
|1|0|1|
|0|1|1|
|0|0|0|

```java
		i = 17;
		j = 13;
    	System.out.println(i + "^" + j + "=" + (i^j));
		// 0001 0001 ^ 0000 1101 = 0001 1100
```
**결과**

<img src ="https://user-images.githubusercontent.com/69107255/100476275-7a957480-3128-11eb-866f-281af8662517.png">

---

```java
public class Operator {
    public static void main(String[] args) {

		System.out.println("--------비트논리----------");
		
		int i = 20;
		int j = 19;
		System.out.println(i + "&" + "=" + (i & j));
		// 0001 0100 & 0001 0011 = 0001 0000
		
		i = 17;
		j = 13;
		
		System.out.println(i + "|" + j + "=" + (i|j));
		// 0001 0001 | 0000 1101 = 0001 1101
		
		System.out.println(i + "^" + j + "=" + (i^j));
		// 0001 0001 ^ 0000 1101 = 0001 1100

    }//main
}//class
```

**결과**

<img src = "https://user-images.githubusercontent.com/69107255/100467397-b96dff00-3115-11eb-9c24-edf97a03ad14.png">

---

## 시프트 연산

1. << : left shift
><< : 비트를 왼쪽으로 밀고, 밀어서 빈칸을 항상 0으로 채운다.
2. `>>` : right shift
>`>>` :  비트를 오른쪽으로 밀고, 밀어서 빈칸을 최상위 부호비트에 따라 0또는 1을 채운다.
3. `>>>` : unsigned right shift
>`>>>` : 비트를 오른쪽으로 밀고, 밀어서 빈칸을 항상 0으로 채운다.

```java
public class Operator {
    public static void main(String[] args) {

        System.out.println("--------시프트 연산----------");
		
        int i = 30;
		
		System.out.println(i + "<< = " + (i << 2));
		// 0001 1110 << 2 = 0111 1000
		
		i = 128;
		System.out.println(i + ">> 3 =" + (i >>3));
		// 1000 0000 >> 3 = 0001 0000
	
		i = 96;
		System.out.println(i + ">>> 4 = " + (i >>> 4));	
		// 0110 0000 >>> 4 = 0000 0110
		
		i = 1;
		System.out.println(i + "<< 31 = " + (i << 31) );
		//  0000 0000 0000 0000 0000 0000 0000 0000 << 1
		//= 1000 0000 0000 0000 0000 0000 0000 0000

		i = -1;
		System.out.println(i + ">> 10 = " + (i >> 10) );
		// 1111 1111 1111 1111 1111 1111 1111 1111 >> 10
		
		i = -1;
		System.out.println(i + ">>> =" + (i >>> 1));
		// 0111 1111 1111 1111 1111 1111 1111 1111 >>> 1

    }//main
}//class
```

**결과**

<img src = "https://user-images.githubusercontent.com/69107255/100467569-081b9900-3116-11eb-9b09-c871c8c5d15c.png">

---

## 비트 전환 연산자 ~
> 비트 전환 연산자는 2진수로 표현했을 때, 0은 1로 1은 0으로 바꾼다.

|x|~x|
|-|-|
|1|0|
|0|1|


# 관계 연산자
- 두 피연산자 관계를 비교하여 boolean값인 참(true)와 거짓(false)로 반환한다.

```java
public class Operator {
    public static void main(String[] args) {

        System.out.println("--------관계 연산----------");
		
		int i = 10, j = 26, k = 10;
		
		System.out.println(i+ " == " + k + "=>" + (i == k)); // 같다면 ture
		System.out.println(i+ " == " + j + "=>" + (i == j)); // 같지 않다면 false
		
		System.out.println(i+ " != " + k + "=>" + (i != k)); // 같다면 false
		System.out.println(i+ " != " + j + "=>" + (i != j)); // 같지 않다면 true

    }//main
}//class
```


# 논리 연산자

## 일반 논리 
> 여러 개의 관계연산자를 묶어서 비교할 때 사용 

##  &&(AND)
- &&: 전항이 ture이고 후항이 ture일 때 ture반환

```java
public class Operator {
    public static void main(String[] args) {

		boolean flag1 = true, flag2=false, flag3=true, flag4=false;
		System.out.println((10 < 26) && (10 > 5));
		System.out.println("---------&&---------");
		//전항이 false이면, 후항에 상관없이 false가 나오기 때문에 후항을 계산하지 않는다.
		System.out.println(flag1 + "&&" + flag3 + "=" + (flag1 && flag3));//true
		System.out.println(flag1 + "&&" + flag2 + "=" + (flag1 && flag2));//false
		System.out.println(flag2 + "&&" + flag3 + "=" + (flag2 && flag3));//false
		System.out.println(flag2 + "&&" + flag4 + "=" + (flag2 && flag4));//false

    }//main
}//class
```

<img src = "https://user-images.githubusercontent.com/69107255/100474016-05737080-3123-11eb-8739-72e4bed4e2e6.png">

```java
public class Operator {
    public static void main(String[] args) {

        boolean flag1, flag2, flag3;

        flag1=true; //전항저장
        flag2=true; //후항저장
        flag3=true; //연산결과

        //전항이 false라면 후항을 계산하지 않아 후항을 저장한 flag2변수에는 true가 그대로 들어가 있다.
        flag3 = (flag1=3<2) && (flag2 = 4 > 5);
        System.out.println("전항:" + flag1 + ",후항:" + flag2 + ", 연산결과:" + flag3 );
        System.out.println();
    }//main
}//class
```
<img src = "https://user-images.githubusercontent.com/69107255/100474461-ff31c400-3123-11eb-8171-6c198bc39659.png">

---

## ||(OR)
- ||: 전항이 false이고, 후항이 false일 때만 false반환

```java
public class Operator {
    public static void main(String[] args) {

        boolean flag1 = true, flag2=false, flag3=true, flag4=false;
        
        System.out.println("---------||---------");
        //전항이 true이면 후항에 상관없이true가 나오기 때문에 후항을 계산하지 않는다.
        System.out.println(flag1 + "||" + flag3 + "=" + (flag1 || flag3));//true
        System.out.println(flag1 + "||" + flag2 + "=" + (flag1 || flag2));//true
        System.out.println(flag2 + "||" + flag3 + "=" + (flag2 || flag3));//true
        System.out.println(flag2 + "||" + flag4 + "=" + (flag2 || flag4));//false
    }//main
}//class
```

<img src = "https://user-images.githubusercontent.com/69107255/100474117-3d7ab380-3123-11eb-89de-7fea7d9be9af.png">

# instanceof
instanceof 연산자는 객체 타입을 비교하는데 사용하는 연산자이다.
- 왼쪽이 오른쪽에 오는 클래스의 객체이거나 하위 클래스의 객체일 경우 true를 반환하고, 그렇지 않을 경우 false를 반환한다.

```java
    String Hello = "Hello";
    System.out.println(Hello instanceof String); 
    // String 변수 Hello는 String클래스 객체이므로 true를 반환한다.
```

```java
class Parent{

}//class

class Child extends Parent{

}//class

    public class UseInstanceof {

        public static void main(String[] args) {

            Parent p = new Parent();
            Child c = new Child();

            System.out.println(p instanceof Parent); //true

            System.out.println(c instanceof Parent); //true

            System.out.println(p instanceof Child); //false

            System.out.println(c instanceof Child); //treu

        }//main
    }//class
```

# assignment(=) operator
> 대상체의 값을 변경한다.

## 순수대입: =
```java
        int i = 3; //순수 대입
```

## 산술대입: +=, -=, *=, %=
```java
        //산술 대입
        i += 3; // i = i + 3;
        i -= 2; // i = i - 2;
        i *= 3; // i = i * 3;
        i /= 5; // i = i / 5;
        i %= 3; // i = i % 3;
```

## 쉬프트 대입: <<=, >>=, >>>=

```java
        // 쉬프트 대입
        i <<=  4; // i = i <<4; //0000 0010 << 4 = 0010 0000
        i >>= 2; //  i =>> 2;  //0010 0000 >> 2 = 0000 1000
        i >>>= 3; // i = i >>> 3; // 0000 1000 >>> 3 = 0000 0001
```

## 비트논리대입: &=, |=, ^=

```java
        //비트 논리대입
        i &= 15; // i = i & 15; // 0000 0001 & 0000 1111 = 0000 0001
        i |= 9; // i= i|9; // 0000 0001 | 0000 1001 = 0000 1001
        i ^= 6; // i = i ^6; // 0000 1001 ^ 0000 0110 = 0000 1111
```

# 화살표(->) 연산자
> 람다 표현식(lambda expression)이란 간단히 말해 **메소드를 하나의 식**으로 표현한 것

**메소드**
```java
    int min(int x, int y) {

        return x < y ? x : y;

    }
```

**람다 표현식**
```java
    (x, y) -> x < y ? x : y;
```
- 출처  [링크](http://www.tcpschool.com/java/java_lambda_concept)

# 3항 연산자
> 조건식 ? 항1 : 항2
- 조건이 true 이면 항1 값을 반환, 조건이 false 이면 항2의 값을 반환하는 연산자

```java
		int i = 10;
		// i변수에 존재하는 수가 "양수"인지 "음수"인지를 출력하는 코드
		System.out.println(i + "은(는) " + (i >= 0 ? "양수" : "음수"));

		//i변수에 존재하는 수가 "짝수"인지 "홀수"인지를 출력하는 코드
		System.out.println(i +"은(는) " + (i%2==0 ? "짝수" : "홀수"));
```


# 연산자 우선 순위
<img src = "https://user-images.githubusercontent.com/69107255/100477577-01981c00-312c-11eb-9a17-4383701e1e22.png">

출처 [링크](https://jeong-pro.tistory.com/138)

# (optional) Java 13. switch 연산자

- `break`키워드 대신에 `yield`키워드를 사용해서 리턴할 수 있다.
- `->`를 사용하여 case 구문 처리가 가능

```java
     String day = "6";
     
    int value  = switch (day){
        case "1" -> 1;
        case "2" -> 2;
        case "3","4","5" -> 3;
        case "6" -> {
            yield 4;
        }
        default ->  5;
    };

        System.out.println(value); //6
```