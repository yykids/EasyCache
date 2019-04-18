
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

### Configuration

* Redis 서버의 설정 정보를 프로파일로 관리할 수 있습니다.

### Monitoring
별도의 설치 과정없이 Redis 인스턴스의 하드웨어 및 Redis의 상태를 모니터링할 수 있습니다. 이상 징후에 대해 알림을 설정함으로써 빠르게 대응할 수 있습니다.

## 용어 설명

### 복제 그룹

* 복제 그룹은 Standalone과 Replication 타입으로 제공합니다.
* 복제 그룹은 최소 2GB~256GB 크기의 Memory를 지원합니다.
* TOAST Cloud 의 Compute & Network 상품에서 제공하는 모든 사양의 가상 장비로 복제 그룹을 생성 할 수 있습니다.
* 복제 그룹의 운영체제에 직접 접근 할 수 없으며, 오직 부여된 IP와 복제 그룹 생성 시 입력하신 port 를 통해서 Redis 서버에 접근 할 수 있습니다.
* 복제 그룹은 사용자의 Compute & Network 상품의 VPC Subnet을 선택해야만 생성할 수 있으며, 이를 통하여 사용자의 Compute & Network 상품의 Instance들과 통신이 가능합니다.
* 복제 그룹은 사용자의 Subnet 이외의 외부 네트워크와 단절되어 있습니다. 
* 만약 Compute & Network 상품을 이용 중이라면, 복제 그룹 생성 시, 연결을 원하시는 subnet 을 설정 할 수 있습니다.
* 연결된 subnet 에 있는 복제 그룹과 인스턴스 간에는 네트워크 연결이 활성화 됩니다.

### Availability Zone

* 복제 그룹이 생성될 논리적인 구역을 의미합니다.

### 설정 프로파일

* Redis 서버의 설정입니다.
* Default 프로파일과 유저 프로파일 중 설정할 수 있습니다.
