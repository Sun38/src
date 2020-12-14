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
