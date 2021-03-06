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
|usr| |Program Files|
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
|ls|디렉토리 내 파일 목록 나열|자세히 보기 옵션 : `-l`<br>숨긴 파일 보기 옵션 : `-a`|
|cd|디렉토리를 변경| |
|man|메뉴얼 파일 열기|`man ls`|

* `ls -l` 와 같이 `-l`옵션을 enable하면 long listing format으로 출력이 가능하다.
  * ex) `-rwxrw-r-- 1 soon soongroup 3 Feb 26 07:08 file`
  * `-rwxrw-r--`
    * 맨 앞의 알파벳은 파일 타입을 나타낸다.
    * 이어지는 rwx 3묶음은 각각 owner, group, other(그 외)에 대한 read, write, execute 권한을 의미한다.
  * `1` = 해당 파일에 대한 Hard Link의 수
  * `soon` = 파일의 소유자
  * `soongroup` = 파일이 속한 그룹
  * `3` = 파일 크기
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

## 그 외 유용한 명령어들
|명령어|설명|예시|
|:-|:-|:-|
|clear|콘솔 지우기| |
|history|명령어 히스토리|`!96` : 96번째 명령어 실행|
|>|Redirection|`echo "hello" > test`<br> `hitory > test`|
|>>|Redirection + 뒤에 추가 |`echo "Okay" >> test"`|
|\||받아서 오른쪽에서 처리|`cat test | grep He`|
|less|한 페이지씩 확인하기|`ls -l | less`|
|sort|정렬|`history | sort`<br>`-r` 옵션으로 역정렬 가능|
|;|명령어 연속 실행|`touch test1; echo "okay~" >> test1; cat test1`|
|ctrl+z|backgroud로 이동(nano 등)| |
|fg 1|1번 foreground로 이동| |

## 파일 압축
### tar(Tape ARchive) + zip
|옵션|설명|
|:-|:-|
|-f|파일 이름을 지정|
|-c|파일을 tar로 묶음|
|-x|tar 압축을 풂|
|-v|내용을 자세히 출력|
|-z|gzip으로 압축하거나 해제함|
|-t|목록 출력|
|-p|파일 권한을 저장|
|-C|경로를 지정|
* 압축 하기
  * `tar -cf name.tar a b c`
  * `tar -zcf name.tar.gz a b c`
* 압축 풀기
  * `tar -xvf name.tar`
  * `tar -zxvf name.tar.gz`

## 링크 파일 만들기
* 명령어
  * `ln [OPTION]... TARGET [...] [LINKNAME [...]]`
  * `-s` 옵션을 통해 Symbolic link를 생성
    * Symbolic Link란 Windows의 바로가기 같은 것
    * `cp -s TARGET LINKNAME` 명령어를 통해서도 생성 가능. 
  * `-s` 옵션이 없으면 Hard link가 생성 됨.
    * Hard Link는 참조하는 파일과 파일 생성일, 크기까지 동일. 파일명만 다르다.

## 리눅스 환경 변수 설정법
* 리눅스의 환경 변수 설정은 `$PATH` 경로 안에 링크 파일을 생성하여 실제 사용하고자 하는 경로를 참조하도록 하는 방식으로 설정이 가능하다.
* `$PATH`의 경로 중 하나인 `/home/(user)/bin` 디렉토리에서 다음과 같은 명령어를 통해 링크파일을 생성한다.
* `ln -s ~/download/jdk1.8.0_161/bin/java java`
* `ln -s ~/download/jdk1.8.0_161/bin/javac javac`

### 하지만 시스템 레벨에선 JDK를 같이 사용할 수도..
* 위와 같은 설정으로는 `/home/(user)/bin`에 접근이 불가능한 사용자가 있을 수 있다
* 이 때 `$PATH`의 경로 중 하나인 `/usr/bin`을 사용할 수도 있다.

## 사용자 관리
|명령어|설명|
|:-|:-|
|useradd|사용자 추가|
|usermod|사용자 변경|
|userdel|사용자 삭제|
|alt + F1~F6|터미널 전환|
|id|현재 사용자 정보 출력|
* 사용자 추가를 했을 경우엔 패스워드와 홈 디렉토리 지정을 해주어야 한다.
  * `sudo useradd (user)`
  * `sudo passwd (user)`
  * `sudo mkdir /home/(user)`
* 사용자 정보를 확인하는 명령어
  * `cat /etc/passwd`
  * `(Username):(Password):(UID):(GID):(User ID Info):(Home directory):(Command/Shell)`
* 사용자가 포함된 그룹을 확인하는 명령어
  * `groups (user)`

* 사용자 변경
  * `sudo chown (user):(group) (file)`

## 스크립트 파일 생성
```vim
useradd testuser
tail -n2 /etc/passwd
mkdir /home/testuser
chown testuser:testuser /home/testuser
echo "testuser user added"
```
* 파일을 생성하고 실행하기 위해선 파일 권한을 변경해줘야 한다.
* 파일 권한 변경
  * `chmod [OPTION]... MODE[,MODE]... FILE...`
  * `OPTION` = `[ugoa]*([-+=]([rwxXst]*|[ugo]))+|[-+=][0-7]+`
  * 예시
    * `chmod 644 test.txt`
    * `chmod go+r test.txt`
* 스크립트 파일에 파라미터 사용하는 법
  * `$n`와 같이 지정하여 사용(n번째 파라미터)

### 그럼 이제 adduser 명령어를 실행가능할까?
* 리눅스는 실행파일에 대해서는 resolving 과정을 거침.
* 셸 자체에서 사용하는 명령어인지 확인한 후, 아니라면 PATH를 확인해서 실행한다.
* 따라서 adduser 명령어를 실행하기 위해선 `./adduser`로 실행해야 함.
* `whereis adduser` 명령어로 리눅스가 가지고 있는 특별한 `adduser`들의 위치 확인 가능
* `./adduser`와 같이 실행하기 어려우므로 `$PATH`에 실행파일을 위치시켜야 함.
* `$PATH`의 목록 중 가장 앞에 있는 것부터 차례로 우선순위를 가진다.
* `which adduser` : 실행될 수 있는 동명의 여러 명령어들이 있다면 어떤 것이 실행되는가?
  * `sudo which adduser` 는 결과가 다를수도..
  * root의 권한의 `$PATH`는 사용자의 것과 다를 수 있기 때문

### 향상된 사용자 추가
* `useradd`보다는 `adduser`가 더 많이 쓰임.
* 마찬가지로 `deluser`도 가능.
* `moduser`는 없고 `usermod`를 사용해야 함.

## 프롬프트 스트링
* `soon@server:~$`와 같이 프롬프트에 나오는 문자열을 의미
* 출력하기
  * `echo $PS1`
* 변경하기
  * `PS1="soon : ";`
  * 변경은 일시적이며, 영구적으로 변경하기 위해선 프로필을 저장해야 함.

### 프롬프트 스트링의 이스케이프 문자
|문자|설명|
|:-|:-|
|\\H|hostname|
|\\h|hostname up to the first '.'|
|\\d|date|
|\\n|newline|
|\\r|carriage return|
|\\t|current time in 24-hour|
|\\T|current time in 12-hour|
* 추가적인 정보는 'Bash Prompt Escape Sequences'로 검색

## 출력 색상 변경
* 명령어 예시
  * `LS_COLORS="(파일 종류)=(타입);(속성)"`
  * `LS_COLORS="di=0;33"`

|파일 종류|설명|
|:-|:-|
|di|directory|
|fi|file|
|ln|symbolic link|
|so|socket file|
|ex|executable file|

|타입|설명|
|:-|:-|
|0|default color|
|1|bold|
|4|underlined|
|5|flashing text|
|7|reverse field|

|색상|설명|
|:-|:-|
|1|red|
|32|green|
|33|orange|

## 명령어 별칭 만들기
* `type ls` 해보면 `ls` 명령어도 사실은 `ls --color=auto`의 별칭인 것을 알 수 있음.
* 명령어 별칭 만들기
  * `alias ls='ls -l'` 과 같이 사용.

## 리눅스 부팅 순서
1. BIOS (Basic I/O System)
   * 메모리, 그래픽카드 등 확인
2. Master Boot Record (MBR)
   * 디스크에 정의되어 있는 가장 바깥 영역
3. LILO or GRUB
   * 운영체제 선택
4. Kernel
5. init : process number 1(PID=1)
   * -/linuxrc : load modules / initialize devices / exits
   * -/sbin/init
     * -/etc/inittab : run boot scripts
       * -/etc/init.d/rcS
         * -/etc/rcS.d/S* scripts
         * -/etc/rc.boot/*
6. Run Levels
   * Windows의 안전모드와 같이 올라가는 서비스의 단계 구분되어 있음.
   * `/etc/rc/...`에 run level에 해당하는 디렉토리가 위치
     * 예) `/etc/rc/rc6.d/`
     * 디렉토리 안에 있는 링크파일명의 접두사는 우선순위를 의미.
     * run level을 바꾸기 위해 `sudo init 6` 실행 (6번은 reboot)

* 종료하는 법
  * `poweroff`, `halt`, `shutdown`, `init 0`
* 재시작
  * `reboot`, `shutdown`, `init 6`

## Shell Script 실행 순서

* Shell 이란?
  * 사용자가 SW를 사용할 수 있게 도와주는 창

### 로그인 할 때 실행되는 스크립트 RC(Run Commands)
1. Bash 시작 스크립트
2. 로그인 쉘
   * `/bin/login` 이후 2개 실행 됨.
     * `/etc/profile` (모든 사용자 설정)
       * `/etc/profile.d/`
       * `/etc/bash.bashrc`
     * `~/.profile` (개인-overwrite)
       * `~/.bashrc`
3. 비로그인 쉘
   * `/bin/bash` or `/bin/su` or `terminal`
     * `virtual terminal run`
     * `/etc/bash.bashrc`
       * `~/.bashrc`
       * `~/.bash_logout`
4. Bash 로그아웃 스크립트
   * `~/.bash_logout`

### 프로필 수정해보기
* 프로필이 적용되려면 새로 로그인 하거나, 프로필을 갱신해줘야 한다.
1. `/bin/etc/profile` 끝에 `alias aa='ls -l'` 추가
2. `/bin/etc/profile.d/`안에 `alias aa='ls -l'`을 넣은 `alias.sh`파일 추가

#### 그럼 프로필에 환경변수를 설정하면 되는건가?
* pam
  * 서비스를 인증하기 위해 사용하는 인증모듈
* `/etc/pam.d/login`
  * 로그인 할 때 실행 됨.
  * pam 모듈을 사용할 때 인증하는 것들은 `/etc/environment`를 읽어들인다.
  * 따라서 환경변수는 `/etc/environment`에 설정하는게 가장 좋음.
    * `/etc/environment`는 위 프로필들과 다르게 script파일은 아님.

## JDK 전역화 하기
* `/usr/environment`에 JDK 경로를 입력한다.
* 아직 환경변수를 읽지 않았기 때문에 JDK 경로 입력 후 바로 `java -version`을 타이핑하면 인식하지 않는다.
* 이 때 환경변수를 다시 읽기 위해 source 명령어를 사용한다.
  * `source /etc/environment` 후에 `echo $PATH`를 타이핑하면 환경변수가 정상적으로 바뀜을 알 수 있다.
  * 이 방법을 통해 다른 user도 JDK를 사용할 수 있게 된다.

## Debian 패키지로 tree 유틸리티 설치하기
* tree : 디렉토리를 현재 디렉토리 뿐만 아니라 tree 형식으로 나타내게 도와주는 유틸리티.
* `wget http://kr.archive.ubuntu.com/ubuntu/pool/universe/t/tree/tree_1.8.0-1_amd64.deb`
* 다운로드 후 `dpkg -i` 명령어를 통해 설치해준다. (debian package)

* dpkg 옵션

|옵션|설명|
|:-|:-|
|-i|패키지 설치|
|-l|설치된 패키지들의 리스트 출력|
|-L|설치된 패키지의 위치 출력|
|-r|패키지 삭제(실행 파일만)|
|-R|패키지 삭제(설정 파일까지)|

* 하지만 Debian 패키지를 직접 다운로드하는 것보다 더 좋은 설치 방법이 있다!

## APT를 이용해 소프트웨어 설치하기
* APT(Advanced Packaging Tool) : 향상된 패키지 관리 도구
  * `.deb` 파일들이 저장되어있는 우분투 패키지 저장소의 목록을 볼 수 있도록 해준다.
* `/etc/apt/sources.list` : 저장소의 목록
  * 만약 저장소를 추가하고 싶다면 목록에 추가 후 `apt-get update`
  * 의존성 검사를 통한 목록 갱신 : `apt-get dist-update`
  * 목록을 업데이트 하게되면 설치할 수 있는 패키지 정보들을 cache화 한다.
  * `apt-cache search X` : cache화된 패키지를 찾는다.
  * `apt-cache show X` : cache화된 패키지의 정보를 보여준다.
* `apt-get remove` : 다운로드 받은 패키지의 실행파일만 삭제
* `apt-get purge` : 다운로드 받은 패키지의 실행파일과 설정파일 삭제

### JDK 찾아서 설치
* `apt-cache pkgnames | grep jdk` : description 없이 패키지 목록만 표기
* `sudo apt-get install openjdk-11-jdk`

## PPA를 이용해 소프트웨어 설치하기
* PPA(Personal Package Archive) : 개인화된 패키지 저장소
* Canonical이 제공하지 않는 패키지를 Launchpad의 PPA 등을 통해 다운받을 수 있음.
* ex) PPA for OpenJDK 검색 -> `ppa:openjdk-r/ppa`
* ex) ubuntu PPA oracle Java 8 -> `ppa:webupd8team/java`
* `add-apt-repository ppa:openjdk-r/ppa` `apt-get update`
* `apt-cache pkgnames | grep oracle | grep java`

## 여러 개의 JDK를 다운받았을 때 버전 변경하는 법
* `update-java-alternatives`
  * `-l` : JDK 리스트 나열
  * `-s` : 해당 JDK로 변경

* 어떻게 이게 가능한걸까?
  * 내부적으로는 링크 파일을 이용한 프로그램 실행
  * 링크 관리 도구 `update-alternatives` 이용하여 설정 변경 가능
    * ex) `sudo update-alternatives --config editor`
  * 반복적인 링크로 연결되어 있다.
    * `whereis editor`
    * `ls -l /usr/bin/editor`
      * `/usr/bin/editor -> /etc/alternatives/editor`
    * `ls -l /etc/alternatives/editor`
      * `/etc/alternatives/editor -> /bin/nano`
  * 비슷한 기능을 직접 추가도 가능하다.
    * `sudo update-alternatives --install ~/bin/bb bb ~/test1.sh 1`

## Telnet 서비스란?
* 보통 Tomcat이나 MySQL 등을 원격 컴퓨터에 설치하고 그것을 관리할 목적으로 리눅스를 사용하는데, 원격으로 터미널에 접속할 수 있게 도와주는 서비스.
* 비슷하게 SSH, FTP가 있음.

### Telnet 설치
* `dpkg -s telnetd`
  * `-s`옵션을 통해 설치 여부를 체크할 수 있음.
  * telnet 뒤에 붙는 d는 서비스를 의미.
  * `sudo apt install telnetd`

### 윈도우에서 Telnet으로 가상머신에 접속해보기
* Linux에서 `ifconfig` 명령어를 사용하면 ip주소 확인가능
* `telnet 10.0.2.15` 명령어를 통해 접속해보자.
  * 이건 가상 머신으로 부여 받은 private ip이기 때문에 접속 되지 않음.
  * 23번 포트를 사용하는 telnet에 접속하기 위해선 Port Forwarding 필요
  * 가상 머신 네트워크 설정에서 호스트 IP + 호스트 포트로 오는 요청이 있으면 게스트 IP + 게스트 포트로 포워딩해줄 수 있도록 설정
  * 마찬가지로 공유기에 Port Forwarding을 해준다면 전세계 어디에서든 telnet으로 가상 머신안의 리눅스에 접속 가능.
  * 하지만 보안상의 문제로 Telnet은 잘 쓰이지 않는다.