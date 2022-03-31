

# 키페어 생성

1. AWS Console에 Login 합니다.

2. 서비스 => EC2로 이동

![image-20220308150041344](images/image-20220308150041344.png)



3. 화면 좌측에서 "네트워크 및 보안" => "키 페어" Click

![image-20220308150436606](images/image-20220308150436606.png)



4. "키 페어 생성" Click

![image-20220308150745288](images/image-20220308150745288.png)



5. 이름 : "DBforMSA" 입력 후 "키 페어 생성" Click

![image-20220308150914899](images/image-20220308150914899.png)



6. 자동으로 Private Key인 DBforMSA.cer 혹은 DBforMSA.pem가 개인 Laptop으로 Download됩니다. 

   보안적으로 매우 중요한 파일이기 때문에 안전한 곳에 저장해둡니다.

![image-20220308151225349](images/image-20220308151225349.png)



![image-20220308151639076](images/image-20220308151639076.png)

7. Console에서도 방금 생성된 Key File을 확인합니다.

![image-20220308151833671](images/image-20220308151833671.png)

# 실습 환경 구성

1. CloudFormation 으로 이동

![image-20220207102938764](images/image-20220207102938764.png)



2. "스택 작업" => "새 리소스" 선택

![image-20220207103001305](images/image-20220207103001305.png)



3. "Amazon S3 URL"에 https://shared-kiwony.s3.ap-northeast-2.amazonaws.com/OnPREM4.yml 을 입력 후 "다음" Click

![image-20220207103043253](images/image-20220207103043253.png)



4. "스택 이름"에 "DBforMSA"를 입력, KeyName에 전 Step에서 다운로드 받은 DBforMSA를 선택 후 "다음" Click

![image-20220308160008365](images/image-20220308160008365.png)



5. "AWS CloudFormation에서 사용자 지정 이름으로 IAM 리소스를 생성할 수 있음을 승인합니다"를 체크 후 "스택 생성" Click

![image-20220207103202153](images/image-20220207103202153.png)



6. "이벤트"를 Click하여 CloudFormation Stack이 정상적으로 생성되는지 확인(약 5~10분 소요)

![image-20220207103855903](images/image-20220207103855903.png)



**Stack 생성이 완료되면 "CREATE_COMPLTE"로 표시 됨**

![image-20220207103925083](images/image-20220207103925083.png)



# 실습을 위해 Bastion Host로 접속

### (모든 작업은 Bastion Host를 통해서 이뤄집니다.)



1. CloudFormation => 출력 => IPWindowsPublicIP를 확인

![image-20220207104312974](images/image-20220207104312974.png)



2. "RDP Client"를 사용하여 Bastion 서버에 접속(Windows는 mstsc.exe, MAC은 Microsoft Remote Desktop 사용)

   아직 EC2 인스턴스가 구동 중이라서 접속이 안 될경우 1~2분 후에 다시 접속을 시도합니다.

**Windows Laptop**

![image-20220207104404321](images/image-20220207104404321.png)

![image-20220207105101422](images/image-20220207105101422.png)



**MAC Laptop**

![image-20220207105204837](images/image-20220207105204837.png)



3. Bastion 접속 (Administrator // Octank#1234)

![image-20220207105237250](images/image-20220207105237250.png)



![image-20220207105240390](images/image-20220207105240390.png)



4. 다운로드 받았던 DBforMSA.cer 파일을 개인 Laptop에서 Bastion Server로 복사 합니다.

**MAC Laptop에서 키 파일 복사**

![image-20220308160910914](images/image-20220308160910914.png)



**Windows Laptop에서 키 파일 복사**

![image-20220308161206849](images/image-20220308161206849.png)



**복사한 pem 파일을 Bastion Server의 C:\keys 로 복사합니다.**



![image-20220308161721721](images/image-20220308161721721.png)

![image-20220308161802763](images/image-20220308161802763.png)



5. MobaXterm(SSH Terminal Program)을 실행합니다.

![image-20220308161915397](images/image-20220308161915397.png)





6. "User Sessions"에서 "OracleServer"를 선택 후 "Edit session" 선택

![image-20220207140508645](images/image-20220207140508645.png)



7. Server접속을 위한 pem key 설정
   1. "Advanced SSH Sessting" 선택
   2. "Use private Key" Check
   3. "Key 불러오기" 선택
   4. "C:\keys"로 이동
   5. "DBforMSA.cer"을 선택 후 open
   6. "OK" Click

![image-20220308165918129](images/image-20220308165918129.png)



![image-20220308170039842](images/image-20220308170039842.png)



8. Oracle Server 접속

   **Execute"로 서버 접속**

![image-20220207141433762](images/image-20220207141433762.png)

**Fingerprint Alert Accept Click**

![image-20220207141628256](images/image-20220207141628256.png)



**서버 접속 확인**

![image-20220207141741293](images/image-20220207141741293.png)



# 작업에 필요한 Session 5개를 생성합니다.



1. 작업을 위해 MobaXterm에서 Session을 5개를 만듭니다.

![image-20220207142002894](images/image-20220207142002894.png)



2. Session 5개 Open

![image-20220207142223185](images/image-20220207142223185.png)



3. Session Rename - Oracle, Redis, APP, ApacheBench, extra로 각각 변경

![image-20220207142326844](images/image-20220207142326844.png)

![image-20220207142438065](images/image-20220207142438065.png)



[다음 워크샵으로 - workshop01 ](../workshop01/workshop01.md) 
