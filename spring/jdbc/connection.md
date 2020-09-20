# JDBC DB Connection

## JDBC DB Connection 과정
  1. [Import JDBC Packages](#Import-JDBC-Packages)
  2. [Register JDBC Driver](#Register-JDBC-Driver)
  3. [Database URL Formulation](#Database-URL-Formulation)
  4. [Create Connection Object](#Create-Connection-Object)

---
## Import JDBC Packages
* Import 문은 코드 내에서 참조하고 있는 클래스가 어디 있는지를 자바 컴파일러에게 알려주는 역할을 한다.
* CRUD 명령을 할 수 있게 도와주는 Standard JDBC package를 사용하기 위해서는 다음과 같은 패키지를 import하면 된다.
```java
import java.sql.*;
```

## Register JDBC Driver
* JDBC를 사용하기 위해서는 먼저 driver를 등록해야 한다.
* Driver를 등록하는 것은 Oracle driver의 class 파일이 메모리에 로드되는 것을 의미한다.
* 따라서 driver 등록은 JDBC 인터페이스의 구현을 통해 이루어질 수 있다.
* 드라이버 등록은 다음과 같은 2가지 방법으로 가능하다.

### `Class.forName()`
* 가장 흔하게 쓰이는 방법이다.
* 이 방법을 통해 동적으로 driver의 class를 메모리에 로드하면, 자동으로 등록이 완료된다.
* Driver 등록에 대한 설정이 가능하고 이동하기 용이하게 만들어지기 때문에 선호된다.
* 다음 예제는 Oracle 드라이버를 등록하기 위해 `Class.forName()`을 사용한다.
```java
try {
    Class.forName("oracle.jdbc.driver.OracleDriver");
}
catch(ClassNotFoundException ex) {
    System.out.println("Error: unable to load driver class!");
    System.exit(1);
}
```
* 호환되지 않는 JVM을 위해 `newInstance()` 메소드를 사용할 수도 있다.
* 이 경우에는 추가적인 예외처리가 필요하다.
```java
try {
   Class.forName("oracle.jdbc.driver.OracleDriver").newInstance();
}
catch(ClassNotFoundException ex) {
   System.out.println("Error: unable to load driver class!");
   System.exit(1);
catch(IllegalAccessException ex) {
   System.out.println("Error: access problem while loading!");
   System.exit(2);
catch(InstantiationException ex) {
   System.out.println("Error: unable to instantiate driver!");
   System.exit(3);
}
```

### `DriverManager.registerDriver()`
* 드라이버를 등록하는 또 하나의 방법은 `static DriverManager.registerDriver()` 메서드를 사용하는 것이다.
* Microsoft에서 배포하는 것과 같이 JDK를 준수하지 않는 JVM을 사용할 때에는 `registerDriver()` 메서드를 사용해야 한다.
* 다음은 Oracle 드라이버를 등록하기 위해 `registerDriver()`를 사용하는 예제이다.
```java
try {
   Driver myDriver = new oracle.jdbc.driver.OracleDriver();
   DriverManager.registerDriver( myDriver );
}
catch(ClassNotFoundException ex) {
   System.out.println("Error: unable to load driver class!");
   System.exit(1);
}
```

## Database URL Formulation
* Driver를 load 했다면, `DriverManager.getConnection()` 메서드를 사용해서 connection을 설정할 수 있다.
* `getConnection()` 메서드는 다음과 같이 overload 되어있다.
  * `getConnection(String url)`
  * `getConnection(String url, Properties prop)`
  * `getConnection(String url, String user, String password)`
* 각각의 형태는 연결하고자 하는 DB의 URL을 요구한다.
* DB 연결 과정 중 대부분의 문제가 발생하는 곳이 URL 설정이다.
* 다음은 DB 각각에 해당하는 JDBC 드라이버와 DB URL을 나타낸 표이다.
|RDBMS|JDBC driver name|URL format|
|-|-|-|
|MySQL|com.mysql.jdbc.Driver|jdbc:mysql://hostname/databaseName|
|Oracle|oracle.jdbc.driver.OracleDriver|jdbc:oracle:thin:@hostname:portNumber:databaseName|

## Create Connection Object
* 다음은 `DriverManager.getConnection()` 메서드를 사용하여 connection object를 만드는 세가지 형태이다.

### URL, username과 password 사용하기
* 가장 많이 쓰이는 형태이다.
```java
String URL = "jdbc:oracle:thin:@localhost:1521:XE";
String USER = "username";
String PASS = "password"
Connection conn = DriverManager.getConnection(URL, USER, PASS);
```

### URL만 사용하기
```java
String URL = "jdbc:oracle:thin:username/password@localhost:1521:XE";
Connection conn = DriverManager.getConnection(URL);
```

### URL과 Properties 오브젝트 사용하기
* Properties 오브젝트는 Driver에 전달할 keyword와 value 페어를 가지고 있다.
```java
import java.util.*;

String URL = "jdbc:oracle:thin:@localhost:1521:XE";
Properties info = new Properties( );
info.put( "user", "username" );
info.put( "password", "password" );

Connection conn = DriverManager.getConnection(URL, info);
```

## JDBC Connection 종료하기
* JDBC 사용이 끝나면 명시적으로 모든 연결을 `close()` 해주어야 한다.
* 연결을 종료하지 않더라도 자바의 GC가 자동으로 stale된 오브젝트를 처리하지만, 보다 통제된 자원 관리를 위해 직접 처리해주는 것이 더 좋다.
* `finally` 블록 안에 `conn.close();` 를 넣어 실행시켜주는 방법을 주로 사용한다.
* `finally` 블록은 exception의 발생 여부와 관계 없이 항상 실행된다.