# 목표
- 자바의 Input과 Ontput에 대해 학습하세요.
# 학습할 것 (필수)
- 스트림 (Stream) / 버퍼 (Buffer) / 채널 (Channel) 기반의 I/O
- InputStream과 OutputStream
- Byte와 Character 스트림
- 표준 스트림 (System.in, System.out, System.err)
- 파일 읽고 쓰기

<hr>

# 1. 스트림 (Stream) / 버퍼 (Buffer) / 채널 (Channel) 기반의 I/O

## IO(Input / Output)Stream
- JVM외부에 존재하는 데이터를 JVM내부로 읽어 들이거나,JVM내부의 데이터를 JVM외부로 내보낼 때 사용하는 객체들
- java.io 패키지에서 관련 클래스를 제공한다.

## 1.1 Stream
키보드,모니터의 입출력,프로그램과 외부 장치,파일의 입출력에서 데이터 흐름도 스트림이 될 수가 있다.
단일 방향으로 연속적으로 흘러간다. 단방향이기 때문에 입력과 출력을 동시에 처리할 수 없다.
입력과 출력을 동시에 처리하고 싶다면 **입력 스트림**과 **출력 스트림**을 각각 만들어서 처리해야한다.
FIFO(Fist In First Out)선입선출 구조이기 때문에 순차적으로 흘러가고 순차적으로 접근이 가능하다.

## 1.2 Buffer
일상으로 치면 하루에 할 수 있는 일이 10개가 있다고 가정하면 내 버퍼가 10개가 최대치인데 4개가 추가적으로 들어온다면 1,2,3,4를 처리하고 11,12,13,14는 대기한다. 
즉,전달하는 데이터를 Buffer의 크기만큼 보관하고 한번에 전송한다. 전달하는 데이터의 크기가 Buffer의 크기보다 크다면 나머지 데이터들은 대기한다.
그렇지만, Buffer가 안찬 상태여도 강제(flush)로 보낼 수 있다.

## 1.3 채널
양방향으로 데이터 전송이 가능하다.


# 2. InputStream과 OutputStream

## 2.1 InputStream
|메서드|설명|
|----|----|
|read()|입력 스트림으로부터 1바이트를 읽어서 바이트를 리턴|
|read(byte[] b)|입력 스트림으로부터 읽은 바이트들을 매개값으로 주어진 바이트 배열 b 에 저장하고 실제로 읽은 바이트 수를 리턴|
|read(byte[] b, int off, int len)|입력 스트림으로부터 len 개의 바이트만큼 읽고 매개값으로 주어진 바이트 배열 b[off] 부터 len 개까지 저장. 그리고 실제로 읽은 바이트 수인 len 개를 리턴. 만약 len 개를 모두 읽지 못하면 실제로 읽은 바이트 수를 리턴|
|close()|사용한 시스템 자원을 반납하고 입력 스트림 닫기|

## 2.2 OutputStream

|메서드|설명|
|----|----|
|write(int b)|출력 스트림으로부터 1바이트를 보낸다.|
|write(byte[] b)|출력 스트림으로부터 주어진 바이트 배열 b의 모든 바이트를 보낸다.|
|write(byte[ ] b, int off, int len)|출력 스트림으로 주어진 바이트 배열 b[off] 부터 len 개까지의 바이트를 보낸다.|
|flush()|	버퍼에 잔류하는 모든 바이트를 출력한다.|
|close()|	사용한 시스템 자원을 반납하고 입력 스트림 닫기|

# 3. Byte와 Character 스트림

## 3.1 Byte 스트림
- 1Byte로 처리한다.

|입력|출력|설명|
|----|----|----|
|FileInputStream|FileOutputStream|파일|
|FilterInputStream|FilterOutputStream|필터를 이용해서 입출력 처리|
|CharArrayInputStream|CharArrayOutputStream|메모리|
|ObjectInputStream|ObjectOutputStream|데이터를 객체 단위로 읽고 사용<br>객체 직렬화와 관련있음|
|SequenceInputStream|없음|두 개의 스트림을 하나로 연결|
|LineNumberInputStream|없음|읽어 온 데이터의 라인 번호를 카운트|
|BufferedInputStream|BufferedOutputStream|버퍼를 이용해서 입출력 성능 향상|
|없음|PrintStream|버퍼를 이용하여 추가적인 print 관련 기능이 있음|
|PushbackInputStream|없음|버퍼를 이용해서 읽어온 데이터를 다시 되돌리는 기능이 있음|


## 3.2 Character 스트림
- 2Byte로 처리를 한다.
- 유니코드간의 변환을 자동적으로 처리해 준다.


|바이트기반 스트림|문자기반 스트림|설명|
|----|----|----|
|FileInputStream|FileReader<br>FileWriter|파일|
|FilterInputStream|FilterReader|필터를 이용해서 입출력 처리|
|CharArrayWriter|CharArrayReader|메모리|
|LinNumberInputStream|LineNumberReader|행 번호를 추적해 관리하는 버퍼링 된 문자 입력|
|BufferedWriter|BufferedReader|버퍼를 이용해서 입출력 향상|
|PrintStream|PrintWriter|버퍼를 이용하여 추가적인 print 관련 기능이 있음|
|PushbackInputStream|PushbackReader|버퍼를 이용해서 읽어온 데이터를 다시 되돌리는 기능이 있음|

# 4. 표준 스트림 (System.in, System.out, System.err)
- in,out,err은 모두 정적 변수이기 때문에 System클래스를 생성하지 않고도 사용이 가능하다.

System 클래스
|클래스 변수|입출력 스트림|설명|
|----|----|----|
|System.in|InputStream|표준 입력 스트림 키보드로 입력을 받는다.|
|System.out|PrintStream|표준 출력 스트림 화면에 데이터 출력|
|System.err|PrintStream|표준 에러 출력 스트림|


# 5. 파일 읽고 쓰기

## 5.1 파일 읽기

```java
    Reader reader = new BufferedReader(new FileReader("c:/java/a.txt"));
    
    BufferedReader bufReader = new BufferedReader(reader);
    
    String line = "";
    while((line = bufReader.readLine()) != null){
        System.out.println(line);
    }
    
    bufReader.close();
```

## 5.2 파일 쓰기
```java
    File file = new File("./Writer.txt");
    
    FileWriter fileWriter = new FileWriter(file);
    
    BufferedWriter bufferedWriter = new BufferedWriter(fileWriter);

    if(file.isFile() && file.canWrite()){
        
        bufferedWriter.write("안녕하세요");

        bufferedWriter.newLine();
        
        bufferedWriter.close();
    }
```

# 참고자료
[InputStream과 OutputStream](https://coding-factory.tistory.com/281)