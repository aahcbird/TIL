# Linux
## Linux를 사용하는 이유
* 대부분의 소프트웨어가 NT가 아닌 Unix를 기반으로 만들어졌다.
* 따라서 Linux의 조상격인 Unix의 기능을 익혀두는 것이 개발 과정에 필요하다.

## Linux 계열
1. Debian
    * Ubuntu 포함
    * 가장 점유율이 높음.
2. Slackware
3. Red Hat

## Linux 공부 목표
* Tomcat/MySQL
* JAVA JDK 설치
* Telnet/SSH/FTP
* 설치파일 관리
* Bash Shell
* 프로세스 관리
* 사용자 관리
<br>

* Linux/Unix 역사
* Linux 서버 설치
* 파일 편집
* 파일 관리

## Shell 이란?
* 사용자는 application을 사용하기 위해서 OS와 커뮤니케이션을 하기 위한 인터페이스
* Windows의 explorer, CLI
* 리눅스의 bash shell (최초의 유닉스 쉘인 Bourne shell과 호환)

### Bash shell
* 권한
  * `$` = 일반 유저
  * `#` = 관리자
```
soon@:~$
root@:~#
```
* root 권한 실행(sudo)
  * `$sudo reboot`
  * `$sudo halt`
* 관리자로 전환
  * 사용자 전환
    * `$sudo su - root`
    * `$sudo su -`
  * 현재 위치에서 권한만 전환
    * `$sudo su `
* 다시 일반 유저로 전환
  * `exit`

## Linux File System
|Linux|설명|Windows|
|:-|:-|:-|
|mnt||Drive(C:\\, D:\\)|
|bin| |System32|
|home| |Documents, Pictures, Downloads, ...|
|usr||Program Files|
|etc|프로그램이 실행되기 전 생성되는 파일들|registry|
|var|프로그램 실행 중 생성되는 파일들| |
|bin|모든 유저가 사용하게 될 실행 파일들| |
|sbin|관리자가 사용하게 될 실행 파일들| |
|tmp|임시 값들| |
|sys|시스템에 대한 설정들| |

## 파일 탐색을 위한 명령어들
|명령어|설명|예시|
|:-|:-|:-|
|pwd|현재 디렉토리 경로를 출력(Print Working Directory)| |
|ls|디렉토리 내 파일 목록 나열|자세히 보기 옵션 : `-l`|
|cd|디렉토리를 변경| |
|man|메뉴얼 파일 열기|`man ls`|

* `ls -l` 명령어로 디렉토리 내 파일 목록 나열 시 맨 앞에 있는 정보
  * ex) `drwxrwxr-x`
  * 맨 앞 d는 해당 파일이  directory임을 나타냄. (혹은 파일명이 파란색인 것을 보고 확인 가능)
* `ls`명령어로 비슷한 파일 검색
  * `ls Hello[12].java` = `Hello1.java`와 `Hello2.java`만 검색 됨.
* 쉘에서의 위치
  * `/` = /(최상위 디렉토리)
  * `~` = /home/soon(홈 디렉토리)

## 파일 관리를 위한 명령어들
|명령어|설명|예시|
|:-|:-|:-|
|mkdir|디렉토리 생성| |
|rmdir|디렉토리 삭제| |
|touch|빈 파일 생성|`touch text.txt`|
|mv|파일 이동/변경|파일 이동 : `mv text.txt workspace/`<br>파일 이름 변경(before->after) : `mv before after`|
|rm|파일 삭제|재귀 옵션 : `-r` (디렉토리도 삭제 가능)<br>상호작용 : `-i` (y/n)?|
|rmdir|디렉토리 삭제| |
|cp|파일 복사|`cp Hello.java Hello2.java`|

## 파일 편집을 위한 명령어들
### vi
* vi 실행 
  * `vi Hello.java`

|명령어|설명|예시|
|:-|:-|:-|
|h|왼쪽으로 이동| |
|j|아래로 이동| |
|k|위로 이동| |
|l|오른쪽으로 이동| |
|i|현재 커서에서 insert 모드 전환| |
|o|한 줄 띄우고 insert 모드 전환| |
|a|한 칸 뒤에서 insert 모드 전환| |
|:q|종료|변경 내용 있을 시엔 경고 뜸|
|:w|저장| |
|y|복사|`yy` : 줄 하나 복사<br>`yw` : 단어 하나 복사<br>`yl` : 문자 하나 복사|
|p|붙여넣기| |

### nano
* nano 실행
  * `nano Hello.java`
  * `editor Hello.java`

## 파일 찾기
* 이름으로 찾기
  * `find ./ -name *.java`
* 파일 크기로 찾기
  * `find . -size +1c`
  * 단위를 지정안하면 512byte(`b)가 디폴트
* root 디렉토리에서 일반 유저 권한으로 찾는다면 일부 파일은 permission denied 뜨게 됨에 유의!

## 파일 출력하기
* `cat Hello.java`
* 앞에서부터 출력하기
  * `head -n2 Hello.java`
* 뒤에서부터 출력하기
  * `tail -n2 Hello.java`

## 파일 내에서 검색하기
* `grep class Hello.java`
* `grep "Hello Linux" Hello.java`
  * case 무시 옵션 : `-i`

## 파일 비교
* 차이가 나는 줄의 위치 출력
  * `cmp Hello.java Hello1.java`
    * `Hello.java Hello1.java differ: byte 90, line 3`
* 명시적으로 차이 출력
  * `diff Hello.java Hello1.java`
```
3c3
<       System.out.println("Hello Linux");
---
>       System.out.println("Hello Linux1");
```

## 파일 정보 확인
* `file Hello.java`
  * `Hello.java: C++ Source, ASCII text`