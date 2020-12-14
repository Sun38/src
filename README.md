# 시스템 프로그래밍 기말 프로젝트

[★★★프로젝트 링크★★★]("http://ec2-54-180-29-25.ap-northeast-2.compute.amazonaws.com/") 

## 20185136 선민구
---
## 프로젝트명 : AWS를 활용하여 데이터베이스 서버를 구축하고 wordpress를 설치하여 블로그 만들기
---
## 프로젝트 멤버 이름 : 선민구
---
## 프로젝트 소개 및 개발 내용 소개

요즘 대세인 AWS를 한번 경험 삼아 사용하고 싶었고, 나만의 홈페이지를 만들고 싶었기도 해서, AWS로 서버를 구축하여 wordpress로 직접 홈페이지를 만들기로 했다.

---

## 프로젝트 다이어그램

![image](https://user-images.githubusercontent.com/68503646/102055259-ea487680-3e2d-11eb-996f-edecbfb327af.png)


## 프로젝트 상세 설명

## 1. RDS로 MySQL 데이터베이스를 생성
### 1) MySQL 데이터베이스 생성
![image](https://user-images.githubusercontent.com/68503646/102038252-1eaa3b80-3e0a-11eb-8624-f0ad6e9ff9ae.png)

![image](https://user-images.githubusercontent.com/68503646/102038398-806aa580-3e0a-11eb-8cc8-ae427dbc4082.png)

템플릿을 프리 티어로 지정해주고, 설정에서 식별자와 사용자 이름, 암호를 지정한다.

![image](https://user-images.githubusercontent.com/68503646/102038954-ec014280-3e0b-11eb-8bc5-c05decd4f625.png)

초기 데이터베이스 이름을 wordpress로 설정한다. 이렇게 하면 초기화와 동시에 RDS가 MySQL 인스턴스에서 데이터베이스를 생성한다. 이 데이터베이스 이름은 데이터베이스에 연결할 때 사용한다.

![image](https://user-images.githubusercontent.com/68503646/102039048-1fdc6800-3e0c-11eb-91b9-a9e8f1cc41b3.png)

데이터베이스를 생성해준다.

## 2. EC2 인스턴스 생성
### 1) Amazon Machine Image 선택
![image](https://user-images.githubusercontent.com/68503646/102039539-801fd980-3e0d-11eb-8880-e87fdecde762.png)

AWS 콘솔에서 Amazon EC2로 이동한다. 인스턴스 시작을 클릭하여 인스턴스 생성 마법사를 연다.

![image](https://user-images.githubusercontent.com/68503646/102039567-97f75d80-3e0d-11eb-908e-9e444bf63236.png)

AMI(프리티어)를 선택한다.

### 2) 인스턴스 유형 선택
![image](https://user-images.githubusercontent.com/68503646/102039592-ad6c8780-3e0d-11eb-8d74-3229bc8c10f1.png)

추가 요금이 청구되지 않도록 t2.micro 인스턴스를 선택한다.(매월 750시간 실행 가능)
검토 및 시작 버튼을 클릭하여 몇 가지 구성 단계를 건너뛴다.

### 3) 보안 그룹 구성
![image](https://user-images.githubusercontent.com/68503646/102039624-c5dca200-3e0d-11eb-8dab-3ae23964413f.png)

보안 그룹 편집 링크를 클릭한다.

![image](https://user-images.githubusercontent.com/68503646/102039639-d260fa80-3e0d-11eb-8b98-428f6840b1db.png)

소스를 클릭하여 나의 IP로 변경해준다.

![image](https://user-images.githubusercontent.com/68503646/102039674-e6a4f780-3e0d-11eb-8039-da800e99f1c7.png)

새 규칙을 추가하여 유형을 HTTP로 변경해준다.

![image](https://user-images.githubusercontent.com/68503646/102039705-fa505e00-3e0d-11eb-8cff-c8991439d0bc.png)

### 4) 시작 및 SSH 키 받기
![image](https://user-images.githubusercontent.com/68503646/102039737-0fc58800-3e0e-11eb-8699-c69951ff43f9.png)

시작하기 버튼으로 EC2 인스턴스를 생성한다.

![image](https://user-images.githubusercontent.com/68503646/102039756-1ce27700-3e0e-11eb-8c06-619cf934c38e.png)

키 페어를 새로 생성해주고, 키 페어 다운로드를 클릭하여 .pem 파일을 다운로드한다.
키 페어가 다운로드 되면 인스턴스 시작 버튼을 클릭하여 EC2 인스턴스를 시작한다.

## 3. RDS 데이터베이스 구성
네트워크 보안과 암호 인증 및 승인을 구성한다.

### 1) EC2 인스턴스가 RDS 데이터베이스에 액세스하도록 허용
![image](https://user-images.githubusercontent.com/68503646/102039836-55825080-3e0e-11eb-8e55-b9495d4bedab.png)

앞서 생성한 MySQL 데이터베이스(wordpress)를 클릭한다.

![image](https://user-images.githubusercontent.com/68503646/102039847-629f3f80-3e0e-11eb-9f82-7ee72f0d5490.png)

연결 & 보안 탭에서 VPC 보안 그룹에 나열된 보안 그룹을 클릭한다.

![image](https://user-images.githubusercontent.com/68503646/102039862-6d59d480-3e0e-11eb-981d-809c00c1b0e9.png)

인바운드 탭을 클릭한 후, 편집 버튼을 클릭하여 보안 그룹에 대한 규칙을 변경한다.

![image](https://user-images.githubusercontent.com/68503646/102039884-7a76c380-3e0e-11eb-8541-457713d622a5.png)

기본 보안 그룹은 기본 보안 그룹의 다른 인스턴스에서 발생하는 모든 인바운드 트래픽을 허용하는 규칙이 있다. 그러나 Wordpress EC2 인스턴스는 해당 보안 그룹에 없기 때문에 RDS 데이터베이스에 액세스할 권한이 없다. 
유형 속성을 MYSQL/Aurora로 변경하면 프로토콜과 포트 범위가 적절한 값으로 업데이트 된다.

![image](https://user-images.githubusercontent.com/68503646/102039917-8febed80-3e0e-11eb-89de-b1e85b61e283.png)

Wordpress를 입력해주고, EC2 인스턴스에서 사용한 wordpress 보안 그룹을 클릭한다.
클릭하면 보안 그룹 ID가 채워진다. 이 규칙을 설정하면 MySQL이 해당 보안 그룹이 구성된 모든 EC2 인스턴스에 액세스할 수 있게 된다. 저장 버튼을 클릭한다.

### 2) EC2 인스턴스에 SSH 적용
EC2 인스턴스가 RDS 데이터베이스에 액세스할 수 있게 되었으므로 EC2 인스턴스에 SSH를 적용하고 몇 가지 구성 명령을 실행한다.

EC2 인스턴스 페이지로 이동한 후, EC2 인스턴스를 클릭하고, 인스턴스 설명에 IPv4 퍼블릭 IP를 잘 기억해 둔다. SSH를 인스턴스에 적용할 때 필요하다.

![image](https://user-images.githubusercontent.com/68503646/102039974-b6118d80-3e0e-11eb-83b9-9d94bf006f03.png)

------------------------------------

## ※ PuTTY를 사용하여 Windows에서 Linux 인스턴스에 연결 ※
Windows용 SSH 클라이언트인 PuTTY를 사용하여 EC2 인스턴스에 연결한다. .pem 파일과 퍼블릭 IP 주소가 필요하다.

[참고 링크](https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/putty.html)

![image](https://user-images.githubusercontent.com/68503646/102040207-7008f980-3e0f-11eb-801f-ae1c6095c58f.png)

PuTTY를 설치해준다.

### 1. PuTTYgen을 사용하여 프라이빗 키 변환

![image](https://user-images.githubusercontent.com/68503646/102040253-9dee3e00-3e0f-11eb-8606-2b9e8e0a402b.png)

PuTTY Gen을 실행한 후, Type of key to generate를 RSA로 설정해준다.
Load를 해준 후, .pem 파일을 Load 해준다.

![image](https://user-images.githubusercontent.com/68503646/102040424-194fef80-3e10-11eb-90f2-6bfb6d0e0c3b.png)

Save private key를 클릭하여 PuTTY에서 사용할 수 있는 형식으로 키를 저장한다.

이제 개인 키가 PuTTY에 사용하기에 올바른 형식으로 되어 있으므로 PuTTY의 SSH 클라이언트를 사용하여 인스턴스에 연결할 수 있다.

### 2. Linux 인스턴스에 연결

![image](https://user-images.githubusercontent.com/68503646/102040448-2ff64680-3e10-11eb-93e2-e354dc0413d8.png)

PuTTY를 실행한 후, 다음과 같이 Host Name을 지정해준다. 사용자이름@IPv4주소(Amazon Linux의 경우 "ec2-user"가 사용자 이름에 해당한다)

![image](https://user-images.githubusercontent.com/68503646/102040492-43091680-3e10-11eb-884e-2b7d753dfcc5.png)

Browse를 클릭하여 앞서 저장한 프라이빗 키 파일(.ppk)를 열고 Open을 클릭한다.

![image](https://user-images.githubusercontent.com/68503646/102040554-78156900-3e10-11eb-80e1-742ecb04c071.png)

다음과 같이 성공적으로, 접속했다.

### 3. WinSCP를 사용하여 Linux 인스턴스로 파일 전송

![image](https://user-images.githubusercontent.com/68503646/102040578-8b283900-3e10-11eb-92ea-7cf4a94dbcc7.png)

WinSCP를 실행 후, 호스트 이름에 퍼블릭 IP를 작성해주고, 사용자 이름은 ec2-user로 작성해준다. 로그인 클릭.

![image](https://user-images.githubusercontent.com/68503646/102040640-b14dd900-3e10-11eb-95d4-47df961ec4e7.png)

다음과 같이 왼쪽에는 로컬 시스템, 오른쪽은 Linux 인스턴스가 위치함을 알 수 있다.

-----------------------------

### 3) 데이터베이스 사용자 생성

```bash
sudo yum install -y mysql
```
mysql 클라이언트 설치

![image](https://user-images.githubusercontent.com/68503646/102040750-0558bd80-3e11-11eb-9169-ad2f28d9762c.png)

AWS 콘솔에서 RDS 데이터베이스 세부 정보의 연결 및 보안 섹션에서 엔드포인트의 호스트 이름을 찾는다.

```bash
export MYSQL_HOST=<your-endpoint>
```
터미널에서 다음의 명령어를 입력하여 MySQL 호스트에 대한 환경 변수를 설정한다. "your-endpoint"는 RDS 인스턴스의 호스트 이름으로 대체한다.

```bash
mysql --user=<user> --password=<password> wordpress
```
다음에는 터미널에서 다음의 명령어를 실행하여 MySQL 데이터베이스에 연결한다. “user” 및 “password”는 RDS 데이터베이스를 생성할 때 구성한 마스터 사용자 이름과 암호로 대체한다.

![image](https://user-images.githubusercontent.com/68503646/102040878-5b2d6580-3e11-11eb-80b9-eb79b777b625.png)

다음과 같이 성공적으로 MySQL 데이터베이스에 연결된 것을 알 수 있다.

마지막으로 WordPress 애플리케이션의 데이터베이스 사용자를 생성하고 “wordpress” 데이터베이스에 액세스할 권한을 부여한다.

```bash
CREATE USER 'wordpress' IDENTIFIED BY 'wordpress-pass';
GRANT ALL PRIVILEGES ON wordpress.* TO wordpress;
FLUSH PRIVILEGES;
Exit
```

터미널에서 다음과 같은 명령을 수행한다.

이번에는 RDS 데이터베이스의 네트워크 및 암호 보안을 구성하는 방법을 했다. 

## 4. EC2에서 WordPress 구성
### 1) Apache 웹 서버 설치
WordPress를 실행하려면 EC2 인스턴스에서 웹 서버를 실행해야 한다.
```bash
sudo yum install -y httpd
```
다음의 명령어를 실행하여 EC2 인스턴스에 Apache를 설치해준다.

![image](https://user-images.githubusercontent.com/68503646/102041092-d98a0780-3e11-11eb-94e7-8a95fbcd28cc.png)

인스턴스 페이지의 세부 정보 탭의 퍼블릭 IPv4 DNS를 찾고, 웹 브라우저에 그 값을 입력한다.

![image](https://user-images.githubusercontent.com/68503646/102041113-e6a6f680-3e11-11eb-9293-82339ae4fa6e.png)

다음과 같이 Apache 테스트 페이지가 표시된다.
이제 wordpress를 다운로드하고 구성해야 한다.

### 2) WordPress 다운로드 및 구성
WordPress 소프트웨어를 설치하고 구성을 설정한다.
```bash
wget https://wordpress.org/latest.tar.gz
tar -xzf latest.tar.gz
```
먼저, 터미널에서 다음의 명령어로 소프트웨어를 다운로드하고 압축을 해제한다.

![image](https://user-images.githubusercontent.com/68503646/102041207-2077fd00-3e12-11eb-92b4-0ca5a2c260af.png)

ls를 입력하면 tar 파일과 압축이 해제된 내용이 들어 있는 wordpress라는 디렉토리가 보인다.

```bash
cd wordpress
cp wp-config-sample.php wp-config.php
```
다음 명령을 사용하여 디렉토리를 wordpress로 변경하고 기본 구성 파일의 사본을 생성한다.

```bash
nano wp-config.php
```
다음 명령을 실행하여 nano 편집기로 wp-config.php 파일을 연다.

다음 행을 변경하여 데이터베이스 구성을 편집한다.
```bash
// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define( 'DB_NAME', 'database_name_here' );

/** MySQL database username */
define( 'DB_USER', 'username_here' );

/** MySQL database password */
define( 'DB_PASSWORD', 'password_here' );

/** MySQL hostname */
define( 'DB_HOST', 'localhost' );
```
값은 다음과 같이 설정해야 한다.

DB_NAME: “wordpress”

DB_USER: 이전 모듈에서 데이터베이스에 생성한 사용자 이름

DB_PASSWORD: 이전 모듈에서 생성한 사용자의 암호

DB_HOST: 이전 모듈에서 찾은 데이터베이스 호스트 이름

![image](https://user-images.githubusercontent.com/68503646/102041284-62a13e80-3e12-11eb-8eb4-7cc7df7eb711.png)

Ctrl-O를 입력하고 Ctrl-X를 입력하여 nano 편집기에서 빠져나온다.

### 3) WordPress 배포
이 단계에서는 Apache 웹 서버가 Wordpress에 대한 요청을 처리하도록 설정한다.

- Wordpress에 필요한 애플리케이션 종속성을 설치한다. 
```bash
sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2
```

- 다음 명령을 실행하여 올바른 디렉토리로 변경한다.
```bash
cd /home/ec2-user
```
- Wordpress 애플리케이션 파일을 Apache에서 사용하는 /var/www/html 디렉토리에 복사한다.
``` bash
sudo cp -r wordpress/* /var/www/html/
```
- 마지막으로, 변경 사항이 적용되도록 Apache 웹 서버를 다시 시작한다.
```bash
sudo service httpd restart
```

![image](https://user-images.githubusercontent.com/68503646/102041442-d93e3c00-3e12-11eb-8000-90e6788ffdda.png)

이전에 띄운 아파치 웹사이트를 새로 고침하면 다음과 같이 Wordpress 시작 페이지가 표시된다.

![image](https://user-images.githubusercontent.com/68503646/102041467-e78c5800-3e12-11eb-8bf6-dd51c77710cd.png)

이를 통해 Amazon RDS 기반의 완전관리형 MySQL 데이터베이스를 사용하며 퍼블릭 액세스가 가능한 WordPress 사이트가 시작되었다.

## 5. 본격적으로 블로그 꾸미기

[★★★프로젝트 링크★★★]("http://ec2-54-180-29-25.ap-northeast-2.compute.amazonaws.com/") 

먼저, Plugins의 Add new를 클릭한다.

![image](https://user-images.githubusercontent.com/68503646/102041511-01c63600-3e13-11eb-903a-a4ef11f477d6.png)

![image](https://user-images.githubusercontent.com/68503646/102041529-0985da80-3e13-11eb-9d5e-fed90d786cd2.png)

Reset을 검색하여 WP Reset 플러그인을 install 한다.

![image](https://user-images.githubusercontent.com/68503646/102041555-15719c80-3e13-11eb-94c1-a2371a1a4356.png)

Install 하려고 하면 다음과 같은 팝업이 뜨는데 wordpress-config.php 파일을 nano 편집기로 들어가서 
```bash
define( 'FS_METHOD', 'direct' );
```
를 입력하던가, 팝업의 Connection Type에 SSH 옵션이 추가되게 하기 위해서 SSH SFTP Updater Support 라는 플러그인을 WordPress 플러그인 사이트에서 수동으로 직접 설치하는 등, 여러 가지 방법이 있지만, 모든 방법이 통하지 않았다.

그래서 수동으로 필요한 플러그인을 설치하기로 했다.

우선, wp-reset를 검색한 후, more details로 들어가서 홈페이지에서 직접 다운받아서 winscp를 사용하여 로컬에서 ec2 인스턴스의 /var/www/html/wp-content/plugins 에 붙여 넣었다.

![image](https://user-images.githubusercontent.com/68503646/102041873-e7d92300-3e13-11eb-8b08-97f92b320e17.png)

그 후, 다음의 명령어를 통해 압축을 해제하였다.

![image](https://user-images.githubusercontent.com/68503646/102041900-f9222f80-3e13-11eb-9654-f9af2deef1cc.png)

![image](https://user-images.githubusercontent.com/68503646/102041928-02ab9780-3e14-11eb-9cb5-20ea5a48349a.png)

압축이 풀린 wp-reset 플러그인을 하위 디렉토리 및 파일을 포함하여 소유자를 ec2-user로 변경해 준다.

![image](https://user-images.githubusercontent.com/68503646/102041972-13f4a400-3e14-11eb-8d9c-c922ff5ebecf.png)

복사한 압축 파일은 삭제한다.

![image](https://user-images.githubusercontent.com/68503646/102041997-21119300-3e14-11eb-9f65-d5733e90f802.png)

대시보드로 돌아와서 installed Plugins에 WP Reset이 있음을 확인하고 Active를 한다.

![image](https://user-images.githubusercontent.com/68503646/102042016-2e2e8200-3e14-11eb-873c-fcf0ed3f549c.png)

Tools의 WP Reset을 클릭하고 쭉 내려와서 Site Reset 탭에 reset을 입력하고 Reset Site를 클릭한다.

![image](https://user-images.githubusercontent.com/68503646/102044086-6dab9d00-3e19-11eb-8c3e-81bec6899574.png)

wp-reset 플러그인 설치와 마찬가지로 Reblog 테마를 다운받아 Active 해준다.

![image](https://user-images.githubusercontent.com/68503646/102044112-7f8d4000-3e19-11eb-9211-cfaf4315e967.png)

![image](https://user-images.githubusercontent.com/68503646/102044123-874ce480-3e19-11eb-9a69-db4a8f5b825a.png)

마찬가지로 Elementor 플러그인도 설치해준다.

![image](https://user-images.githubusercontent.com/68503646/102044149-92a01000-3e19-11eb-9885-dea1d62513d0.png)

글을 새로 추가하여 포스트의 제목을 쓰고, Featured Image로 배경 이미지를 넣어주고, 상단의 Edit with Elementor를 클릭한다.

![image](https://user-images.githubusercontent.com/68503646/102044177-a0ee2c00-3e19-11eb-96d6-ce7a3b079fd3.png)

원하는 템플릿을 설정해주고, 이미지와 글 등의 내용을 작성한다.

![image](https://user-images.githubusercontent.com/68503646/102044196-ab102a80-3e19-11eb-8eaf-5d07176ad621.png)

좌측 하단의 Publish로 저장을 하고, 사이트에 재접속하면 다음과 같은 메인 화면이 나온다. 

이로써 AWS로 서버를 개설하여 설치형 wordpress로 블로그를 만들어보았다.

## 필요성 및 활용 방안
전세계의 사이트 중 60~70% 정도는 WordPress로 구현이 되어있다는 말이 있을 정도로 사용 사례가 아주 많다. 

WordPress는 크게 가입형 WordPress와 설치형 WordPress가 있다. 

가입형 WordPress는 일정한 금액을 지불하면 서버나 데이터베이스와 같은 컴퓨터 관련 지식이 없더라도 누구나 손쉽게 쇼핑몰, 블로그 등을 호스팅 할 수 있지만, 홈페이지를 꾸미는데에 자유도의 제약이 있다는 단점이 있다.

이에 반해, 설치형 WordPress는 어느 정도의 컴퓨터 지식이 필요하지만, 인터넷에 올라온 WordPress 설치 메뉴얼과 서버 구축 포스팅을 잘 참고하면 가입형 WordPress보다 훨씬 더 다양하게 자신만의 홈페이지를 꾸밀 수 있다.

또한, 12개월의 프리 티어를 제공하는 AWS, Google Clould, Naver Cloud Platform 등을 사용하면 무료로 일정 사양만큼의 서버 자원을 원하는데로 사용할 수 있다. 또한, 교육자나 학생이라면 학교 메일을 인증하여 최대 300 크레딧을 받을 수 있어서 이러한 것들까지도 사용하면 학부 수준에서는 충분히 자신만의 서버를 구축할 수 있다.

이러한 장점들로 인해, 많은 사람들이 WordPress를 이용하여 쇼핑몰, 블로그 등을 개설한다고 한다.