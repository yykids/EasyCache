## Database > EasyCache > Console User Guide

## 시작하기 Getting Started 

To use EasyCache, you must create replication groups in the first place. 를 사용하려면 가장 먼저 복제 그룹을 생성해야 합니다.

## 복제 그룹 Replication Groups

### 복제 그룹 생성 Creating Replication Groups 

1. On **Console > Database > EasyCache** and의 **Replication Groups복제 그룹**, click 탭에서 **Create 생성**, and 버튼을 누르면 **Create Replication Groups복제 그룹 생성** popup shows. 창이 나타납니다.

![rep_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/rep_create_001.PNG)

2. Enter all requirements on the setting window and click **Create** at the bottom. 설정 창에서 표시된 필수 항목을 모두 입력하고 하단의 **생성** 버튼을 클릭합니다.

    - Name of Replication Group복제 그룹 이름: Enter name of a replication group. 복제 그룹 이름을 입력합니다.
    - Description설명: Enter description of the group. 복제 그룹의 설명을 입력합니다.
    - Service Port 서비스 포트: Enter port number of Redis의 포트 번호를 입력합니다.
      - Setting is available between 10000 and 12000 사이로 설정할 수 있습니다.
    - Version 버전: Select a Redis version to create. 생성할 Redis 버전을 선택합니다.
      - 2020년 6월 현재 5.0.8만 지원합니다. As of June 2020, only 5.0.8 is supported. 
    - Instace Type 인스턴스 타입: Select specifications for the replication group. 복제 그룹의 사양을 선택합니다.
    - Max Memory: Adjust the max memory to prevent memory shortage from synchronization or backup. 최대 메모리를 조정해 동기화나 백업 실행 시 메모리 부족을 예방할 수 있습니다.
      - You may change the volume of max memory for Redis server. 서버에 사용할 최대 메모리의 용량을 변경할 수 있습니다.
      - If required, management volume can be secured. 필요할 때 관리용 메모리의 용량도 유연하게 확보할 수 있습니다.
    - Availability Area 가용성 영역: Select an area in which replication group is to be created. 복제 그룹이 생성될 영역을 선택합니다.
    - Configuration File설정 프로필: Select a configuration file for Redis의 설정 파일을 선택합니다.
      - Provides basic profile. 기본 프로필을 제공합니다.
      - More configuration file can be added for selection. 설정 프로필을 추가해 선택할 수 있습니다.
    - VPC Subnet: 사설(private) 네트워크 통신을 원하는 Compute & Network 서비스의 서브넷을 선택합니다. 선택하지 않으면 기본 네트워크로 설정됩니다.
    - Auto Backup Setting자동 백업 설정: Select to enable auto backup. 자동 백업 사용 여부를 선택합니다.
      - Backup Retention Period 백업 보관 기간: 1일부터 최대 30일까지 보관할 수 있습니다. Available from 1 day up to 30 days
      - Backup Start Time 백업 시작 시간: 백업 시작 시간을 지정합니다. 30분 단위로 지정할 수 있습니다. Specify the start time of backup, by 30-minute interval.
      - Backup Time 백업 소요 시간: 백업 시작 시간부터 지정한 시간 사이의 임의의 시점에 시작합니다. 1시간부터 최대 3시간까지 지정할 수 있습니다. Backup to start at a random point between backup start time and specified time. Available from 1 hour up to 3 hours. 
3. Click **Create 생성** 버튼을 클릭합니다.

4. Check what has been entered and click **Create**. 확인 화면에서 입력한 내용을 확인하고 **생성** 버튼을 클릭합니다.
   Along with a replication group, the master node is created. It takes a few minutes to create.  복제 그룹이 생성되면서 Master 노드가 생성됩니다. 생성될 때까지 몇 분 정도 걸립니다.
   
##### 제약 사항 Constraints 
- 서비스에 치명적인 영향을 줄 수 있는 명령어에 대해서 사용이 제한됩니다. Service is restricted for such commands that may severely impact service.  
- 해당 명령어는 개발자 가이드를 참고 하세요. See developer's guide to find out the commands. 

### 복제(노드 추가) Replication (Adding Nodes) 

Redis가 지원하는 Replica 노드를 만들어 가용성을 높일 수 있습니다. By creating a replica node supported by Redis, availability can be raised. 

1. Replica 노드를 만들려면 원본 복제 그룹을 선택한 후 **노드 추가** 버튼을 클릭합니다. To create a replica node, select an original replication group and click **Add Nodes**. 

![nod_ad_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/rep_node_add_002.PNG)

2. Master 노드가 다운되었는지 판단하기 위해 헬스 체크 응답 대기 시간을 설정할 수 있습니다. 기본값은 3000ms입니다. To see if the master node has gone down, wait time can be set for health check response. Default is 3000ms. 

3. Select an available zone to create a replica node. Selecting a different available zone from the original master node makes it more available.  Replica 노드가 생성될 가용 존을 선택할 수 있습니다. 원본 Master 노드와 다른 가용 존을 선택하면 가용성이 좋습니다.

4. Master 노드의 정보를 확인할 수 있습니다. Find out information of the master node. 

5. Click **Add**, and a replica node is created. 버튼을 누르면 Replica 노드가 생성됩니다.
6. To check information of the node, go to 생성된 노드의 정보는 **Replication Groups복제 그룹 > Node Information노드 정보**에서 확인할 수 있습니다.
   생성 중 자동으로 복제 관계가 설정됩니다. Replication relation is automatically set while it is created. 

Replica 노드는 원본 Master 노드와 동일한 서버 사양입니다. The replica node has the same server specifications as the original master node. 
원본 Master 노드의 크기에 비례하여 Replica 노드 생성 시간이 늘어날 수 있습니다. It may take more time to create a replica node in proportion to the size of the original master node.

##### 제약 사항 Constraints 

- 원본 Master 노드로 1개의 Replica 노드만 만들 수 있습니다. Original master node can create only one replica node.  
- Replica 노드의 Replica 노드는 만들 수 없습니다. A replica node cannot create its own replica node. 

#### High Availability 고가용성(HA)

Standalone의 Master 노드에 Replica 노드를 추가하면 자동으로 고가용성 기능이 설정됩니다. By adding a replica node to the master node of Standalone, high availability is automatically configured. 

- With an auto failover when an error occurs on the master node, downtime can be reduced to the minimum. Master 노드를 감시하여 장애가 발생했을 때 자동으로 장애 조치(failover)를 해 다운타임(downtime)을 최대한 단축할 수 있습니다.
- Failover refers to detecting a master node in which error occurred and automatically promoting a replica node as the master. 장애 조치(failover)는 장애가 발생한 Master 노드를 감지해 자동으로 Replica 노드를 Master 노드로 승격시키는 것을 말합니다.
- You may find events on failure and status of the master or replica node. aster, Replica 노드의 장애 및 상태에 관한 이벤트를 확인할 수 있습니다.

##### 제약 사항 Constraints 

- Replica 노드 추가 시 HA 설정에 실패하면 **복제 그룹 > 기본 정보**에서 **HA 재설정** 버튼을 클릭해 HA를 다시 설정할 수 있습니다. If it fails in high availability configuration while adding a replica node, go to **Replication Groups > Basic Information** and click **Reconfigure HA** to re-configure high availability.  

![rep_ha_error_001.PNG](https://static.toastoven.net/prod_easycache/19.12.06/rep_ha_error_001.PNG)

- With a failover, the existing master node in which error occurred is suspended. When the failed node is deleted, it is changed into a general standalone master node in which high-availability is not enabled. 장애가 발생해 장애 조치를 한 경우, 장애가 발생한 기존 Master 노드는 중지됩니다. 장애가 발생한 노드를 삭제하면 고가용성 기능을 사용하지 않는 일반 Standalone의 Master 노드로 변경됩니다.
- Standalone이 된 Master 노드에 Replica 노드를 추가하면 고가용성 기능을 새로 지정해 사용할 수 있습니다. By adding a replica node to a standalone master node, high availability can be newly specified. 
- 변경된 새 Master 노드는 기존 Master 노드의 접속에 사용되는 도메인을 승계합니다. The newly changed master node inherits the domain applied to access the existing master node. 
- 장애 조치를 수행한 기존의 Master 노드는 ‘이용 불가’ 상태가 되고, 이용 불가 상태에서 새 마스터 노드로만 고가용성 기능이 제공되지 않습니다. The existing node with failover becomes 'Disabled', under which, high availability is not provided to a new master node only. 

### 복제 그룹 수정 Modifying Replication Groups 

1. 원본 복제 그룹을 선택하고 **수정** 버튼을 클릭합니다.Select an original replication group, and click **Modify**. 
2. **복제 그룹 수정** 대화 상자에서 이름과 백업 기간 등을 설정합니다. On the **Modify Replication Group** window, set name and backup period. 

![rep_mo_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/rep_modify_002.PNG)

- Name of Replication Group복제 그룹 이름: Name of a replication group can be changed. 복제 그룹 이름을 변경할 수 있습니다.
- Description설명: Description of a replication group can be changed. 복제 그룹 설명을 변경할 수 있습니다.
- Configuration Profile설정 프로필: Redis setting can be changed. 설정을 변경할 수 있습니다.
- Max Memory: Volume of the maximum memory for usage can be changed. 사용할 최대 메모리의 용량을 변경할 수 있습니다.
- Master Down Timer 마스터 다운 판정 시간 :Wait time can be configured for a health check response to see if the master node is down; default is 3000ms.  Master 노드가 다운되었는지 판단하기 위해 헬스 체크 응답 대기 시간을 설정할 수 있습니다. 기본값은 3000ms입니다.
- Auto Backup Configuration 자동 백업 설정: Select whether to use auto backup 자동 백업 사용 여부를 선택합니다.
	- Backup Retention Period 백업 보관 기간 : From 1, up to 30 days. 1일부터 최대 30일까지 보관할 수 있습니다.
	- Backup Start Time백업 시작 시간 : Specify start time of a backup, by 30-minute interval.  백업 시작 시각을 지정합니다. 30분 단위로 지정할 수 있습니다.
	- Backup Time백업 소요 시간 : Backup to start randomly between start time and a specific time, from 1 hour up to 3 hours. 백업 시작 시각부터 지정한 시간 사이의 임의의 시점에 시작합니다. 1시간부터 최대 3시간까지 지정할 수 있습니다.

3. Check changes and click **Change**. 변경 내용을 확인하고 **변경** 버튼을 클릭합니다.
   Service port, Redis version, Instance type, and Availability area cannot be changed, once they are configured.  한번 설정한 서비스 포트, Redis 버전, 인스턴스 타입, 가용성 영역은 변경할 수 없습니다.
    
### 자동 백업 Auto Backups 

- Memory data (RDB file) is automatically backed up at a specified time once every day. 매일 1회 지정된 시간에 자동으로 메모리 데이터(RDB 파일)를 백업합니다.
- To manage auto backups that are created, go to 생성된 자동 백업은 **Backup백업 **탭에서 관리할 수 있습니다.
- When a replication group bound for backup is deleted, backup files are deleted altogether. 백업 대상이 된 복제 그룹이 삭제되면 백업 파일도 삭제됩니다.
- After a backup retention period, backup files will be automatically deleted. 지정된 백업 보관 기간이 지나면 백업 파일은 자동으로 삭제됩니다.
- Auto backup is to start randomly between start time and backup time. 자동 백업은 백업 시작 시각부터 백업 소요 시간 사이 중 임의의 시점에 시작됩니다.

### 수동 백업 생성 Creating Manual Backups 

복제 그룹의 백업을 원하는 시점에 바로 생성할 수 있습니다. 백업 대상이 된 복제 그룹을 삭제해도 수동 백업 파일은 삭제되지 않습니다. You may create a backup for replication group at a time of choice. Even if a replication group bound for backup is deleted, manual backup files cannot be deleted. 

- 생성된 수동 백업은 **백업**탭에서 관리할 수 있습니다. To manage manual backups that are created, go to **Backup**. 
- 백업이 실행되는 동안 성능이 저하될 수 있습니다. Performance may be degraded while backup is executed. 
- 설정된 백업 보관 기간이 지나면 백업 파일은 자동으로 삭제됩니다. After a backup retention period, backup files will be automatically deleted. 
- 백업 대상인 복제 그룹이 삭제되었다면 기본 정보에서 복제 그룹의 상세 내용은 표시되지 않습니다. If a replication group bound for backup is deleted, details of the group are not displayed on basic information. 

1. 수동 백업 파일을 만들려면  대상 복제 그룹을 선택한 후 **수동 백업** 버튼을 클릭합니다. To create manual backup files, select a replication group and click **Manual Backup**. 
2. **수동 백업** 대화 상자에서 정보를 입력하고 **백업** 버튼을 클릭합니다. Enter information for **Manual Bakup** and click **Backup**.  
    데이터 크기에 비례해 백업 생성 시간이 늘어날 수 있습니다. BAckup 
    ![manual_backup_001.png](https://static.toastoven.net/prod_easycache/20.04.28/rep_manual_backup_001.PNG)

- Backup Name 백업 이름: Enter name of a backup.백업 이름을 입력합니다.
- Description 설명: Enter description of the backup. 백업 설명을 입력합니다.
- Backup Retention Period 백업 보관 기간: 삭제하지 않거나 1일부터 최대 30일까지 보관할 수 있습니다.You may not delete, or retain backup from 1 day, up to 30 days. 

### 도메인 관리 Domain Management 

* 복제 그룹은 같은 서브넷을 사용하는 인스턴스에서 만이 접속할 수 있습니다만, 외부에서 접속을 하고 싶다면 도메인 관리에서 공인 도메인 설정을 하실 수 있습니다. Access to a replication group is available only on instances sharing the same subnet, bu to enable external access, configure public domain setting from domain mnanagement.  

![manual_backup_001.png](https://static.toastoven.net/prod_easycache/20.05.14/rep_public_domain_001.png)

##### 제약 사항 Constraints 

- 수동 백업 생성 중에 중복으로 수동 백업을 할 수 없습니다. 진행 중인 수동 백업이 끝난 뒤 다시 시도해 주세요. Redundant manual backup is unavailable. Try again after current manual backup is done.  
- 자동 백업 시간에 수동 백업을 할 경우 수동 백업이 즉시 생성되지 않고 지연될 수 있습니다. A manual backup execution during auto backup time may be delayed. 

### 복제 그룹 상세 Replication Group Details 

복제 그룹의 기본, 접속, 노드, 모니터링 등의 상세 정보를 확인할 수 있습니다. Details of a replication group, such as basic, access, node, and monitoring, can be found. 

#### 기본 정보 Basic Information 

Select a created replication group, press the **Basic Information** tab and check details of the replication group. 생성된 복제 그룹을 선택하고 **기본 정보** 탭을 누르면 복제 그룹의 상세 정보를 확인할 수 있습니다.

![rep_detail_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/rep_detail_002.PNG)

확인할 수 있는 항목은 다음과 같습니다. Following items can be found. 

- 복제 그룹 이름, 설명, 타입, 버전, 서비스 포트, 인스턴스 타입 Replication group's name, description, type, version, service port, and instance type 
- Max Memory(최대 메모리), 가용성 영역, 설정 프로필 Max memory, Availability area, and configuration profile  
- VPC Subnet(서브넷), 생성일, 자동 백업 설정 VPC subnet, Creation time, auto backup configuration 

Replica 노드가 있을 경우에 확인할 수 있는 항목은 아래와 같습니다. Following items can be found when there is a replica node:

- 마스터 다운 판정 시간 

#### 복제 그룹 접속 Access to Replication Groups 

Select a created replication group and click **Access Information**. 생성된 복제 그룹을 선택하고 **접속 정보** 탭을 누릅니다.

![rep_de_002.PNG](https://static.toastoven.net/prod_easycache/20.04.28/rep_connection_info_kr.png)

- 암호화된 비밀번호를 보려면 **보기** 버튼을 클릭합니다. To see encrypted password, click **View**. 
- **복사**버튼을 누르면 비밀번호를 복사할 수 있습니다. With **Copy**, you can copy password.  
- 접속 가능한 도메인 정보를 확인할 수 있습니다. Check information of domains that can be accessed. 
- 공인 도메인을 설정하지 않은 Redis 노드는 외부에서 접근할 수 없습니다. A Redis node without public domain setting does not allow external access.  
- **복사**버튼을 누르면 도메인을 복사할 수 있습니다. Click **Copy** to copy domain. 
- 접속 정보는 같은 VPC Subnet으로 연결된 노드의 애플리케이션에서 사용할 수 있습니다. Access information is available on an application of node connected with same VPC subnet. 
- 커맨드는 같은 VPC Subnet으로 연결된 노드에서 실행할 수 있습니다 Commands are executable on nodes connected with same VPC subnet. 
- 접속 제어 정보: 복제 그룹에 접근 가능한 사용자를 CIDR 형식으로 입력합니다. Access Control Information: Enter accessible users to a replication group in the CIDR format. 
  - **Show My IP 내 IP 표시**: Displays local IPs in the CIDR format. 로컬 IP가 CIDR 형식으로 표시됩니다.
  - Press **Create 생성** to register. 버튼을 누르면 등록됩니다.
  - Cannot access with IPs that are not registered for access control information. 접속 제어 정보에 등록되지 않은 IP는 접속할 수 없습니다.

#### 노드 정보 Node Information 

생성된 복제 그룹을 선택하고 **노드 정보** 탭을 누르면 복제 그룹 노드의 상세 정보를 확인하고 Replica 노드를 Master 노드로 승격할 수 있습니다.

![rep_node_info_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/rep_node_info_002.PNG)

- Select a replica node and press promotion to master, and the selected replica node can be promoted to the master node. Then, the existing master node is changed to a replica node. Replica 노드를 선택하고 마스터 승격을 누르면, 선택한 Replica 노드를 Master 노드로 승격할 수 있습니다. 이 때 Master 노드는 Replica 노드로 변경됩니다.
- 확인할 수 있는 항목은 다음과 같습니다.Following itesm can be found:
  - 노드 이름, 종류, IP, 가용성 영역, 생성일, 상태 Node name, Type, IP, Availability area, Date of creation, and Status 

## 모니터링 Monitoring 

EasyCache는 Redis 운영 및 사용에 필요한 모니터링 항목을 1분 마다 수집하고 있으며, 수집한 데이터를 차트로 보여줍니다.  EasyCache collects monitoring items that are required to run and use Redis at every minute, and shows such data on a chart. 

![monitoring_001.png](https://static.toastoven.net/prod_easycache/20.05.14/monitoring_001.PNG)

- At every press of the 1-hour or 24-hour button, it is updated as of the current time. 1시간, 24시간 등의 버튼을 누를 때마다 현재 시각을 기준으로 계산하여 갱신합니다.
  - The **1 Hour시간** button shows data collected at every minute on a chart. 버튼은 1분마다 수집한 데이터를 차트에 표시합니다.
  - The **12 Hour시간** button shows 10-minute average value of collected data on a chart.  버튼은 수집한 데이터의 10분간의 평균값을 차트에 표시합니다.
  - The **24 Hour 시간** button shows 10-minute average value of collected data on a chart. 버튼은 수집한 데이터의 10분간의 평균값을 차트에 표시합니다.
  - The **1 Month개월** button shows 6-hour average value of collected data on a chart. 버튼은 수집한 데이터의 6시간의 평균값을 차트에 표시합니다.
  - Click **Specify 지정** to specify search period. 버튼을 클릭해 직접 검색 기간을 지정할 수 있습니다.
- Search period can be specified with clicks on the calendar. 캘린터를 클릭하여 검색 시점을 지정할 수 있습니다.
  - Although a day or time is selected on the calendar, selected search period shall sustsin. 캘린더에서 날짜나 시간을 선택하여도 선택한 검색 기간은 유지됩니다.
- A click on the current time results in the re-search of the period selected as of the current time. 현재 시간 버튼을 클릭하면 현재시간을 기준으로 선택한 검색 기간을 재검색 합니다.
- With an arrow on the right of the current time button, you may search for time before or after, as much as the search period.  현재 시간 버튼의 오른쪽에 있는 화살표 버튼을 이용하여 검색 기간 만큼의 이전 시간, 이후 시간을 검색할 수 있습니다.
- 복제 그룹 드롭다운에서 차트를 표시할 복제 그룹을 선택할 수 있습니다. A replication group can be selected to show charts from the replication group dropdown. 
- 자동 갱신 을 체크하면 60초 마다 차트 데이터를 갱신합니다. With Auto Update enabled, chart data is updated at every 60 seconds. 
- 차트를 클릭하면 차트를 확대하여 표시할 수 있습니다. By clicking on a chart, it is expanded for display.  
- 확대한 차트에서는 통계와 집계 기간을 변경하여 표시할 수 있습니다. On the expanded chart, statistics and collection period may be changed for display. 
  - 통계 방법은 합산 데이터를 표시할 경우 사용되며 집계 기간이 1분이 경우에는 로우 데이터를 사용하므로 통계를 변경하여도 같은 값을 표시하게 됩니다.Statistical method is applied to show accumulated data, and if the collection time is 1 minute, 
- 모니터링 데이터 보존 기간은 1개월입니다.Monitoring data is retained for 1 month. 

![monitoring_002.PNG](https://static.toastoven.net/prod_easycache/20.05.14/monitoring_002.PNG)
- 모니터링 항목은 **필터 조건**에서 원하는 항목만을 표시하도록 선택할 수 있습니다.
- 모니터링 항목은 다음과 같습니다.
  - CPU 이용률 CPU Usage Ratio 
  - 시스템 메모리 System Memory
  - 연결된 클라이언트 Connected Client
  - 블록된 클라이언트 Blocked Client
  - Redis 메모리 사용량 Redis Memory Usage Volum
  - Redis 메모리 사용량(rss) 
  - 메모리 파편화 비율
  - 초당 처리한 명령 수
  - 입력 바이트 
  - 출력 바이트
  - 만료된 키 수(expired)
  - 삭제된 키 수(evicted)
  - 조회 성공 수 
  - 조회 실패 수
  - 조회 성공률
  - 키 개수
  - get 실행 횟수
  - get usec/get calls
  - set 실행 횟수
  - set usec/get calls


## Backups 백업

**백업** 탭에서 백업과 백업 삭제 등을 할 수 있습니다. 백업 중에는 성능이 저하될 수 있으므로 서비스 부하가 적은 시간에 백업하는 것이 좋습니다. On the **Backup** tab, you may back up or delete backup. Since performance may be degraded during a backup, it is recommended to execute backup while service load is low. 

![backup_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/backup_001.PNG)

- 백업 파일을 하나 또는 여러 개 선택해 삭제할 수 있습니다.
- 검색어란에 백업 이름 또는 복제 그룹 이름을 입력하고 **검색**을 누르면 결과가 나타납니다.
- **새로 고침**을 눌러 백업 파일 목록을 갱신해 정보를 확인할 수 있습니다.

- **기본 정보**에서 백업 파일 상세 내용과 복제 그룹의 상세 내용을 확인할 수 있습니다.
![backup_002.PNG](https://static.toastoven.net/prod_easycache/20.04.28/backup_003.PNG)
	- 백업 파일 상세
  백업 이름, 설명, 타입, 캐시 크기, 백업 파일 크기, 백업 보관 기간, 백업 최종 보관일, 상태, 백업 시작 일자
	- 복제 그룹 상세
  복제 그룹 이름, 인스턴스 타입, 버전, Max Memory(최대 메모리), 서비스 포트, VPC Subnet

### 복원Restoration

보관된 백업 파일을 이용해 메모리 데이터를 복원할 수 있습니다. 

1. 복원하려면 백업 파일을 선택하고 **복제 그룹 복원**을 클릭합니다. 복원 시 원본 노드를 변경하지 않고 같은 사양 또는 다른 사양의 새 노드를 생성할 수 있습니다.
   ![restore_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/restore_001.PNG)

2. **복제 그룹 복원** 대화 상자에서 다음 항목을 입력하고 **생성** 버튼을 클릭합니다. 생성된 복제 그룹은 **복제 그룹** 탭에서 확인할 수 있습니다.
  - 백업 이름: 복원할 백업 파일 이름
  - 복제 그룹 이름: 복제 그룹 이름을 입력합니다.
  - 설명: 복제 그룹의 설명을 입력합니다.
  - 서비스 포트: 백업 대상이 된 복제 그룹의 포트가 표시됩니다.
    - Redis의 포트 번호를 변경할 수 있습니다.
    - 10000~12000 사이로 설정할 수 있습니다.
  - 버전: 백업 대상이 된 복제 그룹의 Redis 버전이 표시됩니다.
    - 2020년 6월 현재 5.0.8만 지원합니다.
  - 인스턴스 타입: 백업 대상이 된 복제 그룹의 사양이 표시됩니다.
    - 백업의 캐시 크기보다 큰 인스턴트 타입만 표시됩니다.
    - 인스턴트 타입을 변경할 수 있습니다.
  - Max Memory: 최대 메모리를 조정해 동기화나 백업 실행 시 메모리 부족을 예방할 수 있습니다.
    - Redis 서버에 사용할 최대 메모리의 용량을 변경할 수 있습니다.
    - 최대 메모리 용량을 변경할 수 있어 필요할 때 관리용 메모리의 용량도 유연하게 확보할 수 있습니다.
  - 가용성 영역: 복제 그룹이 생성될 영역을 선택합니다.
  - 설정 프로필: 백업 대상이 된 복제 그룹의 Redis 설정 파일이 표시됩니다.
    - 설정 프로필을 추가해 변경할 수 있습니다.
  - VPC Subnet: 백업 대상이 된 복제 그룹의 VPC Subnet이 표시됩니다.
    - 사설(private) 네트워크 통신을 원하는 Compute & Network 서비스의 서브넷을 선택할 수 있습니다.
  - 자동 백업 설정: 자동 백업 사용 여부를 선택합니다.
    - 백업 보관 기간: 1일부터 최대 30일까지 보관할 수 있습니다.
    - 백업 시작 시간: 백업 시작 시각을 지정합니다. 30분 단위로 지정할 수 있습니다.
    - 백업 지연 시간: 백업 시작 시각부터 지정한 시간 사이의 임의의 시점에 시작합니다. 3시간까지 지정할 수 있습니다.

## 설정 프로필 Configuration Profile 

### 설정 프로필 생성 Creating Configuration Profile

변경이 가능한 Redis의 설정을 프로필 형태로 등록해 관리할 수 있습니다.

1. 프로필로 등록하려면 **프로필 설정** 탭에서 **프로필 생성** 버튼을 클릭합니다.
2. **프로필 생성** 대화 상자에서 프로필 이름, 설명, 프로필 적용 버전을 선택할 수 있습니다. 

![pro_002.PNG](https://static.toastoven.net/prod_easycache/20.05.14/profile_001_ko.png)

3. **상세 설정**을 클릭하여 프로필 설정을 항목 별로 변경 할 수 있습니다. 변경 없이 프로필을 등록하면 기본 설정을 사용합니다.

![pro_003.PNG](https://static.toastoven.net/prod_easycache/20.05.14/profile_003_ko.png)

4. **생성** 버튼을 클릭하여 프로필을 등록할 수 있습니다. 

- 등록한 프로필 정보를 수정하면 이용 중인 노드에도 반영됩니다.

- 등록한 프로필을 삭제할 수 있습니다. 단, 이용 중인 노드가 있는 프로필은 삭제할 수 없습니다.

- 등록한 프로필을 복사하여 사용할 수 있습니다. 또한 복사할때 항목 값을 변경할 수 있습니다.

- 기본 설정 정보가 있는 기본 프로필을 제공합니다.

- 기본 프로필은 수정, 삭제할 수 없습니다.

- 프로필의 상태를 확인할 수 있습니다.

| Status        | Description                                                         |
| ------------ | ------------------------------------------------------------ |
| 정상         | 프로필을 수정, 삭제할 수 있습니다.                           |
| 변경 적용 중 | 프로필을 변경했고 변경 내용을 각 노드에 전파 중인 상태입니다. <br />변경 내용의 전파가 끝나면 상태는 정상으로 변경됩니다. <br />변경 중 상태에서는 복제 그룹을 작성, 수정, 삭제할 수 없습니다. |
| 이용 중      | 프로필을 이용하여 작성, 변경 중인 복제 그룹이 있는 상태입니다. <br />복제 그룹의 작성, 완료 후 상태는 정상으로 변경됩니다. <br />프로필이 이용중인 상태에서는 프로필을 작성, 수정할 수 없습니다. |



### 프로필 상세 Profile Details 

프로필 상세 정보를 확인할 수 있습니다. Profile details can be found. 

![profile_detail_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/profile_002.PNG)

- 프로필 상세 정보
  - 항목 이름
  - 기입 예: 항목의 입력 예시
  - 항목 값: 실제 설정된 값
  - 설명: 항목에 대한 설명
- 프로필 항목
  - hash-max-ziplist-entries
  - hash-max-ziplist-value
  - latency-monitor-threshold
  - list-compress-depth
  - list-max-ziplist-size
  - maxmemory-policy
  - maxmemory-samples
  - set-max-intset-entries
  - slowlog-log-slower-than
  - slowlog-max-len
  - tcp-keepalive
  - timeout
  - zset-max-ziplist-entries
  - zset-max-ziplist-value
  - replica-ignore-maxmemory (redis 5.0 추가)
  - lazyfree-lazy-eviction (redis 5.0 추가)
  - lazyfree-lazy-expire (redis 5.0 추가)
  - lazyfree-lazy-server-del (redis 5.0 추가)
  - repl-backlog-size (redis 5.0 추가)
  - stream-node-max-bytes (redis 5.0 추가)
  - stream-node-max-entries (redis 5.0 추가)
  - client-query-buffer-limit (redis 5.0 추가)
  - proto-max-bulk-len (redis 5.0 추가)

## 알람 Alarm

EasyCache에서는 원하는 리소스에서 발생하는 특정 이벤트의 알림을 수신 그룹에 전달할 수 있습니다.

![eve_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/alarm_001.PNG)

### 알람 규칙 Alarm Rules 

알람 발생 조건과 대상, 수신 그룹을 지정합니다.
1. 원하는 알림을 설정하려면 **알림** 탭에서 **알람 규칙 생성** 버튼을 클릭합니다.

2. **알람 규칙 생성** 대화 상자에서 알람 발생 조건과 알람을 수신할 수신 그룹을 지정합니다.
![eve_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/alarm_002.PNG)

3. 알람 발생 조건에는 **메트릭 조건**과 **이벤트 조건**, 2가지가 있습니다.

- **메트릭 조건**: 캐시 인스턴스에서 수집한 각종 성능 지푯값(모니터링 항목 참조)을 이용해 알람 조건을 지정하며 다음과 같은 조건을 지정할 수 있습니다.
  - 메트릭 이름, 연산자, 집계의 종류, 평가의 빈도, 임곗값
- **이벤트 조건**: 서비스 내에서 발생하는 모든 이벤트 중에서 알람을 받고 싶은 이벤트(이벤트 항목 참조)를 지정할 수 있습니다.

4. **수신 그룹 보기**을 클릭해 수신 그룹을 확인 또는 추가할 수 있습니다.

5. 작성한 알람 규칙은 기본적으로는 모든 복제 그룹이 대상입니다. 특정 복제 그룹용으로 알람 규칙을 작성하려면 **대상 복제 그룹**에 복제 그룹을 지정합니다.

6. 설정 후 **생성** 버튼을 클릭합니다.

작성한 알람 규칙은 알람 기능을 사용 안 함으로 변경해 일시적으로 끌 수 있습니다.

### 수신 그룹 Recipient Group 

알림을 받을 수신자를 그룹으로 만들어서 관리할 수 있습니다.

![not_re_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/alarm_004.PNG)

- 수신 그룹을 확인하려면 **수신 그룹 보기** 버튼을 클릭합니다.
- 원하는 수신 그룹이 없다면 **수신 그룹 생성** 버튼을 클릭해 새로운 수신 그룹을 작성합니다.
- 수신 그룹에서 지정할 수 있는 수신인은 프로젝트 멤버로 한정됩니다.
  - TOAST 회원 정보에 등록한 메일 주소와 전화번호로 메일 또는 SMS를 보낼 수 있습니다.
- 알람 규칙에서 사용 중인 수신 그룹을 삭제하면 다른 수신 그룹이 없는 알람 규칙의 경우 더이상 알람을 보내지 않게 되므로 주의해야 합니다.

##### 제약 사항 Constraints 

- 알람 규칙의 대상 복제 그룹에 한 개의 복제 그룹만을 입력하고, 해당 복제 그룹을 복제 그룹 화면에서 삭제한 경우, 알람은 유일한 대상 복제 그룹이 없어져 이후부터는 모든 복제 그룹을 대상으로 인식합니다.
- 알람 규칙의 수신 그룹에 한 개의 수신 그룹만 입력하고, 해당 수신 그룹을 수신 그룹 상세 화면에서 삭제한 경우, 알람은 유일한 수신 그룹이 없어져 이후부터는 알람을 보낼 수 없게 됩니다.
- 복제 그룹 생성의 알람은 대상 복제 그룹이 있어도 모든 복제 그룹이 대상이 되어 알람을 보냅니다.
- 프로젝트에 새로운 사용자를 추가할 경우 수신 그룹의 프로젝트 유저 목록에 동기화되기까지 1시간 정도의 대기 시간이 발생할 수 있습니다.

## 이벤트 Events

1. Select **Event이벤트** 탭을 선택합니다.

2. EasyCache automatically retains significant events occurred at a replication group. 는 복제 그룹에서 발생한 의미 있는 이벤트를 자동으로 남깁니다.

3. Enter a word to search on the search window and click **Search**, and search result shows on the resource name and description of an event.  검색어란에 검색할 단어를 입력하고 **검색** 버튼을 클릭하면 이벤트의 리소스 이름과 설명을 대상으로 검색한 결과가 나타납니다.

![eve_002.PNG](https://static.toastoven.net/prod_easycache/20.04.28/event_001.PNG)

- 시간, 날짜별로 검색할 수 있습니다. Search by time and date is available. 
- 이벤트 데이터 보존 기간은 1개월입니다. Event data can be retained for a month. 
- 이벤트 타입은 어떤 리소스에서 발생한 이벤트인지를 뜻합니다. Event type refers to a resource type from which an event has occurred. 
  - ALL: NODE와 REPLICATION_GROUP 관련된 이벤트입니다. Events that are related to NODE and REPLICATION_GROUP.  
  - NODE: NODE에 관련된 이벤트입니다. Events that are related to NODE.
  - REPLICATION_GROUP: REPLICATION_GROUP에 관련된 이벤트입니다. Events related to REPLICATION_GROUP.
  - PROFILE: PROFILE에 관련된 이벤트입니다. Events related to PROFILE. 

##### 이벤트 항목 Event Item

|Type | Event   | Event Details |
|-----| ------ | ---------------- |
| **Replication Group복제 그룹** | Delete 삭제   | 시작, 실패, 종료 |
|             | 생성   | 시작, 실패, 종료 |
|             |  수정   | 시작, 실패, 종료 |
|             |  재시작 | 시작, 실패, 종료 |
| **공인 도메인** | 설정 | 시작, 실패, 종료 |
|             | 해제 | 시작, 실패, 종료 |
| **Cache Instance 캐시 인스턴스** | 연결 | 성공, 실패 |
| **Node노드** | 삭제 | 시작, 실패, 종료 |
|         | 추가 | 시작, 실패, 종료 |
|         | 마스터 승격 | 시작, 실패, 종료 |
|         | 상태 | 비활성화됨, 활성화됨 |
| **Profile 프로필** | 수정 | 시작, 실패, 종료 |
| **Auto자동 HA** | 삭제 | 시작, 종료 |
|            | 설정 | 시작, 실패, 종료 |
| **Failover 장애 조치(failover)** |  | 성공 |
| **Backup 백업** | 수동 백업 | 시작, 실패, 종료 |
|        | 자동 백업 | 시작, 실패, 종료 |
