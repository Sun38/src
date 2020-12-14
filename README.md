# 시스템 프로그래밍 기말 프로젝트
## 20185136 선민구
---
## 프로젝트명 : AWS를 활용하여 데이터베이스 서버를 구축하고 wordpress를 설치하여 블로그 만들기
---
## 프로젝트 멤버 이름 : 선민구
---
## 프로젝트 소개 및 개발 내용 소개
### 요즘 대세인 AWS를 한번 경험 삼아 사용하고 싶었고, 나만의 홈페이지를 만들고 싶었기도 해서, AWS로 서버를 구축하여 wordpress로 직접 홈페이지를 만들기로 마음을 먹었다.
---
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

## 1) EC2 인스턴스가 RDS 데이터베이스에 액세스하도록 허용
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

## ※ PuTTY를 사용하여 Windows에서 Linux 인스턴스에 연결 ※
Windows용 SSH 클라이언트인 PuTTY를 사용하여 EC2 인스턴스에 연결한다. .pem 파일과 퍼블릭 IP 주소가 필요하다.

![image](https://user-images.githubusercontent.com/68503646/102040207-7008f980-3e0f-11eb-801f-ae1c6095c58f.png)

PuTTY를 설치해준다.

1. PuTTYgen을 사용하여 프라이빗 키 변환

![image](https://user-images.githubusercontent.com/68503646/102040253-9dee3e00-3e0f-11eb-8606-2b9e8e0a402b.png)
