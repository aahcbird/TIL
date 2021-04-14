# AWS (Amazon Web Services)
## AWS를 사용하는 이유
* AWS란 클라우드 컴퓨팅을 제공하는 서비스
  * 클라우드 컴퓨팅의 사례
    * 대용량 연산이 필요한 작업을 외부 컴퓨터에 요청하고 연산된 결과를 받아서 사용.
## Google OTP 이용하여 MFA 설정
* Identity & Access Management에서 MFA(Multi-factor Authentication) 활성화
  * MFA는 2단계 인증같은 보안 절차임.
* Google OTP를 사용해서 MFA Device 등록

## Region
* AWS의 상품을 제공하는 Regoin(지역)마다 가격이 다르고, AWS를 이용하고자 하는 클라이언트와의 거리에 따라 지연률이 달라진다.
* `cloudping.info`에서 Latency 측정 가능

## Availability Zone
* 하나의 Region에 여러 Availability zone이 존재.
* Availablity zone들은 서로 전용선으로 연결되어 있기 때문에 같은 Region에 속한 가용구역들은 데이터 백업(fault tolerance) 및 이전의 역할을 빠르게 할 수 있다. 