# Servlet
## Servlet 코드 작성과 컴파일
* Servlet 코드는 WAS에 의해서 load된다.
* Servlet 코드는 `main()` 메서드 대신 `service()` 메서드를 사용한다.
* Servlet 코드는 Servlet를 참조하기 위해 추상 클래스 혹은 인터페이스를 상속 받는다.
  * 따라서 Servlet 코드에서 호출하는 함수는 미리 정해져 있는 서비스 함수이다.
```java
import javax.servlet.*;
import javax.servlet.http.*;
import java.io.*;
public class Nana extends HttpServlet {
    public void service(HttpServletRequest request, HttpServletResponse response) throws IOException, ServletException {
        System.out.println("Hello Servlet");
    }
}
```
* 클래스패스에 Servlet 라이브러리를 넣어 .java 파일을 컴파일 하기 위해서는 CLI에서 `javac -cp "(Tomcat폴더)/lib/servlet-api.jar" Nana.java` 명령어를 실행하면 된다.
* 컴파일 된 .class파일은 Tomcat 폴더의 `webapps/ROOT/WEB-INF/classes`에 위치하는 것이 규칙이다.
  * WEB-INF 폴더 안의 파일들은 클라이언트가 직접 요청하는 것이 아닌, 서버에서 활용되는 자원이다. 
* 클라이언트가 URL을 서버에 요청하면, WAS는 URL을 매핑하여 해당하는 Servlet 코드를 찾아 실행하게 된다.
  * 이 매핑 정보는 Tomcat의 WEB-INF폴더 안의 web.xml에 기록한다.
```xml
<servlet>
    <servlet-name>na</servlet-name>
    <servlet-class>Nana</servlet-class>
</servlet>

<servlet-mapping>
    <servlet-name>na</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping>
```
* 위 코드에서 사용자가 `http://localhost/hello` 주소로 요청을 보내게 되면, WAS가 매핑해 Nana.class를 찾아 처리한다.

#### Servlet 코드에서의 출력이 서버가 아닌 클라이언트 쪽에서 보여지도록 하려면?
```java
import javax.servlet.*;
import javax.servlet.http.*;
import java.io.*;
public class Nana extends HttpServlet {
    public void service(HttpServletRequest request, HttpServletResponse response) throws IOException, ServletException {
        OutputStream os = response.getOutputStream();
        PrintStream out = new PrintStream(os, true); // true = 버퍼가 꽉차지 않아도 전송하겠다.
        out.println("Hello Servlet");
    }
}
```
* Java에서는 문자의 단위가 2바이트이기 때문에 바이트 기반 스트림을 보조 하기 위해 문자 기반 스트림을 사용한다.
* `PrintStream` 은 문자 기반 스트림이고, 추가로 `print()`, `println()` 등의 메서드를 제공한다.
```java
        PrintWriter out = response.getWriter();
        out.println("Hello Servlet");
```
* 위와 같이 `OutputStream`을 생략하고 문자 전용 스트림인 `PrintWriter`를 사용하는 방법도 있다.
* `PrintWriter`는 `PrintStream`에 비해 더 많은 문자를 지원한다.
  * 하지만 `System.out`이 여전히 `PrintStream`이기 때문에 `PrintStream`도 여전히 사용된다.