
## Database > EasyCache > 개요
TOAST EasyCache는 Redis(REmote DIctionary Server)를 클라우드 환경에서 제공하는 상품입니다.
간단한 설정으로 고가용성의 Redis 서버를 사용할 수 있습니다.

## 특징 및 기능

*  EasyCache는 사용자의 Compute & Network 상품을 활성화해야만 사용할 수 있습니다.

### 복제 그룹

* 원하는 즉시 생성할 수 있는 Redis 서버입니다. 
* 관리 기능를 사용할 수 있습니다. 

### 이벤트

* 복제 그룹과 노드의 상태 정보를 검색, 확인할 수 있습니다.

### 알림

* 복제 그룹의 이벤트와 복제 그룹의 Monitoring 상태를 통지 받을 수 있습니다.
* 이벤트와 Monitoring 임계치 설정을 관리할 수 있습니다. 

### 프로파일 설정

* Redis 서버의 설정 정보를 프로파일로 관리할 수 있습니다.

### 백업
* 메모리 데이터를 매일 1회, 지정한 시간에 자동으로 백업을 할 수 있습니다. 
* 메모리 데이터를 원하는 시점에 즉시 수동으로 백업을 할 수 있습니다.
* 안전한 외부 스토리지에 저장합니다. 
* 저장된 백업 데이터를 이용하여 언제든 새로운 복제그룹을 생성할 수 있습니다.

## 용어 설명

### 복제 그룹

* 복제 그룹은 Standalone과 Replication 타입으로 제공합니다.
* 서버 스펙은 최소 2GB~64GB 크기의 Memory를 지원합니다.
* TOAST Cloud 의 Compute & Network 상품에서 제공하는 모든 사양의 가상 장비로 복제 그룹을 생성 할 수 있습니다.
* 복제 그룹의 운영체제에 직접 접근 할 수 없으며, 오직 부여된 도메인과 복제 그룹 생성 시 입력하신 port 를 통해서 Redis 서버에 접근 할 수 있습니다.
* 복제 그룹은 사용자의 Compute & Network 상품의 VPC Subnet을 선택해야만 생성할 수 있으며, 이를 통하여 사용자의 Compute & Network 상품의 Instance들과 통신이 가능합니다.
* 복제 그룹은 사용자의 Subnet 이외의 외부 네트워크와 단절되어 있습니다. 외부에서 연결을 원하면 Floating IP 를 붙여야 합니다.
* 만약 Compute & Network 상품을 이용 중이라면, 복제 그룹 생성 시, 연결을 원하시는 subnet 을 설정 할 수 있습니다.
* 연결된 subnet 에 있는 복제 그룹과 인스턴스 간에는 네트워크 연결이 활성화 됩니다.
* Master는 read, write가 가능한 일반적인 인스턴스입니다.
* Replica는 Master를 실시간으로 복제(replication)하는 인스턴스입니다.

### 가용성 영역

* 복제 그룹이 생성될 논리적인 구역을 의미합니다.

### Floating IP

* 외부와 통신하기 위한 유동 IP 입니다.
* Floating IP는 설정하고자 하는 인스턴스와 연결된 사용자 VPC Subnet에 Internet Gateway가 연결되어 있어야 사용이 가능합니다.
* Floating IP 가 연결된 인스턴스의 Redis 는 public 도메인을 통해서 외부에서 접속이 가능합니다.
* Floating IP 는 생성하는 즉시 Redis 인스턴스와는 별도로 요금이 부과됩니다.

### 고가용성(자동HA)

* 고가용성 기능을 사용하면 복제그룹의 master를 감시, 장애를 감지하여 자동으로 장애 조치(failover)를 수행합니다. 서비스의 downtime을 최대한 단축할 수 있습니다. 

### 프로파일

* Redis 서버의 설정입니다.
* Default 프로파일과 유저 프로파일 중 설정할 수 있습니다.
