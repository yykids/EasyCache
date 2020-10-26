## Database > EasyCache > Console User Guide

## Getting Started

To enable EasyCache, it is required to create a replication group first. 

## Replication Groups

### Create 

1. From **Replication Group** on **Console > Database > EasyCache**, click **Create** and a popup for **Create Replication Groups** shows.

![rep_001.PNG](https://static.toastoven.net/prod_easycache/20.08.04/rep_create_001.PNG)

2. Enter all requirements on the setting window and click **Create** at the bottom. 

    - Name of Replication Group: Enter name of a replication group. 
    - Description: Enter description of the group.
    - Service Port: Enter port number of Redis. 
      - Setting is available between 10000 and 12000.  
    - Version: Select a Redis version to create. 
      - As of June 2020, only 5.0.8 is supported.
    - Instance Type: Select specifications for the replication group. 
    - Max Memory:  Adjust the max memory to prevent memory shortage from synchronization or backup.
      - You may change the volume of max memory for a Redis server. 
      - If required, memory volume can be flexibly secured for management. 
    - Availability Area:  Select an area to create a replication group. 
    - Configuration Profile: Select a configuration file for Redis.
      - Provides default profile. 
      - More configuration profiles can be added for selection.
    - VPC Subnet: Select a subnet for Compute &  Network to allow private network communication; if not, a default network shall be configured. 
    - Auto Backup Setting: Select whether to enable auto backup. 
      - Backup Retention Period: Available from 1 day up to 30 days.
      - Backup Start Time: Specify start time of backup, by 30-minute interval. 
      - Backup Time: Backup starts randomly between start time and specified time. Available from 1 hour up to 3 hours. 
3. Click **Create**. 

4. Check inputs on the screen and click **Create**. 
   Along with a replication group, a master node is created. It takes a few minutes to create. 
##### Constraints
- Service is restricted for such commands that may severely impact service. 
- See developer's guide to find out the commands. 

### Replicate (Add Nodes)

By creating a replica node supported by Redis, availability can be raised. 

1. To create a replica node, select an original replication group and click **Add Nodes**. 

![nod_ad_001.PNG](https://static.toastoven.net/prod_easycache/20.07.09/rep_node_add_002.PNG)

2. To see if the master node has gone down, set wait time for health check response. Default is 3000ms.  

3. Select an availability area to create a replica node. By selecting a different availability area from the original master node, the availability goes higher. 

4. Find out information of the master node. 

5. Click **Add**, and a replica node is created. 
6. To check information of the node, go to **Replication Groups > Node Information**. 
   Replication relation is automatically set while it is created. 

The replica node has the same server specifications as the original master node. 
It may take more time to create a replica node, in proportion to the size of the original master node. 

##### Constraints 

- An original master node can create only one replica node. 
- A replica node cannot create its own replica nodes under it. 

#### High Availability (HA)

By adding a replica node to the standalone master node, high availability is automatically configured. 

- By setting an auto failover, downtime can be reduced to the minimum when an error occurs on the master node. 
- Failover refers to detecting a master node in which error has occurred and thereby automatically promoting a replica node to the master. 
- You may find events on failure and status of the master or replica node. 

##### Constraints

- If it fails to set up high availability while adding a replica node, go to **Replication Groups > Basic Information** and click **Reconfigure HA** so as to re-configure high availability. 

![rep_ha_error_001.PNG](https://static.toastoven.net/prod_easycache/20.07.09/rep_ha_error_001.PNG)

- With a failover, the existing master node in which error occurred is suspended. When the failed node is deleted, it is changed into a general standalone master node in which high availability is not enabled. 
- By adding a replica node to the standalone master node, high availability can be newly specified. 
- The newly changed master node inherits the domain applied to access the existing master node. 
- The existing node with failover becomes 'Disabled', under which, high availability is not enabled only with the new master node.  

### Modify 

1. Select an original replication group, and click **Modify**. 
2. On the popup of **Modify Replication Group**, set name and backup period.  

![rep_mo_001.PNG](https://static.toastoven.net/prod_easycache/20.07.09/rep_modify_002.PNG)

- Name of Replication Group: Name of a replication group can be changed. 
- Description: Description of a replication group can be changed. 
- Configuration Profile: Redis setting can be changed. 
- Max Memory: Volume of the maximum memory for usage can be changed. 
- Master Down Time: Wait time can be configured for a health check response to see if the master node is down; default is 3000ms. 
- Auto Backup Setting: Select whether to use auto backup. 
	- Backup Retention Period: From 1 day, up to 30 days
	- Backup Start Time: Specify start time of a backup, by 30-minute interval.
	- Backup Time: Backup to start randomly between start time and a specific time, from 1 hour up to 3 hours. 

3. Check changes and click **Change**. 
    Service port, Redis Version, Instance Type, and Availability Area cannot be changed, once they're configured. 
### Auto Backups

- Memory data (RDB file) is automatically backed up at a specific time once every day. 
- To manage auto backups that are created, go to **Backup**. 
- When a replication group bound for backup is deleted, bacup files are deleted altogether. 
- After a backup retention period, backup files will be automatically deleted. 
- Auto backup is to start randomly between start time and backup time. 

### Create Manual Backups 

You may create a backup for replication group at a time of choice. Even if a replication group bound for backup is deleted, manual backup files cannot be deleted. 

- Manage created manual backups from the **Backup** tab. 
- Performance may be degraded while backup is executed. 
- After a backup retention period, backup files will be automatically deleted. 
- If a replication group bound for backup is deleted, details of the group are not displayed for basic information. 

1. To create manual backup files, select a replication group and click **Manual Backup**. 
2. Enter information for **Manual Backup** and click **Backup**. It may take more time to create a backup in proportion to the size of data. 
    ![manual_backup_001.png](https://static.toastoven.net/prod_easycache/20.07.09/rep_manual_backup_001.PNG)

- Backup Name: Enter name of a backup. 
- Description: Enter description of a backup. 
- Backup Retention Period: You may not delete, or retain backup from 1 day, up to 30 days. 

### Manage Domains

* Access to a replication group is available only on instances sharing the same subnet; but to enable external access, configure public domain setting from domain management. 

![manual_backup_001.png](https://static.toastoven.net/prod_easycache/20.07.09/rep_public_domain_001.png)

### Change Instance Types 

* It is available to change the instance type of a node in service.  
* Change of an instance type means upgrading to higher specifications only. 
* While a type change is underway, node is suspended  from service.  
* With the change of instance type, data is reverted to a time of backup, and if backup was not available, data goes back to default.   
* When there's a replica node, failover occurs to change instance type of the master node.  

![instance_type_001.png](https://static.toastoven.net/prod_easycache/20.07.09/rep_instance_type_001.png)

##### Constraints 

- Redundant manual backup is unavailable. Try again after current manual backup is done. 
- Executing a manual backup during auto backup time may cause delays in the backup. 

### Replication Group Details 

Details of a replication group, such as basic, access, node, and monitoring, can be found. 
#### Basic Information  

Select a created replication group, press **Basic Information** and check details of the replication group. 

![rep_detail_001.PNG](https://static.toastoven.net/prod_easycache/20.07.09/rep_detail_002.PNG)

Following items can be found: 

- Name, description, type, version, service port, and instance type of replication group 
- Max memory, availability area, and configuration profile 
- VPC subnet, creation date, and auto backup configuration 

Following items can be found when there's a replica node: 

- Master down timer 

#### Access to Replication Groups 

Select a created replication group and click **Access Information**. 

![rep_de_002.PNG](https://static.toastoven.net/prod_easycache/20.07.09/rep_connection_info_kr.png)

- To see encrypted password, click **View**. 
- Press **Copy** to copy password. 
- Check available domain information. 
- A Redis node without public domain setting does not allow external access. 
- Click **Copy** to copy domain. 
- Access information is available on an application of node connected with same VPC subnet. 
- Commands are executable on nodes connected with same VPC subnet. 
- Access Control Information: Enter accessible users to a replication group in the CIDR format. 
  - **Show My IP**: Displays local IPs in the CIDR format.  
  - Press **Create** to register. 
  - Cannot access with IPs that are not registered for access control information. 

#### Node Information 

Select a created replication group and press **Node Information**, and you can check node details of the replication group and promote a replica node to the master node.  

![rep_node_info_001.PNG](https://static.toastoven.net/prod_easycache/20.07.09/rep_node_info_002.PNG)

- Select a replica node and press Promote to Master, and the selected replica node is promoted to the master node. Then, the existing master node is changed to a replica node. 
- Following items can be found: 
  - Name, type, IP, availability area, date of creation, and status of node 

## Monitoring 

EasyCache collects monitoring items that are required to run and use Redis at every minute and shows such data on a chart. 

![monitoring_001.png](https://static.toastoven.net/prod_easycache/20.05.14/monitoring_001.PNG)

- With every click of the 1-hour or 24-hour button, it is updated as of the current time. 
  - **1 Hour** shows data collected at every minute on a chart. 
  - **12 Hours** shows 10-minute average of collected data on a chart. 
  - **24 Hours** shows 10-minute average of collected data on a chart. 
  - **1 Month** shows 6-hour average of collected data on a chart. 
  - Click **Specify** to specify a search period. 
- Search period can be specified with clicks on the calendar.  
  - Although a day or time is selected on the calendar, selected search period sustains. 
- A click on the current time results in the re-search of a selected period as of the current time. 
- With an arrow on the right of the current time button, you may search for time before or after, as much as the search period. 
- A replication group can be selected to show charts from the replication group dropdown. 
- With Auto Update enabled, chart data can be updated at every 60 seconds. 
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
  - get Execution Count 
  - get usec/get calls 
  - set Execution Count 
  - set usec/get calls


## Backups 

On the **Backup** tab, you may  back up or delete backups. Since performance may be degraded during a backup, it is recommended to execute backup while service load is low. 

![backup_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/backup_001.PNG)

- You may select one or many backup files to delete. 
- Enter name of a backup or a replication group on the search window, and press **Search** to find the result. 
- With **Refresh**, update the list of backup files and find information. 

- **Basic Information** has details of a backup file or a replication group. 
![backup_002.PNG](https://static.toastoven.net/prod_easycache/20.04.28/backup_003.PNG)
	- Backup File Details 
  Name, description, or type of backup; size of cache or backup file, backup retention period, last retention date, status, and backup start date 
	- Replication Group Details 
  Name of replication group, type or version of instance, max memory, service port, and VPC subnet  

### Restore 

Memory data can be restored by using retained backup files. 

1. To restore, select a backup file and click **Restore Replication Groups**. For restoration, a new node with same or different specifications can be created without changing the origin node. 
   ![restore_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/restore_001.PNG)

2. On the **Restore Replication Groups** window, enter the following and click **Create**. Find created replication groups on the **Replication Group** tab. 
  - Name of Backup: Backup file name to restore 
  - Name of Replication Group: Enter name of a replication group. 
  - Description: Enter description of a replication group. 
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
  - Configuration Profile: Shows Redis configuration file of a replication group bound for backup. 
    - Configuration can be changed by adding more profiles. 
  - VPC Subnet: Shows VPC subnet of a replication group for backup. 
    - Select a subnet for Compute & Network to allow private network communication. 
  - Auto Backup Setting: Select whether to enable auto backup. 
    - Backup Retention Period: Available from 1 day up to days 
    - Backup Start Time: Specify start time of backup, by 30-minute interval. 
    - Backup Delay Time: To start randomly between backup start time and specified time. Available up to 3 hours. 

## Configuration Profiles

### Create 

Redis configuration which is available for change can be registered as profile for management. 

1. To register as profile, go to **Profile Configuration** and click **Create Profiles**. 
2. On the popup for **Create Profiles**, select name, description, and version of a profile. 

![pro_002.PNG](https://static.toastoven.net/prod_easycache/20.05.14/profile_001_ko.png)

3. On **Detail Setting**, you many change each profile item. When a profile is registered without changes, default setting is applied. 

![pro_003.PNG](https://static.toastoven.net/prod_easycache/20.05.14/profile_003_ko.png)

4. Click **Create** and register profile. 

- Modify registered profile and it is also applied to nodes in service. 

- You may delete a registered profile, unless it has a node in service. 

- You may copy a registered profile for use. Item values may be changed when copied. 

- Basic profile with default setting information is provided. 

- Default profile cannot be modified or deleted. 

- You can check profile status. 

| Status           | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| Normal           | Profile can be modified or deleted.                          |
| Applying Changes | Changed profile and transmitting changes to each node. <br />Once changes are transmitted, the status is changed to normal. <br />While change is underway, you cannot create, modify, or delete a replication group. |
| In Service       | Replication group is being created or changed with a profile. <br />After a replication group is created and completed, the status will be changed to normal. <br />Profile cannot be created or modified while in service. |



### Profile Details 

Check profile details like below. 

![profile_detail_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/profile_002.PNG)

- Profile Details 
  - Item name 
  - Example of Input: Example of item input
  - Item: Actual set value 
  - Description: Description on items 
- Profile Items 
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
  - replica-ignore-maxmemory (added for redis 5.0)
  - lazyfree-lazy-eviction (added for redis 5.0)
  - lazyfree-lazy-expire (added for redis 5.0)
  - lazyfree-lazy-server-del (added for redis 5.0)
  - repl-backlog-size (added for redis 5.0)
  - stream-node-max-bytes (added for redis 5.0)
  - stream-node-max-entries (added for redis 5.0)
  - client-query-buffer-limit (added for redis 5.0)
  - proto-max-bulk-len (added for redis 5.0)

## Alarms 

EasyCache sends alarms on a particular event occurred from a resource of choice to a recipient group. 

![eve_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/alarm_001.PNG)

### Alarm Rules 

Specify the condition, target, and recipient group for an alarm. 
1. To set alarms you need, go to **Notification** and click **Create Alarm Rules**. 

2. On the popup for **Create Alarm Rules**, specify the condition of sending an alarm and recipient groups. 
![eve_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/alarm_002.PNG)

3. There are two alarm conditions: **Metric Condition** and **Event Condition**. 

- **Metric Condition**: Alarm conditions are specified by using performance indicators (see monitoring items) that are collected from cache instances, like follows: 
  - Metric name, operator, type of collection, frequency of evaluation, and threshold value 
- **Event Condition**: Specify events to be alerted (see event items) out of all events occurred within service. 

4. Click **View Recipient Groups** to check recipient groups or add more. 

5. Alarm rules are basically applied to all replication groups. To create an alarm rule only for a specific replication group, specify the replication group for **Target Replication Groups**. 

6. After setting is done, click **Create**. 

Alarm rules, after created, can be disabled and temporarily turned off. 

### Recipient Groups 

Alarm recipients can be managed under each group. 

![not_re_001.PNG](https://static.toastoven.net/prod_easycache/20.04.28/alarm_004.PNG)

- To check recipient groups, click **View Recipient Groups**. 
- If you don't have a group in need, click **Create Recipient Groups** to create a new group. 
- Available recipients to be specified by each group are confined to project members only. 
  - Messages can be mailed or texted to the email address or phone number registered for TOAST membership. 
- Note that, by deleting a current recipient group for alarm rules, no more alarms are to be sent, if there's no other recipient group. 

##### Constraints 

- If there's only one replication group as the target of alarm rules, and if the group has been deleted from the replication group page, further alarms are to be sent to all replication groups because its only replication group is gone. 
- If there's only one recipient group for alarm rules, and if the group has been deleted from the detail recipient group page, no further alarms can be sent because its only recipient group is gone. 
- Alarms for the creation of a replication group are sent for all replication groups, even if there's a target replication group. 
- If a new user is added to a project, about an hour of wait time may be incurred until the user is synchronized to the list of project users of a recipient group. 

## Events

1. Select **Event**. 

2. EasyCache automatically retains significant events occurred at a replication group. 

3. Enter a word to search on the search window and click **Search**, and search results shows on the resource name and description of an event. 

![eve_002.PNG](https://static.toastoven.net/prod_easycache/20.04.28/event_001.PNG)

- Search by time or date is available. 
- Event data can be retained for a month. 
- Event type refers to a resource type from which an event has occurred. 
  - ALL: Events related to NODE and REPLICATION_GROUP. 
  - NODE: Events related to NODE. 
  - REPLICATION_GROUP: Events related to REPLICATION_GROUP. 
  - PROFILE: Events related to PROFILE. 

##### Event Items 

|Type | Event | Event Details |
|-----| ------ | ---------------- |
| **Replication Group** | Delete | Started, Failed, Closed |
|             | Create | Started, Failed, Closed |
|             | Modify | Started, Failed, Closed |
|             | Restart | Started, Failed, Closed |
|             | Change Group Instance | Started, Failed, Closed |
| **Publicly Credited Domain** | Set | Started, Failed, Closed |
|             | Cancel | Started, Failed, Closed |
| **Cache Instance** | Connect | Successful, Failed |
| **Node** | Delete | Started, Failed, Closed |
|         | Add | Started, Failed, Closed |
|         | Promote to Master | Started, Failed, Closed |
|         | Status | Disabled, Enabled |
|         | Change Node Instance | Started, Failed, Closed |
| **Profile** | Modify | Started, Failed, Closed |
| **Auto HA** | Delete | Started, Closed |
|            | Set | Started, Failed, Closed |
| **Failover** |  | Successful |
| **Backup** | Manual Backup | Started, Failed, Closed |
|        | Auto Backup | Started, Failed, Closed |
