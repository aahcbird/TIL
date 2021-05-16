# EC2
## EC2(Elastic Compute Cloud)란?
* 독립된 컴퓨터 한 대를 통째로 임대해주는 서비스
* 가장 범용적인 서비스

## Instance
* 컴퓨터 한 대가 하나의 instance라고 보면 된다.

### Instance 생성 
1. Choose AMI
   * AMI(Amazon Machine Image)
     * Instance를 생성할 때 사용할 운영체제
     * 상당수는 무료로 이용할 수 있지만, SQL Server의 경우 MS에서 고가의 정책을 가지고 있기 때문에 무료가 아님.
2. Instance Type
   * Family : 주 사용 용도에 따른 인스턴스의 분류
   * Type
     * `m**` : 같은 가격 기준으로 볼 때 memory 성능이 좋은 타입
     * `c**` : 같은 가격 기준으로 볼 때 cpu 성능이 좋은 타입
   * vCPUs : virtual CPU의 개수
   * Network Performance : 네트워크 속도
3. Instance Details
   * Shutdown behavior : 셧다운 시 OS의 행동
     * Stop 설정 시 Shutdown 하면 Storage에 해당하는 비용만 발생.
   * Enable termination protection : 실수로 인스턴스를 삭제하는 행위를 방지.
   * Monitoring : CPU, Memory에 대한 모니터링을 디테일하게 적용(추가 요금)
4. Add Storage
   * Volume Type
     * Provisioned IOPS : 직접 저장장치의 성능을 설정
   * Delete on Termination : default로는 Instance와 Storage는 라이프사이클이 다름.
5. Tag Instance
6. Configure Security Group
   * 제한된 설정으로만 인스턴스에 접속할 수 있도록 만들도록 하기 위한 그룹.
   * Type
     * SSH(22) : Linux / Unix 운영체제에서 원격 제어를 할 때 사용하는 프로토콜.
     * HTTP(80) : 인스턴스를 웹 서버로 사용하고자 할 경우.
     * RDP(3389) : Windows 인스턴스 일 경우에 지정됨.
       * Windows는 독자적인 원격 제어의 방식을 사용한다.
7. Review Instance Launch
   * Key pair
     * 인스턴스에 접근할 때 사용하는 일종의 비밀번호
     * public key, private key를 파일의 형태로 저장.

## 가격 정책
* On-demand
  * 필요할 때 켜고 필요없을 때는 끄는 방식
* 예약 인스턴스
  * 기본적으로는 On-demand 방식이나 한 번에 긴 기간을 계약하는 사용자에게 할인을 해주는 정책
* 스팟 인스턴스
  * AWS가 인스턴스 할당을 하면서 어쩔 수 없이 노는 컴퓨터가 발생하게 되는데, 노는 인스턴스의 수가 많아지면 가격이 내려가고, 그렇지 않으면 가격이 올라가는 방식의 가격 정책.

## 인스턴스 접속

### Linux

#### OSX에서 리눅스 인스턴스로 접속
* 원격제어를 하기 위해선 원격제어할 수 있는 프로그램(SSH Client)이 필요.
  * 리눅스의 경우 Terminal
* key를 `aws_password.pem`으로 변경 후 터미널을 실행할 위치로 이동.
* key의 권한은 읽기만 허용, 다른 모든 사람은 권한 없음.
* `ssh -i "aws_password.pem" ubuntu@{대상ip주소}`
  * `ubuntu`는 우분투 인스턴스가 생성될 때 자동으로 만들어지는 아이디
  * 우분투 인스턴스가 아니라면 `ec2-user`
* 접속을 끊고 싶을 때는 `exit`

#### Windows에서 리눅스 인스턴스로 접속
* Windows에선 SSH 사용 위해 별도 프로그램 설치 필요(Xshell, PuTTY 등)
* Xshell의 경우 새로운 세션을 등록해야 함.
  * 호스트 : 대상 ip 주소
  * 사용자 인증
    * Public Key 방식으로 변경
    * 사용자 이름
    * 사용자 키
    * 암호 : 공백으로 둔다.

#### 리눅스에서 웹서버 사용
* 인스턴스의 Security Group을 확인해보면 `80` Port가 열려있기 때문에 인스턴스가 서버로서의 기능 수행 가능.
* `sudo apt-get install apache2`
  * 설치된 이후 바로 apache가 실행된다.
* Instance의 Description 탭에서 Public DNS에 있는 도메인 이름을 주소창에 입력하여 인스턴스에 접속 가능
  * 페이지 중간 부분 Document Roots에 서버를 위한 파일들의 위치 정보가 나와있다.

### Windows

#### OSX에서 Windows 인스턴스로 접속
* Windows server란 Window를 서버 특화로 사용할 수 있게 만든 서버
* 윈도우 인스턴스에 접속하고자 할 때 Key pair를 입력하면 RDP를 사용하기 위한 Public IP, User name, Password를 발급해줌.
* OSX에서 Windows 인스턴스를 사용하려면 Microsoft에서 만든 MAC용 원격 제어 프로그램을 사용할 수 있음.
  * 앱스토어에서 Microsoft Remote Desktop 다운로드
  * New -> Edit remote desktop에서 PC name에는 IP 주소를 입력

#### Windows에서 Windows 인스턴스로 접속
* Remote Desktop File을 다운로드해 접속할 수도 있음.

#### Windows에서 웹서버 사용
* 윈도우 서버는 기본적으로 웹서버가 내장되어 있음.
  * IIS (Internet Information Services)
* Server Manager -> Manage -> Add Roles and Features
  * Server Roles 에서 IIS에 체크
* IIS 실행 후 WIN-xx... -> Sites -> Default Web Site -> Explore 를 통해 서버 root 폴더에 접근 가능

## AMIs (Amazon Machine Image)
* 컴퓨터의 상태를 얼려서 보관해놓은 것이라고 생각해도 됨.
* Instance -> Create Image를 통해 저장장치에 Image를 저장할 수 있음.
  * Image를 생성하게 되는 동안 인스턴스는 잠깐 멈춤.
* Image -> Launch를 통해 Image로 인스턴스를 생성할 수도 있음.
* 백업 등의 용도로 사용 가능.

## AWS Marketplace
* 다른 사람이 만들어놓은 AMI를 통해 인스턴스를 생성할 수도 있음.
* AWS Marketplace 검색해서 찾고자 하는 AMI 선택
  * ex) WordPress powered by Bitnami (HVM)
* 다른 사람이 만든 AMI를 사용할 경우 Image 제작자에게 값을 지불해야하는 경우도 있음.
* 인스턴스 생성이 되면, 메일 등에서 AMI Usage Instruction 링크에 접속할 수 있음.
  * Instance, Application, Database 등에 사용되는 username, password를 찾는 방법에 대한 설명이 있음.

## Scalability
* 클라우드 컴퓨터의 핵심적인 아이디어 : 가상화, 종량제
  * 대규모의 컴퓨팅 파워, 자원 절약
  * EC2 인스턴스의 타입을 선택한다는 것 = scale이 정해져있는 물리적 기계를 쪼개거나 합쳐서 저렴하거나 감력한 컴퓨터를 만드는 방식
  * 여러 대의 컴퓨터를 병렬로 연결하는 ELB
* Scalability : 수요 변화에 따른 탄력적인 공급 변화 능력
  * 여러 대의 컴퓨터를 자동으로 연결하고 삭제하는 Autoscaling

### Scale up
* 컴퓨터적 수요가 늘어나면, 더 좋은 컴퓨터로 대체하여 업그레이드하는 것

#### 스트레스 테스트
* 웹 서버 위에 Java, Wordpress 등 웹 애플리케이션을 설치하게 되면 서버가 무거워짐.

* 서버
  * 리눅스 인스턴스 접속 후 `top` 명령어로 cpu 상황 모니터링 가능

* 클라이언트
  * `sudo apt-get update`
    * 이 컴퓨터에 설치할 수 있는 목록들을 최신 버전으로 업데이트
  * `sudo apt-get install apache2-utils`
  * `ab` : apache에서 만든 부하 발생기

#### Scale up 하는 법
* 인스턴스를 이미지화 시킨 후, 이미지를 이용해서 더 좋은 인스턴스로 바꿀 수 있음.
* 인스턴스를 멈췄다가 다시 켜면 IP주소와 도메인이 달라진다.
* 따라서 Scale up을 한다고 한다면 이전에 사용하던 IP주소와 도메인으로 인스턴스에 접근할 수 없다.
* Elastic IP
  * 고정 IP주소를 얻기 위해 Elastic IP를 발급받을 수 있음.
  * 실행 중인 인스턴스와 연결된 한 개의 Elastic IP는 무료
  * 인스턴스와 연결시키지 않고 가지고만 있으면 과금 됨.
  * Elastic IP를 통해 Scale up한 새로운 인스턴스에 동일한 IP로 사용자들이 접속하게 할 수 있다.
* 한 개의 컴퓨터를 업그레이드하는 Scale up의 한계의 도달하게 되면?