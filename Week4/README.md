# 제어문
> 프로그램의 순차적인 흐름을 변경하는 문장들

# 조건문
- if문
- if ~ else문
- switch~case문

# 단일 if
> 조건에 맞을 경우에만 코드를 실행해야 할 때

**단일 if 문법**
```java
         if(조건식) {
            조건에 맞을 경우 실행되어야 할 코드들..
    }
```
**단일 if 예시 코드**
```java 
		int i = 27;
		
		if(i < 0) {
			i = -i;
		}// end if
		
		System.out.println("i는 " + i);
		
		System.out.println("------------------------------------");
		
		if( (i >= 0) && (i<=100)) {
			System.out.println(i);
		}//end if
		
		System.out.println("감사합니다.");
```
**결과**

<img src = "https://user-images.githubusercontent.com/69107255/101969185-6d1ed500-3c66-11eb-9308-c23d71a680aa.png">

# if~else문
> 둘 중 하나의 코드가 반드시 실행 되어야할 때

**if~else문 문법**
```java
	문법:
		if(조건식) {
			조건에 맞을 때 실행될 문장들...
		}
		else {
			조건에 맞지 않을 때 실행 될 문장들...
		}
```
**if~else문 예시 코드**
```java
        //입력되는 두번째 arguments는 나이입니다. 입력된 나이를 사용하여 "성년"인지 "미성년"인지를 출력하는 코드 작성
        // 성년 판정 19살 이상 이다.

        int age = 20;

        System.out.print("입력나이 " + age + "살은");

        if(age > 18) {
            System.out.println("성년");
        }
        else {
            System.out.println("미성년");
        }
```
**결과**

<img src = "https://user-images.githubusercontent.com/69107255/101969283-ed453a80-3c66-11eb-9461-3194dfee9b68.png">

# 다중if 문(else~if)
> 연관성있는 여러 조건을 비교해야 할 때

```java
    문법:
        if(조건식) {
            조건에 맞을 수행 문장들...
        }
        else if(조건식) {
            조건에 맞을 때 수행 문장들...
        }
        else if(조건식) {
            조건에 맞을 때 수행 문장들..
        }
       else {
           모든 조건에 맞지 않을 때 수행 문장들...
       } 
```

```java
		/*
		 	자격시험 점수 score 변수에 들어있다.
		 	자격시험 점수의 판정
		  	과락: 0 ~40
		  	다른 과목점수 참조 : 41 ~ 60
		  	합격: 61 ~ 100
		 */

        int score = 84;

        if(score <= 40 && score >= 0) {
            System.out.println("과락");
        }
        else if(score > 40 && score < 61) {
            System.out.println("다른 과목점수 참조");
        }
        else if(score > 60 && score <= 100){
            System.out.println("합격");
        }
        else {
            System.out.println("잘못된 점수 입력");
        }
```
**결과**

<img src = "https://user-images.githubusercontent.com/69107255/101969340-38f7e400-3c67-11eb-8c9b-f1a364b88350.png">

# switch~case

> 일치하는 정수를 비교할 때 사용

**switch~case 문법**
```java
    문법:
        switch(변수명) { //비교 가능 타입: byte,short,int,char, String(JDK1.7부터 사용가능)

            case 상수: 변수의 값이 상수와 같을 때 수행 문장들...
            case 상수: 변수의 값이 상수와 같을 때 수행 문장들...
            case 상수: 변수의 값이 상수와 같을 때 수행 문장들...
            .
            .
            .
            default: 변수의 값에 해당하는 case가 없을 때 수행문장들..
        }
```

**switch~case 예시 코드**
```java
		int i = 1; //비교 가능 타입: byte,short,int,char, String(JDK1.7부터 사용가능)
		//case의 상수는 비교용도이기 때문에 위의 case와 인접상수(0,1,2,3)가 아니어도 된다.
		//가급적이면 인접상수로 case 작성한다. (비교 속도 향상)
		switch(i) {
			case 0: System.out.println("A"); break;
			case 1: System.out.println("B"); break;
			case 2: System.out.println("C"); 
			default: System.out.println("Z"); break;
		}//end switch
```

# 반복문 
> 코드의 실행을 여러 번 하기 위해서 제공되는 문장

# 단일 for
> 시작과 끝을 알 때 사용하는 반복문

**for문법**
```java
    for(초기화식 ; 조건식; 증,감소식) {
        반복수행 할 문장들.....
    }
```

```java
		for(int i = 0; i < 10; i++) {
			System.out.println(i);
		}
```

<img src = "https://user-images.githubusercontent.com/69107255/101969658-f800cf00-3c68-11eb-9fb6-0c739cfae939.png">

# 다중 for
> for문안에 for문 정의
- 바깥 for가 한번 실행 될 때 안쪽 for는 몇번 실행되는지 생각

**다중 for 예시코드**
```java
		for(int i = 0; i < 4; i++) {
			for(int j = 0; j <= i; j++) {
				System.out.print(i + " " + j + " ");
			}
			System.out.println();
		}		
```

**결과**

<img src = "https://user-images.githubusercontent.com/69107255/101969801-ce947300-3c69-11eb-9639-fc1f9b04bd13.png">


# for~each
> 인덱스를 사용할 수 없다.

**특징**
- Java SE5(JDK1.5)에서부터 지원하는 문법
- 배열, Collection(List,Set)의 처음 방부터 끝방까지 출력하는 일을 함
- 기존의 for보다 처리되는 속도가 느림

```java
    for(데이터형 변수명 : 배열명){ 
                    //배열명에는 List명,Set명이 올수도 있음
    }
```

# while문
> 최소 0번 수행에 최대 조건까지 수행

```java
    //초기값
    while(조건식){ 
        //조건식에는 관계연산자, 일을 하는 method가 들어갈 수 있다.
        반복 수행문장;
        //증,감소식
    }

    //초기값과 증,감소식이 들어가면 for의 형태다
```
# do~while문
> 시작과 끝을 알 수 없을 때 사용
- 최소 1번 수행에 최대 조건까지 수행

**do~while 문법**

```java
    //초기값;
    do{
        반복수행 문장들;
        증,감소식;
    }while(조건식);

//조건식의 결과가 true이면 do로 올라가서 실행
//조건식이 false이면 해당 do~while문 탈출
```

# 무한 loop (infinite loop)

**특징**
- 끝나지 않는 프로그램을 만들어야 할 때
- 무한 loop 코드 아래줄에 코드가 작성되어 있으면 error가 발생

- 무한 loop 사용 사례
  - OS, 시계, 서버

```java
    EX1)
    for( ; ; ){

    }
    // 초기식,조건식,증,감소식을 작성하지 않을 때
    // 증가하는 값을 알수 없다

----------------------------------------------------------------------------
    
    EX2)
    for(초기값;  ;증,감소식){

    }
    //조건식만 생략하여 작성 할 때
    //증가하는 값을 알 수 있다. 

    EX)
    while(true){

    }
    //조건식을 참으로 작성하여 빠져나올 수 없다.
```

# break;
> switch-case, for, while, do~while문에서 실행을 멈추고 빠져 나갈 때 사용

# continue;
> 반복문의 수행을 건너 뛸 때 사용

**특징**
- continue를 반복문의 제일 마지막줄에 기술하지 않는다.
- 조건식에 넣어서 사용

**continue 예시 코드**
```java
		for(int i = 1; i < 101; i++) {
			if(i%2== 1) {
				continue;
			}
			System.out.println(i + " ");
```

**결과**
1에서부터 100까지 짝수만 출력된다.
