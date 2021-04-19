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
4. 

## 가격 정책
* On-demand
  * 필요할 때 켜고 필요없을 때는 끄는 방식
* 예약 인스턴스
  * 기본적으로는 On-demand 방식이나 한 번에 긴 기간을 계약하는 사용자에게 할인을 해주는 정책
* 스팟 인스턴스
  * AWS가 인스턴스 할당을 하면서 어쩔 수 없이 노는 컴퓨터가 발생하게 되는데, 노는 인스턴스의 수가 많아지면 가격이 내려가고, 그렇지 않으면 가격이 올라가는 방식의 가격 정책.