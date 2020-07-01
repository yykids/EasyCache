## Database > EasyCache > Console User Guide

## Getting Started 

To use EasyCache, you must create replication groups in the first place. 

## Replication Groups

### Creating Replication Groups 

1. On **Console > Database > EasyCache** and **Replication Groups**, click **Create**, and **Create Replication Groups** popup shows. 

![rep_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/rep_create_001.PNG)

2. Enter all requirements on the setting window and click **Create** at the bottom.

    - Name of Replication Group: Enter name of a replication group. 
    - Description: Enter description of the group. 
    - Service Port: Enter port number of Redis.
      - Setting is available between 10000 and 12000.
    - Version: Select a Redis version to create. 
      - As of June 2020, only 5.0.8 is supported. 
    - Instance Type: Select specifications for the replication group.
    - Max Memory: Adjust the max memory to prevent memory shortage from synchronization or backup.
      - You may change the volume of max memory for Redis server. 
      - If required, memory volume can be flexibly secured for management. 
    - Availability Area: Select an area in which replication group is to be created. 
    - Configuration Profile: Select a configuration file for Redis.
      - Provides default profile. 
      - More configuration profile can be added for selection. 
    - VPC Subnet: Select a subnet for Compute & Network to allow private network communication; if not, a default network shall be configured. 
    - Auto Backup Setting: Select whether to enable auto backup. 
      - Backup Retention Period: Available from 1 day up to 30 days
      - Backup Start Time: Specify start time of backup, by 30-minute interval.
      - Backup Time: Backup to start randomly between backup start time and specified time. Available from 1 hour up to 3 hours. 
3. Click **Create**.

4. Check what has been entered and click **Create**. 
   Along with a replication group, a master node is created. It takes a few minutes to create.  
   
##### Constraints 
- Service is restricted for such commands that may severely impact service.  
- See developer's guide to find out the commands. 

### Replication (Adding Nodes) 

By creating a replica node supported by Redis, availability can be raised. 

1. To create a replica node, select an original replication group and click **Add Nodes**. 

![nod_ad_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/rep_node_add_002.PNG)

2. To see if the master node has gone down, wait time can be set for health check response. Default is 3000ms. 

3. Select an available zone to create a replica node. By selecting a different available zone from the original master node, more availability can be attained.   

4. Find out information of the master node. 

5. Click **Add**, and a replica node is created.
6. To check information of the node, go to **Replication Groups > Node Information**.
   Replication relation is automatically set while it is created. 

The replica node has the same server specifications as the original master node. 
It may take more time to create a replica node in proportion to the size of the original master node.

##### Constraints 

- An original master node can create only one replica node.  
- A replica node cannot create its own replica node. 

#### High Availability (HA)

By adding a replica node to the master node of Standalone, high availability is automatically configured. 

- By configuring an auto failover, downtime can be reduced to the minimum when an error occurs on the master node. 
- Failover refers to detecting a master node in which error has occurred and automatically promoting a replica node as the master. 
- You may find events on failure and status of the master or replica node. 

##### Constraints 

- If it fails in high availability configuration while adding a replica node, go to **Replication Groups > Basic Information** and click **Reconfigure HA** to re-configure high availability.  

![rep_ha_error_001.PNG](https://static.toastoven.net/prod_easycache/19.12.06/rep_ha_error_001.PNG)

- With a failover, the existing master node in which error occurred is suspended. When the failed node is deleted, it is changed into a general standalone master node in which high-availability is not enabled. 
- By adding a replica node to the standalone master node, high availability can be newly specified. 
- The newly changed master node inherits the domain applied to access the existing master node. 
- The existing node with failover becomes 'Disabled', under which, high availability is not enabled on the new master node only. 

### Modifying Replication Groups 

1. Select an original replication group, and click **Modify**. 
2. On the **Modify Replication Group** window, set name and backup period. 

![rep_mo_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/rep_modify_002.PNG)

- Name of Replication Group: Name of a replication group can be changed. 
- Description: Description of a replication group can be changed. 
- Configuration Profile: Redis setting can be changed. 
- Max Memory: Volume of the maximum memory for usage can be changed. 
- Master Down Timer: Wait time can be configured for a health check response to see if the master node is down; default is 3000ms.  
- Auto Backup Setting: Select whether to use auto backup.
	- Backup Retention Period: From 1 day, up to 30 days. 
	- Backup Start Time: Specify start time of a backup, by 30-minute interval.  
	- Backup Time: Backup to start randomly between start time and a specific time, from 1 hour up to 3 hours. 

3. Check changes and click **Change**. 
   Service Port, Redis Version, Instance Type, and Availability Area cannot be changed, once they are configured.  
    
### Auto Backups 

- Memory data (RDB file) is automatically backed up at a specified time once every day. 
- To manage auto backups that are created, go to **Backup**.
- When a replication group bound for backup is deleted, backup files are deleted altogether. 
- After a backup retention period, backup files will be automatically deleted. 
- Auto backup is to start randomly between start time and backup time. 

### Creating Manual Backups 

You may create a backup for replication group at a time of choice. Even if a replication group bound for backup is deleted, manual backup files cannot be deleted. 

- Manage manual backups that are created on **Backup**. 
- Performance may be degraded while backup is executed. 
- After a backup retention period, backup files will be automatically deleted. 
- If a replication group bound for backup is deleted, details of the group are not displayed for basic information. 

1. To create manual backup files, select a replication group and click **Manual Backup**. 
2. Enter information for **Manual Bakup** and click **Backup**.  
    It may take more time to create a backup in proportion to the size of data.
    ![manual_backup_001.png](https://static.toastoven.net/prod_easycache/20.04.28/rep_manual_backup_001.PNG)

- Backup Name: Enter name of a backup.
- Description: Enter description of a backup.
- Backup Retention Period: You may not delete, or retain backup from 1 day, up to 30 days. 

### Domain Management 

* Access to a replication group is available only on instances sharing the same subnet, but to enable external access, configure public domain setting from domain mnanagement.  

![manual_backup_001.png](https://static.toastoven.net/prod_easycache/20.05.14/rep_public_domain_001.png)

##### Constraints 

- Redundant manual backup is unavailable. Try again after current manual backup is done.  
- Executing a manual backup during auto backup time may cause delays in the backup. 

### Replication Group Details 

Details of a replication group, such as basic, access, node, and monitoring, can be found. 

#### Basic Information 

Select a created replication group, press the **Basic Information** tab and check details of the replication group. 

![rep_detail_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/rep_detail_002.PNG)

Following items can be found. 

- Replication group's name, description, type, version, service port, and instance type 
- Max memory, availability area, and configuration profile  
- VPC subnet, creation date, auto backup configuration 

Following items can be found when there is a replica node:

- Master down timer 

#### Access to Replication Groups 

Select a created replication group and click **Access Information**. 

![rep_de_002.PNG](https://static.toastoven.net/prod_easycache/20.04.28/rep_connection_info_kr.png)

- To see encrypted password, click **View**. 
- With **Copy**, you can copy password.  
- Check accessible domain information.  
- A Redis node without public domain setting does not allow external access.  
- Click **Copy** to copy domain. 
- Access information is available on an application of node connected with same VPC subnet. 
- Commands are executable on nodes connected with same VPC subnet. 
- Access Control Information: Enter accessible users to a replication group in the CIDR format. 
  - **Show My IP**: Displays local IPs in the CIDR format. 
  - Press **Create** to register. 
  - Cannot access with IPs that are not registered for access control information. 

#### Node Information 

Select a created replication group, press **Node Information**, and you can check node details of the replication group and promote a replica node to master node. 

![rep_node_info_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/rep_node_info_002.PNG)

- Select a replica node and press Promote to Master, and the selected replica node can be promoted to the master node. Then, the existing master node is changed to a replica node. 
- Following itesm can be found:
  - Node name, Type, IP, Availability area, Date of creation, and Status 

## Monitoring 

EasyCache collects monitoring items that are required to run and use Redis at every minute, and shows such data on a chart. 

![monitoring_001.png](https://static.toastoven.net/prod_easycache/20.05.14/monitoring_001.PNG)

- With every click of the 1-hour or 24-hour button, it is updated as of the current time. 
  - The **1 Hour** button shows data collected at every minute on a chart. 
  - The **12 Hour** button shows 10-minute average value of collected data on a chart.  
  - The **24 Hour** button shows 10-minute average value of collected data on a chart. 
  - The **1 Month** button shows 6-hour average value of collected data on a chart. 
  - Click **Specify** to specify search period. 
- Search period can be specified with clicks on the calendar. 
  - Although a day or time is selected on the calendar, selected search period sustains. 
- A click on the current time results in the re-search of the period selected as of the current time. 
- With an arrow on the right of the current time button, you may search for time before or after, as much as the search period.  
- A replication group can be selected to show charts from the replication group dropdown. 
- With Auto Update enabled, chart data is updated at every 60 seconds. 
- By clicking on the chart, it is expanded for display.  
- On an expanded chart, statistics and collection period may be changed for display. 
  - Statistical method is applied to show accumulated data, and if the collection time is 1 minute, same value will be displayed even with changed statistics, since low data is applied.  
- Monitoring data can be retained for 1 month. 

![monitoring_002.PNG](https://static.toastoven.net/prod_easycache/20.05.14/monitoring_002.PNG)
- In monitoring, you may opt to show selected items only from **Filter Conditions**. 
- Find out the monitoring items as follows: 
  - CPU Usage Ratio 
  - System Memory
  - Connected Client
  - Blocked Client
  - Redis Memory Usage Volume
  - Redis Resident Set Size (rss) 
  - Memory Fragmentation Ratio
  - Command Count per Second 
  - Input Byte
  - Output Byte 
  - Expired Key Count
  - Evicted Key Count
  - Successful Query Count
  - Failed Query Count 
  - Successful Query Rate 
  - Key Count 
  - get execution count 
  - get usec/get calls
  - set execution count 
  - set usec/get calls


## Backups 

On the **Backup** tab, you may back up or delete backups. Since performance may be degraded during a backup, it is recommended to execute backup while service load is low. 

![backup_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/backup_001.PNG)

- You may select one or many backup files to delete. 
- Enter name of a backup or a replication group on the search window, and press **Search** to find the result. 
- With **Refresh**, update the list of backup files and find information.  

- **Basic Information** has details of a backup file or a replication group.  
![backup_002.PNG](https://static.toastoven.net/prod_easycache/20.04.28/backup_003.PNG)
	- Backup File Details 
  Name, Description, or Type of backup, Size of cache or Backup file, Backup retention period, Last retention date, Status, or Backup start date  
	- Replication Group Details 
  Name of replication group, Type or version of instance, Max memory, Service port, and VPC Subnet  

### Restoration

Memory data can be restored by using retained backup files. 

1. To restore, select a backup file and click **Restore Replication Groups**. For restoration, a new node with the same or different specifications can be created without changing the origin node. 
   ![restore_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/restore_001.PNG)

2. On the **Restore Replication Groups** window, enter the following and click **Create**. Find created replication groups on the **Replication Group** tab.  
  - Name of Backup: Backup file name to restore 
  - Name of Replication Group: Enter name of a replication group. 
  - Description: Enter description of replication group.
  - Service Port: Shows the port of a replication group bound for backup. 
    - Port number of Redis can be changed.
    - Available between 10000 and 12000. 
  - Version: Shows the version of Redis of a replication group for backup. 
    - As of June 2020, only 5.0.8 is supported. 
  - Instance Type: Shows the specification of a replication group bound for backup. 
    - Shows instance types that are larger than cache of a backup only.  
    - Instance type can be changed. 
  - Max Memory: Max memory can be adjusted to prevent memory shortage from synchronization or backup. 
    - Volume of the max memory can be changed for Redis server. 
    - Since max memory volume is changeable, management memory can be flexibly secured. 
  - Availability Area: Select an area in which a replication group is to be created.
  - Configuration Profile: Shows Redis configuration files of a replication group bound for backup. 
    - More configuration profile can be added for change.  
  - VPC Subnet: Shows VPC Subnet of a replication group for backup.
    - Select a subnet for Compute & Network to allow private network communication.  
  - Auto Backup Setting: Select whether to enable auto backup.
    - Backup Retention Period: Available from 1 day up to 30 days. 
    - Backup Start Time: Specify start time of backup, by 30-minute interval. 
    - Backup Delay Time: To start randomly between backup start time and specified time. Available up to 3 hours. 
     

## Configuration Profile 

### Creating Configuration Profile

Redis configuration which is available for change can be registered as profile for management. 

1. To register as profile, go to **Profile Setting** and click **Create Profile**. 
2. On the **Create Profile** window, select name, description, and version of a profile.   

![pro_002.PNG](https://static.toastoven.net/prod_easycache/20.05.14/profile_001_ko.png)

3. On **Detail Setting**, you may change each profile item. When profile is registered without change, default setting is applied. 

![pro_003.PNG](https://static.toastoven.net/prod_easycache/20.05.14/profile_003_ko.png)

4. Click **Create** and register profile.  

- Modify registered profile and it is also applied to nodes in service. 

- You may delete a registered profile, unless it has a node in service. 

- You may copy a registered profile for use. Item values may be changed when copied. 

- Basic profile with default setting information is provided. 

- Default profile cannot be modified or deleted. 

- You can check profile status. 

| Status        | Description                                                         |
| ------------ | ------------------------------------------------------------ |
| Normal        | Profile can be modified or deleted.                          |
| Applying Changes | Changed profile and transmitting changes to each node. <br /> Once changes are transmitted, the status is changed to normal. <br /> While change is underway, you cannot create, modify, or delete a replication group. |
| In Service    | Replication group is being created or changed with a profile. <br /> After a replication group is created and completed, the status will be changed to normal. <br /> Profile cannot be created or modified while in service. |



### Profile Details 

Check profile details like below. 

![profile_detail_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/profile_002.PNG)

- Profile Details
  - Item name
  - 기입 예: 항목의 입력 예시
  - 항목 값: 실제 설정된 값
  - 설명: 항목에 대한 설명
- 프로필 항목 Profile items 
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

알람 발생 조건과 대상, 수신 그룹을 지정합니다. Specify conditions, targets, and recipient groups of an alarm. 
1. 원하는 알림을 설정하려면 **알림** 탭에서 **알람 규칙 생성** 버튼을 클릭합니다. To set alarms you need, go to **Alarms** and click **Create Alarm Rules**. 

2. **알람 규칙 생성** 대화 상자에서 알람 발생 조건과 알람을 수신할 수신 그룹을 지정합니다. On the **Create Alarm Rules** window, specify the condition for setting off an alarm and recipient groups. 
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

## Events

1. Select **Event**.

2. EasyCache automatically retains significant events occurred at a replication group. 

3. Enter a word to search on the search window and click **Search**, and search result shows on the resource name and description of an event.  

![eve_002.PNG](https://static.toastoven.net/prod_easycache/20.04.28/event_001.PNG)

- Search by time or date is available. 
- Event data can be retained for a month. 
- Event type refers to a resource type from which an event has occurred. 
  - ALL: Events related to NODE and REPLICATION_GROUP.  
  - NODE: Events related to NODE.
  - REPLICATION_GROUP: Events related to REPLICATION_GROUP.
  - PROFILE: Events related to PROFILE. 

##### Event Items

|Type | Event   | Event Details |
|-----| ------ | ---------------- |
| **Replication Group** | Delete   | Started, Failed, Closed |
|             | Create   | Started시작, Failed, Closed |
|             | Modify   | Started, Failed, Closed |
|             | Restart  | Strated, Failed, Closed |
| **Publicly Credited Domain** | Setting | Started, Failed, Closed |
|             | Cancel | Started, Failed, Closed |
| **Cache Instance** | Connect | Successful, Failed |
| **Node** | Delete | Started, Failed, Closed |
|         | Add  | Started, Failed, Closed |
|         | Promote to Master  | Started, Failed, Closed |
|         | Status | Disabled, Enabled |
| **Profile** | Modify | Started, Failed, Closed |
| **Auto HA** | Delete  | Started, Closed  |
|            | Set | Started, Failed, Closed  |
| **Failover** |  | Successful |
| **Backup** | Manual Backup | Started, Failed, Closed  |
|        | Auto Backup | Started, Failed, Closed |
