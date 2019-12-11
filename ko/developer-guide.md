## Database > EasyCache > 개발자 가이드

## Clients 접속

* 같은 VPC Subnet을 이용하는 인스턴스의 애플리케이션에서 접속할 수 있습니다.
* Redis를 기반으로 만든 EasyCache는 다양한 개발 언어를 지원합니다.

### JAVA

* Jedis 는 JAVA용 Redis Client입니다.
* 설치한 필요한 Jar 파일입니다.
    * jedis-2.9.0.jar
    * commons-pool2-2.4.2.jar
* 접속 코드
 ```
 public static void main( String[] args ) {
    Jedis jedis = new Jedis("localhost", 6379);
    jedis.set("foo", "bar");
}
 ```
 
### PHP

* Predis 는 PHP용 Redis Client입니다.
* 접속 코드
```
$client = new Predis\Client('tcp://127.0.0.1:6379');
$client->set('hogehoge','fugafuga');
```
OR
```
$client = new Predis\Client([
    'scheme' => 'tcp',
    'host'   => '192.168.10.33',
    'port'   => 6379,
]);
$client->set('hogehoge','fugafuga');
```

### PYTHON

* redis-py 는 PYTHON용 Redis Client입니다.
* redis-py 는 아래와 같이 설치가 필요합니다.
```
$ pip install redis
```

* 접속 코드
```
import redis

r = r = redis.StrictRedis(host='localhost', port=6379, db=0)
r.set('hoge', 'moge')
```
OR
```
import redis

pool = redis.ConnectionPool(host='localhost', port=6379, db=0)
r = redis.StrictRedis(connection_pool=pool)
r.set('hoge', 'moge')
```

## 인스턴스에서 EasyCache for Redis 서버에 접속

* 같은 VPC Subnet내에서만 Redis 서버에 접속이 가능합니다. 
* 같은 VPC Subnet에 있는 인스턴스를 생성합니다.
* Redis Client를 이용하기 위해서는 각 OS별로 Redis를 설치해야 합니다.
    ```
    CentOS 경우
    yum -y install epel-release   
    yum -y install redis
    ```
* 설치가 완료되면 제대로 설치가 되었는지 확인합니다.
    ```
    redis-cli -v
    ```

* 접속하고자 하는 복제 그룹를 선택하고 상세 정보에서 **접속 정보** 탭을 누룹니다. 
 ![rep_de_005.PNG](https://static.toastoven.net/prod_easycache/19.12.06/rep_connection_info_001.PNG)
* 사설/공인 커맨드중 선택하여 **복사**버튼을 눌러 커맨드를 복사하여 인스턴스의 커맨드 창에 붙여넣기를 합니다.
* Redis 서버에 접속합니다. 
* 패스워드에서 **보기**버튼을 누르면 패스워드가 보여지고 **복사**버튼이 활성화가 됩니다.
* **복사**버튼을 누르면 패스워드를 복사합니다.
* AUTH 커맨드를 이용하여 인증을 합니다.
    * AUTH {복사한 패스워드}
    
## Restricted Redis commands
##### 아래의 명령어를 사용할 경우 서비스에 치명적인 영향을 줄 수 있는 가능성이 있습니다. 사용하지 말아주세요.

* BGREWRITEAOF
* BGSAVE
* CONFIG
* DEBUG
* MIGRATE
* SAVE
* SHUTDOWN
* SLAVEOF
* REPLICAOF
* SYNC

##### key 또는 아이템이 대용량(수십만개 이상)일때 아래와 같은 명령어를 사용할 경우는 성능 저하및 시스템이 멈출 수 있습니다.

* KEYS
* FLUSHALL, FLUSHDB
* Delete Collections
* Get All Collections
