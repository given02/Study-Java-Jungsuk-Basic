# 9. java.lang패키지와 유용한 클래스

## Object클래스

- 모든 클래스의 최고 조상. 오직 11개의 메서드만을 가지고 있다.
- notify(), wait() 등은 쓰레드와 관련된 메서드이다.
- protected Object clone() : 객체 자신의 복사본을 반환한다.
- public boolean equals(Object obj) : 객체 자신과 객체 obj가 같은 객체인지 알려준다.(같으면 true)
- protected void finalize() : 객체가 소멸될 때 가비지 컬렉터에 의해 자동적으로 호출된다. 이 때 수행되어야하는 코드가 있을 때 오버라이딩한다.(거의 사용안함)
- public Class getClass() : 객체 자신의 클래스 정보를 담고 있는 Class 인스턴스를 반환한다.
- public int hashCode() : 객체 자신의 해시코드를 반환한다.
- public String toString() : 객체 자신의 정보를 문자열로 반환한다.
- public void notify() : 객체 자신을 사용하려고 기다리는 쓰레드를 하나만 깨운다.
- public void notifyAll() : 객체 자신을 사용하려고 기다리는 모든 쓰레드를 깨운다.
- public void wait(long timeout, int nanos) : 다른 쓰레드가 notify()나 notifyAll()을 호출할 때까지 현재 쓰레드를 무한히 또는 지정된 시간동안 기다리게 한다.(timeout은 천 분의 1초, nanos는 10^9분의 1초)

## equals(Object obj)

- 객체 자신(this)과 주어진 객체(obj)를 비교한다. 같으면 true, 다르면 false
- Object클래스의 equals()는 객체의 주소를 비교(참조변수 값 비교)

## equals(Object obj)의 오버라이딩

- 인스턴스 변수의 값을 비교하도록 equals()를 오버라이딩해야 한다.
  ```java
  class Person {
      long id;
      public boolean equals(Object obj) {
          if(obj instanceof Person)
              return id == ((Person) obj).id;
          else
              return false;
      }
  }
  ```

## String 클래스

- String클래스 : 데이터(char[]) + 메서드(문자열 관련)
- 내용을 변경할 수 없는 불변(immutable) 클래스
- 덧셈 연산자(+)를 이용한 문자열 결합은 성능이 떨어짐.
- 문자열의 결합이나 변경이 잦다면, 내용을 변경가능한 StringBuffer를 사용

## 문자열의 비교

- String str = “abc”;와 String str = new String(”abc”);의 비교
  ```java
  String str1 = "abc";
  String str2 = "abc"; // str1 == str2 ? true (주소가 같기 때문에)
  String str3 = new String("abc");
  String str4 = new String("abc"); // str3 == str4 ? false (주소가 다르기 때문에)
  ```
  - 값 비교 시 String equals를 사용해야함(String은 equals가 내용 비교로 오버라이딩 되어 있다.)

## 문자열 리터럴

- 문자열 리터럴은 프로그램 실행시 자동으로 생성된다.(constant pool에 저장)
- 같은 내용의 문자열 리터럴은 하나만 만들어진다.

## 빈 문자열(””, empty string)

- 내용이 없는 문자열. 크기가 0인 char형 배열을 저장하는 문자열
- 크기가 0인 배열을 생성하는 것은 어느 타입이나 가능
- 문자(char)와 문자열(String)의 초기화

## String클래스의 생성자와 메서드

- String(String s) : 주어진 문자열(s)을 갖는 String 인스턴스를 생성한다. (잘 안씀)
- String(char[] value) : 주어진 문자열(value)을 갖는 String 인스턴스를 생성한다.
  ```java
  char[] c = { 'H', 'e', 'l', 'k', 'o' };
  String s = new String(c);
  ```
- String(StringBuffer buf) : StringBuffer인스턴스가 갖고 있는 문자열과 같은 내용의 String 인스턴스를 생성한다.
- char charAt(int index) : 지정된 위치(index)에 있는 문자를 알려준다.
- int compareTo(String str) : 문자열(str)과 사전순서로 비교한다. 같으면 0, 사전순으로 이전이면 음수, 이후면 양수를 반환다.
- String concat(String str) : 문자열(str)을 뒤에 덧붙인다.
- boolean contains(CharSequence s) : 지정된 문자열(s)이 포함되었는지 검사한다.
- boolean endsWith(String suffix) : 지정된 문자열(suffix)로 끝나는지 건사한다.
- boolean equals(Object obj) : 매개변수로 받은 문자열(obj)과 String 클래스의 문자열을 비교한다. obj가 String이 아니거나 문자열이 다르면 false를 반환한다.
- boolean equalsIgnoreCase(String str) : 문자열과 String인스턴스의 문자열을 대소문자 구분없이 비교한다.
- int indexOf(int ch) : 주어진 문자(ch)가 문자열에 존재하는지 확인하여 위치(index)를 알려준다. 못 찾으면 -1을 반환한다.
- int indexOf(int ch, int pos) : 주어진 문자(ch)가 문자열에 존재하는지 지정된 위치(pos)부터 확인하여 위치(index)를 알려준다. 못 찾으면 -1을 반환한다.
- int indexOf(String str) : 주어진 문자열이 존재하는 지 확인하여 그 위치를 알려준다. 없으면 -1을 반환한다.
- int lastIndexOf(int ch) : 지정된 문자 또는 문자코드를 문자열의 오른쪽 끝에서부터 찾아서 위치를 알려준다. 못찾으면 -1을 반환한다.
- int lastIndexOf(String str) : 지정된 문자열을 인스턴스의 문자열 끝에서 부터 찾아서 위치를 알려준다. 못 찾으면 -1을 반환한다.
- int length() : 문자열의 길이를 알려준다.
- String[] split(String regex) : 문자열을 지정된 분리자(regex)로 나누어 문자열 배열에 담아 반환한다.
- String[] split(String regex, int limit) : 문자열을 지정된 분리자(regex)로 나누어 문자열배열에 담아 반환한다. 단, 문자열 전체를 지정된 수(limit)로 자른다.
- boolean startsWith(String prefix) : 주어진 문자열(prefix)로 시작하는지 검사한다.
- String substring(int begin, int end)) : 주어진 시작위치(begin)부터 끝 위치(end)범위에 포함된 문자열을 얻는다. 이 때, 시작위치의 문자는 범위에 포함되지만, 끝 위치의 문자는 포함되지 않는다.(end 생략 시 자동으로 마지막 문자열까지 반환)
- String toLowerCase() : String 인스턴스에 저장되어있는 모든 문자열을 소문자로 변환하여 반환한다.
- String toUpperCase() : String 인스턴스에 저장되어있는 모든 문자열을 대문자로 변환하여 반환한다.
- String trim() : 문자열의 왼쪽 끝과 오른쪽 끝에 있는 공백을 없앤 결과를 반환한다. 이 때 문자열 중간에 있는 공백은 제거되지 않는다.
- static String valueOf() : 지정된 값을 문자열로 변환하여 반환한다. 참조변수의 경우, toString()을 호출한 결과를 반환한다.
- 코드는 가독성을 최우선으로 작성한다. 이후 성능 문제 되면 그 때 코드 수정

## join()과 StringJoiner

- join()은 여러 문자열 사이에 구분자를 넣어서 결합한다.
- 문자열과 기본형 간의 변환
  - 숫자를 문자열로 바꾸는 방법
    ```java
    int i = 100;
    String str1 = i + "";
    String str2 = String.valueOf(i);
    ```
  - 문자열을 숫자로 바꾸는 방법
    ```java
    int i = Integer.parseInt("100");
    int i2 = Integer.valueOf("100");
    Integer i2 = Integer.valueOf("100");
    ```

## StringBuffer클래스

- String처럼 문자형 배열(char[])을 내부적으로 가지고 있다.
- 그러나, String과 달리 내용을 변경할 수 있다.(mutable)
  ```java
  StringBuffer sb = new StringBuffer("abc");
  sb.append("123"); // sb = abc123
  ```
- 배열은 길이 변경불가. 공간이 부족하면 새로운 배열 생성해야 함
- StringBuffer는 저장할 문자열의 길이를 고려해서 적절한 크기로 생성해야 함
- append()는 지정된 내용을 StringBuffer에 추가 후, StringBuffer의 참조를 반환
- StringBuffer는 equals()가 오버라이딩 되어 있지 않다.(주소비교)
- StringBuffer를 String으로 변환 후에 equals()로 비교해야 한다.

## StringBuffer의 생성자와 메서드

- StringBuffer() : 16문자를 담을 수 있는 버퍼를 가진 StringBuffer 인스턴스를 생성한다.
- StringBuffer(int length) : 지정된 개수의 문자를 담을 수 있는 버퍼를 가진 StringBuffer인스턴스를 생성한다.
- StringBuffer(String str) : 지정된 문자열 값(str)을 갖는 StringBuffer인스턴스를 생성한다.
- StringBuffer append() : 매개변수로 입력된 값을 문자열로 변환하여 StringBuffer인스턴스가 저장하고 있는 문자열의 뒤에 덧붙인다.
- int capacity() : StringBuffer인스턴스의 버퍼크기를 알려준다. (length는 버퍼에 담긴 문자열의 길이를 알려준다.)
- char charAt(int index) : 지정된 위치에 있는 문자를 반환한다.
- StringBuffer delete(int start, int end) : 시작위치부터 끝위치 사이에 있는 문자를 제거한다. 단, 끝 위치의 문자는 제외
- StringBuffer deleteCharAt(int index) : 지정된 위치의 문자를 제거한다.
- StringBuffer insert(int pos, 값) : 두 번째 매개변수로 받은 값을 문자열로 변환하여 지정된 위치(pos)에 추가한다.
- int length() : StringBuffer인스턴스에 저장되어 있는 문자열의 길이를 반환한다.
- StringBuffer replace(int start, int end, String str) : 지정된 범위의 문자들을 주어진 문자열로 바꾼다. end위치의 문자는 범위에 포함 되지 않음
- StringBuffer reverse() : StringBuffer인스턴스에 저장되어 있는 문자열의 순서를 거꾸로 반환한다.
- void setCharAt(int index, char ch) : 지정된 위치의 문자를 주어진 문자(ch)로 바꾼다.
- void setLength(int newLength) : 지정된 길이로 문자열의 길이를 변경한다. 길이를 늘리는 경우에 나머지 빈 공간을 널문자 ‘\u0000’로 채운다.
- String toString() : StringBuffer인스턴스의 문자열을 String으로 반환
- String substring(int start, int end) : 지정된 범위 내의 문자열을 String으로 뽑아서 반환한다. 시작위치만 지정하면 시작위치부터 문자열 끝까지 뽑아서 반환한다.

## StringBuilder

- StringBuffer는 동기화 되어 있다. 멀티 쓰레드에 안전(thread-safe)
- StringBuilder는 동기화 되어 있지 않다.
- 멀티 쓰레드 프로그램이 아닌 경우, 동기화는 불필요한 성능저하
  - 이럴 땐 StringBuffer 대신 StringBuilder를 사용하면 성능 향상
  - 메서드는 동일 함

## Math 클래스

- 수학 관련 static메서드의 집합
  - E : 자연로그의 밑
  - PI : 원주율
- round()로 원하는 소수점 아래 세 번째 자리에서 반올림하기
- Math 클래스의 메서드
  - abs() : 주어진 값의 절대값을 반환한다.
  - ceil() : 주어진 값을 올림하여 반환한다.
  - floor() : 주어진 값을 버림하여 반환한다.
  - max(a, b) : 주어진 두 값을 비교하여 큰 쪽을 반환한다.
  - min(a, b) : 주어진 두 값을 비교하여 작은 쪽을 반환한다.
  - random() : 0.0~1.0범위의 임의의 double 값을 반환한다.(1.0은 범위에 포함되지 않는다.)
  - rint() : 주어진 double값과 가장 가까운 정수값을 double형으로 반환한다. 단, 두 정수의 정가운데 있는 값은 짝수를 반환
  - round() : 소수점 첫째자리에서 반올림한 정수값(long)을 반환한다. 두 정수의 정가운데있는 값은 항상 큰 정수를 반환
    ```java
    Math.rint(4.5) // 4.0
    Math.round(4.5) // 5
    ```

## 래퍼(wrapper) 클래스

- 8개의 기본형을 객체로 다뤄야할 때 사용하는 클래스
- boolean : Boolean
- char : Character
- byte : Byte
- short : Short
- int : Integer
- long : Long
- float : Float
- double : Double

## Number 클래스

- 모든 숫자 래퍼 클래스의 조상

## 문자열을 숫자로 변환하기

- 문자열을 숫자로 변환하는 다양한 방법
  ```java
  new Integer("100").intValue();
  Integer.parseInt("100"); // 문자열 -> 기본형
  Integer.valueOf("100"); // 문자열 -> 래퍼 클래스
  ```
- n진법의 문자열을 숫자로 변환하는 방법
  ```java
  Integer.parseInt("100", 2); // 4
  Integer.parseInt("100", 8); // 64
  Integer.parseInt("100", 16); // 256, 두번째 값 입력 안하면 자동으로 10 입력
  ```

## 오토박싱 & 언박싱

- JDK 1.5 이전에는 기본형과 참조형간의 연산이 불가능 했음
- 이후에는 가능해짐
  - 기본형의 값을 객체로 자동변환하는 것을 오토박싱, 그 반대는 언박싱
    ```java
    int i = 5;
    Integer iObj = new Integer(7);

    int sum = i + iObj; // 이 문장을
    int sum = i + iObj.intValue(); // 이렇게 컴파일러에서 자동으로 바꿔줌
    ```
