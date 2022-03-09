 # 실습 환경 접속

1. 전달 받은 접속 정보를 확인 합니다.

![image-20220207095919980](images/image-20220207095919980.png)



**team-hash-login에서 개인별 접속 URL을 확인합니다.**

![image-20220207102643956](images/image-20220207102643956.png)



2. team-hash-login URL로 접속 후 "Accept Terms & Login"을 Click 합니다.

![image-20220207102721865](images/image-20220207102721865.png)



3. 사용자 인증 절차 수행

   **"Email One-Time Password (OTP)"를 Click**

![image-20220207100130480](images/image-20220207100130480.png)

**사전에 등록한 email 주소를 입력 후  "send passcode" click** 

![image-20220207100136517](images/image-20220207100136517.png)

**email로 전송 된 one-time passcode를 확인**

![image-20220207100305293](images/image-20220207100305293.png)



4. Dashboard 접속 확인 및 Team이름 설정, SSH KEY Download

**Team이름 설정**

![image-20220207110206617](images/image-20220207110206617.png)



![image-20220207110257108](images/image-20220207110257108.png)

**Team Name이 변경되지 않았으면, 화면을 새로 고침 한번 합니다.**



**Dashboard 접속 확인 및 "SSH KEY" Click**

![image-20220207102326752](images/image-20220207102326752.png)

**"Download Key"를 Click하여 SSH KEY 다운로드**

![image-20220207102804035](images/image-20220207102804035.png)

**Download된 KEY를 확인**

![image-20220207102443065](images/image-20220207102443065.png)



5. AWS Console Login

**"Open AWS Console"을 Click하여 Login**

![image-20220207102840119](images/image-20220207102840119.png)

**Login 성공 확인 **

![image-20220207102856649](images/image-20220207102856649.png)



# 실습 환경 구성

1. CloudFormation 으로 이동

![image-20220207102938764](images/image-20220207102938764.png)



2. "스택 작업" => "새 리소스" 선택

![image-20220207103001305](images/image-20220207103001305.png)



3. "Amazon S3 URL"에 https://shared-kiwony.s3.ap-northeast-2.amazonaws.com/OnPREM4.yml 을 입력 후 "다음" Click

![image-20220207103043253](images/image-20220207103043253.png)



4. "스택 이름"에 "DBforMSA"를 입력, KeyName에 전 Step에서 다운로드 받은 ee-default-keypair를 선택 후 "다음" Click

![image-20220207103752370](images/image-20220207103752370.png)



5. "AWS CloudFormation에서 사용자 지정 이름으로 IAM 리소스를 생성할 수 있음을 승인합니다"를 체크 후 "스택 생성" Click

![image-20220207103202153](images/image-20220207103202153.png)



6. "이벤트"를 Click하여 CloudFormation Stack이 정상적으로 생성되는지 확인(약 5분 소요)

![image-20220207103855903](images/image-20220207103855903.png)



**Stack 생성이 완료되면 "CREATE_COMPLTE"로 표시 됨**

![image-20220207103925083](images/image-20220207103925083.png)



# 실습을 위해 Bastion Host로 접속

### (모든 작업은 Bastion Host를 통해서 이뤄집니다.)



1. CloudFormation => 출력 => IPWindowsPublicIP를 확인

![image-20220207104312974](images/image-20220207104312974.png)



2. "RDP Client"를 사용하여 Bastion 서버에 접속(Windows는 mstsc.exe, MAC은 Microsoft Remote Desktop 사용)

**Windows Laptop**

![image-20220207104404321](images/image-20220207104404321.png)

![image-20220207105101422](images/image-20220207105101422.png)



**MAC Laptop**

![image-20220207105204837](images/image-20220207105204837.png)



3. Bastion 접속 (Administrator // )

![image-20220207105237250](images/image-20220207105237250.png)



![image-20220207105240390](images/image-20220207105240390.png)



4. 다운로드 받았던 ee-default-keypair.pem(사용중인 Laptop이나 PC에서) 파일을 Bastion Server로 복사 합니다.

**MAC Laptop**

![image-20220207105353640](images/image-20220207105353640.png)



**Windows Laptop**

![image-20220207133650908](images/image-20220207133650908.png)



**복사한 pem 파일을 Bastion Server의 C:\keys 로 복사합니다.**

![image-20220207133804585](images/image-20220207133804585.png)



![image-20220207133837751](images/image-20220207133837751.png)



5. MobaXterm(SSH Terminal Program)을 실행합니다.

![image-20220207134018822](images/image-20220207134018822.png)



6. "User Sessions"에서 "OracleServer"를 선택 후 "Edit session" 선택

![image-20220207140508645](images/image-20220207140508645.png)



7. Server접속을 위한 pem key 설정
   1. "Advanced SSH Sessting" 선택
   2. "Use private Key" Check
   3. "Key 불러오기" 선택
   4. "C:\keys"로 이동
   5. "ee-default-keypair.pem"을 선택 후 open
   6. "OK" Click

![image-20220207141113681](images/image-20220207141113681.png)

![image-20220207141343661](images/image-20220207141343661.png)



8. Oracle Server 접속

   **Execute"로 서버 접속**

![image-20220207141433762](images/image-20220207141433762.png)

**Fingerprint Alert Accept Click**

![image-20220207141628256](images/image-20220207141628256.png)



**서버 접속 확인**

![image-20220207141741293](images/image-20220207141741293.png)





# Workshop1 시작 

```
당신은 Game을 개발하는 회사의 개발자 혹은 DBA입니다. 
현재 Game(World) Server를 포함한 Login, Manager, Log, SHOP, Auction의 기능들은 하나의 RDBMS(Oracle)을 사용하고 있습니다.
당신의 Game은 예상 이상의 놀라운 인기를 얻고 있으며, 이에 따라 Game APP Server와 Game DB Server는 큰 부하가 생기고 있습니다. 

최근 예정되었던 한정 수량 아이템 이벤트에 수 많은 사용자들이 모여들었고, 이로 인해 Main DB의 성능 저하가 발생하였습니다.
인기가 높았던 만큼 사용자들의 불만도 폭증하였고, 당신은 예정되어 있는 두번째 한정 수량 아이템 이벤트 전에 이 문제를 해결해야 합니다.
DB팀과 문제의 원인을 확인한 결과 Oracle DB의 HOT Block에 의한 성능 저하임을 확인하였습니다.

RDBMS을 사용할 경우 특정 DB Block에 동시에 Access가 발생 할 경우 Hot Block이 발생 할 수 있으며,
이러한 문제는 Game내 Item Event뿐 아니라, 통신사 Billing System, Retail Order System등에서 자주 발생 합니다.
이러한 문제를 해결 하기 위하여 Hash-partitioned reverse-index를 이용하는 방법도 있긴 하지만, 해결이 어려운 경우도 있습니다.

이 문제를 해결하기 위하여 당신은 당신의 개발팀과 DBA들과 이야기를 나누었고, HOT Block을 유발하는 부분을 In-Memory DB로 변경하기로 하였습니다. 
```



1. 작업을 위해 MobaXterm에서 Session을 5개를 만듭니다.

![image-20220207142002894](images/image-20220207142002894.png)



2. Session 5개 Open

![image-20220207142223185](images/image-20220207142223185.png)



3. Session Rename - Oracle, Redis, APP, ApacheBench, extra로 각각 변경

![image-20220207142326844](images/image-20220207142326844.png)

![image-20220207142438065](images/image-20220207142438065.png)



4. Oracle Session에서 DB에 접속하여 Data 초기화 수행

```
ec2-user@ip-10-100-1-101:/home/ec2-user> sudo su -
Last login: Tue Jan 25 08:14:31 UTC 2022 on pts/1
root@ip-10-100-1-101:/root# su - oracle
Last login: Mon Feb  7 04:55:48 UTC 2022
oracle@ip-10-100-1-101:/home/oracle> sqlplus oshop/oshop

SQL*Plus: Release 11.2.0.2.0 Production on Mon Feb 7 05:26:23 2022
Copyright (c) 1982, 2011, Oracle.  All rights reserved.

Connected to:
Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production

SQL> @purge
1000 rows updated.
Commit complete.
Table truncated.
SQL> 

```

![image-20220207142734174](images/image-20220207142734174.png)



5. Redis에 접속하여 Data 초기화 수행

```
ec2-user@ip-10-100-1-101:/home/ec2-user> redis-cli
127.0.0.1:6379> auth Welcome1234
OK
127.0.0.1:6379> set prod-001-quantity 10000
OK
127.0.0.1:6379> get prod-001-quantity
"10000"
127.0.0.1:6379>

```

![image-20220207142911631](images/image-20220207142911631.png)



6. Oracle을 Repository로 사용하고 있는 Legacy Game Application을 구동합니다.

```
ec2-user@ip-10-100-1-101:/home/ec2-user> cd workshop1/legacy
ec2-user@ip-10-100-1-101:/home/ec2-user/workshop1/legacy> source bin/activate
(legacy) ec2-user@ip-10-100-1-101:/home/ec2-user/workshop1/legacy> flask run --host=0.0.0.0
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on all addresses.
   WARNING: This is a development server. Do not use it in a production deployment.
 * Running on http://10.100.1.101:5000/ (Press CTRL+C to quit)

```



![image-20220207144437593](images/image-20220207144437593.png)



7. "한정 수량 아이템" 이벤트가 시작되었습니다. apachebench를 사용하여 동시 150 사용자가 3000개의 한정 수량 아이템을 구매하는데 얼마나 걸리는지 확인합니다. 약 100초 정도가 걸렸습니다.

```
ec2-user@ip-10-100-1-101:/home/ec2-user> ab -c 150 -n 3000 http://10.100.1.101:5000/order
This is ApacheBench, Version 2.3 <$Revision: 1430300 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking 10.100.1.101 (be patient)
Completed 300 requests
Completed 600 requests
Completed 900 requests
Completed 1200 requests
Completed 1500 requests
Completed 1800 requests
Completed 2100 requests
Completed 2400 requests
Completed 2700 requests
Completed 3000 requests
Finished 3000 requests


Server Software:        Werkzeug/2.0.2
Server Hostname:        10.100.1.101
Server Port:            5000

Document Path:          /order
Document Length:        4 bytes

Concurrency Level:      150
Time taken for tests:   100.827 seconds
Complete requests:      3000
Failed requests:        0
Write errors:           0
Total transferred:      468000 bytes
HTML transferred:       12000 bytes
Requests per second:    29.75 [#/sec] (mean)
Time per request:       5041.344 [ms] (mean)
Time per request:       33.609 [ms] (mean, across all concurrent requests)
Transfer rate:          4.53 [Kbytes/sec] received


```

![image-20220220022820343](images/image-20220220022820343.png)



8. MobaXterm - APP Session으로 돌아와서 CTRL+C를 눌러서 Legacy Game Application을 중지합니다.

![image-20220207145342620](images/image-20220207145342620.png)



9. Oracle과 Redis의 Data를 초기화 합니다. 위의 Step 4, 5를 수행합니다.

   

   

10. SHOP 의 모듈 중 "한정 수량 아이템" 의 로직을 별도의 Application으로 분리하였고, 사용하는 Repository를 In-Memory REDIS로 변경하였습니다.

```
# LEGACY Order의 Application logic
# Workshop의 진행을 위해 Code에 Credential정보를 넣었습니다. 실제 환경에서는 AWS Secret Manager을 사용하면 Application Code에 사용자의 Credentail을 기술할 필요 없이, 안전하게 사용자 비밀번호를 보호하며 사용 할 수 있습니다.

@app.route('/order', methods=['GET'])
def order():
    conn=cx_Oracle.connect("oshop/oshop@10.100.1.101:1521/XE")
    cursor=conn.cursor() 
    sql="select quantity from HOTDEAL_LIST where PROD_ID = 1 for update"
    output=0
    rs = cursor.execute(sql)
    for record in rs:
        currVal = record[0]
        if(currVal > 0):
            currVal = currVal - 1;
            update_sql = "update HOTDEAL_LIST set quantity="+str(currVal)+" where PROD_ID=1"
            cursor.execute(update_sql);
            insert_sql = "insert into ORDER_HISTORY values (sysdate, 1,1)"
            cursor.execute(insert_sql);
            time.sleep(0.03);
            conn.commit()

            return str(currVal)
        else:
            return "Out Of Stock"

    cursor.close()
    conn.close()
    return "Completed"

```

```
# MSA로 ORDER module만 별도로 분리하고, 한정 수량을 체크하는 부분을 기존 Oracle의 HOTDEAL_LIST Table 대신 REDIS의 prod-001-quantity를 사용하도록 변경
# Workshop의 진행을 위해 Code에 Credential정보를 넣었습니다. 실제 환경에서는 AWS Secret Manager을 사용하면 Application Code에 사용자의 Credentail을 기술할 필요 없이, 안전하게 사용자 비밀번호를 보호하며 사용 할 수 있습니다.

@app.route('/order-redis', methods=['GET'])
def order_redis():
    conn=cx_Oracle.connect("oshop/oshop@10.100.1.101:1521/XE")
    r = redis.Redis(host='localhost',port=6379,password='Welcome1234')
    # You can use following statements when you want to use ElastiCache REDIS
    #r = redis.StrictRedis(host='redis-test2.h3rll4.0001.apn2.cache.amazonaws.com',port=6379,db=0)
    cursor=conn.cursor() 
    currVal = int(r.get('prod-001-quantity'))
    output=0
   # rs = cursor.execute(sql)
    print('START')
    if(currVal > 0):
        #print(currVal)
        #currVal = currVal - 1;
        #r.set('quantity',currVal)
        r.decr('prod-001-quantity',1)
        insert_sql = "insert into ORDER_HISTORY values (sysdate, 1,1)"
        cursor.execute(insert_sql);
        #time.sleep(1);
        time.sleep(0.03);
        conn.commit()

        return str(currVal)
    else:
        print("Out of Stock")
        return "Out Of Stock"

    cursor.close()
    conn.close()
    return "Completed"

```



11. REDIS를 사용하는 MSA Application을 기동

```
(legacy) ec2-user@ip-10-100-1-101:/home/ec2-user/workshop1/legacy>  cd ../msa/
(legacy) ec2-user@ip-10-100-1-101:/home/ec2-user/workshop1/msa> source bin/activate
(msa) ec2-user@ip-10-100-1-101:/home/ec2-user/workshop1/msa> flask run --host=0.0.0.0
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on all addresses.
   WARNING: This is a development server. Do not use it in a production deployment.
 * Running on http://10.100.1.101:5000/ (Press CTRL+C to quit)

```



12. 두번째 "한정 수량 아이템" 이벤트가 시작되었습니다. apachebench를 사용하여 동시 150 사용자가 3000개의 한정 수량 아이템을 구매하는데 얼마나 걸리는지 확인합니다. 약 25초 정도가 걸렸습니다. 4배의 속도 개선이 이뤄졌습니다.

```
ec2-user@ip-10-100-1-101:/home/ec2-user> ab -c 150 -n 3000 http://10.100.1.101:5000/order-redis
This is ApacheBench, Version 2.3 <$Revision: 1430300 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking 10.100.1.101 (be patient)
Completed 300 requests
Completed 600 requests
Completed 900 requests
Completed 1200 requests
Completed 1500 requests
Completed 1800 requests
Completed 2100 requests
Completed 2400 requests
Completed 2700 requests
Completed 3000 requests
Finished 3000 requests


Server Software:        Werkzeug/2.0.2
Server Hostname:        10.100.1.101
Server Port:            5000

Document Path:          /order-redis
Document Length:        12 bytes

Concurrency Level:      150
Time taken for tests:   24.927 seconds
Complete requests:      3000
Failed requests:        0
Write errors:           0
Total transferred:      495000 bytes
HTML transferred:       36000 bytes
Requests per second:    120.35 [#/sec] (mean)
Time per request:       1246.356 [ms] (mean)
Time per request:       8.309 [ms] (mean, across all concurrent requests)
Transfer rate:          19.39 [Kbytes/sec] received

```

![image-20220220022745790](images/image-20220220022745790.png)



## Standalone REDIS가 아닌 Amazon ElatiCache REDIS를 사용 할 수 있습니다. DEV 환경에서는 Standalone REDIS로 개발을 할 수 있지만, 실제 PRODUCTION에서는 HA와 Backup등이 고려되어야 하기 때문에...

