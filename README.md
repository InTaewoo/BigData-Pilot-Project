# BigData-Pilot-Project

## 소프트웨어 아키텍처
![image](https://user-images.githubusercontent.com/81672260/134315284-dd19bf8e-cb57-4799-baca-421209cb98bc.png)


## VirualBox를 통해 Server01, Server02를 구성
![image](https://user-images.githubusercontent.com/81672260/134792405-55d40d90-f322-49b6-8cde-0e40da4b305a.png)


## ClouderaManager에 HDFS, YARN, ZooKeeper 설치
![cloudera manager](https://user-images.githubusercontent.com/81672260/134792468-a13e7f1a-5986-432c-947d-16a0dad6a4fb.png)

## Server02에 스마트카 로그 시뮬레이터를 업로드
- 스마트카 운전자의 운행정보를 실시간으로 발생시키는 DriverLogMain.java -- (1)
- 스마트카의 정보를 주기적으로 발생시키는 CarLoginMain.java -- (2)
- 우선 DriverLogMain.java를 실행
![image](https://user-images.githubusercontent.com/81672260/134793146-47af9977-d2bb-4085-8440-b3aa03490b02.png)
(1)

![image](https://user-images.githubusercontent.com/81672260/134793283-393f77a1-2746-47c8-a39a-b8084be2fc2b.png)
(2)

## 빅데이터 수집 소개
![image](https://user-images.githubusercontent.com/81672260/134793759-9c7465ce-3ca9-47e3-8219-a4ddf5275ab5.png)


## Flume 설치
![image](https://user-images.githubusercontent.com/81672260/134902957-47764937-88f1-4224-b149-be9f2a9ed113.png)

## Kafka 설치후 Data Rentention Time을 10분으로 수정
![image](https://user-images.githubusercontent.com/81672260/134903531-a8960b26-9c9a-4a8b-902a-5c8ec470beda.png)

## Flume 수집 기능 구현
플럼의 에이전트에서 사용할 Source, Channel, Sink의 각 리소스 
![image](https://user-images.githubusercontent.com/81672260/134906130-a842b022-57c3-4d9b-a14e-8dab4d5c27c4.png)
