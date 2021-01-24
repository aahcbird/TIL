# 백엔드 기초
## Web 탄생 배경
* Client와 Server가 단순 data를 주고 받는 것은 비효율적.
* 그래서 data 전송을 원활히 하기 위해 **socket**, **RPC** 등의 기술이 사용됐지만 한계가 있었음.
* Data를 전달하는 방식의 규격화가 계속 발전하여 **Web**과 **Page**이라는 개념이 만들어지고 **Web Client와 Web Server가 page를 주고 받게 됨**.

## Web의 동작 방식
* 현재 Web에서의 페이지 요청은 다음과 같은 방식으로 이루어짐.
  1. **Web Client**가 브라우저를 통해 **Web Server**에 page를 **GET Request**
  2. **Web Server**는 요청을 받아 요청에 해당하는 코드가 홈 디렉토리에 있는지 찾아 봄.
  3. **Web Server**는 동적으로 문서를 만들기 위해 **WAS(Web Application Server)**을 호출.
  4. **WAS**는 Code를 실행하고 DB와 소통하며 페이지를 만들어 이를 **Web Client**에 **Response**한다.

## WAS Context
* 프로젝트의 규모가 커져 여러 사람이 협업을 하는 구조에서는 **각 디렉토리 Path를 접근할 수 있는 다른 이름**이 필요하다.
* 이를 WAS에서의 **Context**라고 한다.
* 예로 Tomcat에서는 Context가 다음과 같이 사용된다.
```
server.xml

<Host name="localhost" appBase="webapps" unpackWARs="true" autoDeploy="true">
    <Context Path="it" docBase="D:tools\apache-tomcat-9.0.19\webapps\ITWeb" privileged="true"/>
...
```
* 이 설정을 적용하면 WAS를 거쳐 `it/foo`에 접근을 시도할 때 `ITWeb/foo`에 접근한 것과 같은 기능을 가지게된다.