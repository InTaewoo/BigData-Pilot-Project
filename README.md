# BigData-Pilot-Project

## 소프트웨어 아키텍처
![image](https://user-images.githubusercontent.com/81672260/134315284-dd19bf8e-cb57-4799-baca-421209cb98bc.png)

# 1. 서버구성

## 1-1 VirualBox를 통해 Server01, Server02를 구성
![image](https://user-images.githubusercontent.com/81672260/134792405-55d40d90-f322-49b6-8cde-0e40da4b305a.png)


## 1-2 ClouderaManager에 HDFS, YARN, ZooKeeper 설치
![cloudera manager](https://user-images.githubusercontent.com/81672260/134792468-a13e7f1a-5986-432c-947d-16a0dad6a4fb.png)

## 1-3 Server02에 스마트카 로그 시뮬레이터를 업로드
- 스마트카 운전자의 운행정보를 실시간으로 발생시키는 DriverLogMain.java -- (1)
- 스마트카의 정보를 주기적으로 발생시키는 CarLoginMain.java -- (2)
- 우선 DriverLogMain.java를 실행
![image](https://user-images.githubusercontent.com/81672260/134793146-47af9977-d2bb-4085-8440-b3aa03490b02.png)
(1)

![image](https://user-images.githubusercontent.com/81672260/134793283-393f77a1-2746-47c8-a39a-b8084be2fc2b.png)
(2)

# 2. 빅데이터 수집

## 2-1 빅데이터 수집 소개

![image](https://user-images.githubusercontent.com/81672260/134793759-9c7465ce-3ca9-47e3-8219-a4ddf5275ab5.png)


## 2-2 Flume 설치
![image](https://user-images.githubusercontent.com/81672260/134902957-47764937-88f1-4224-b149-be9f2a9ed113.png)

## 2-3 Kafka 설치후 Data Rentention Time을 10분으로 수정
![image](https://user-images.githubusercontent.com/81672260/134903531-a8960b26-9c9a-4a8b-902a-5c8ec470beda.png)

## 2-4 Flume 수집 기능 구현
플럼의 에이전트에서 사용할 Source, Channel, Sink의 각 리소스 변수 정의
![image](https://user-images.githubusercontent.com/81672260/134906130-a842b022-57c3-4d9b-a14e-8dab4d5c27c4.png)

## 2-5 SmaerCar에이전트에 Interceptor 추가
![image](https://user-images.githubusercontent.com/81672260/134906861-5c54f61a-9ae7-4ae3-9e9d-2d28a2703f1a.png)

## 2-6 DriverCarInfo 에이전트 생성
![image](https://user-images.githubusercontent.com/81672260/134907392-e56490b8-0b0f-4283-b754-f3544e824dec.png)

## 2-7 카프카 Producer 사용
![image](https://user-images.githubusercontent.com/81672260/134909967-3e18052c-d9a7-45d4-bfc7-a8c0ffb1e1e6.png)

## 2-8 카프카 Consumer 사용
- Server02에 새로 SSH터미널을 2개 열어서 각각 카프카 Consumer명령을 실행하여 수신된 메세지를 
![image](https://user-images.githubusercontent.com/81672260/134910652-814a8012-6cdb-485d-847e-7a52c77f1c00.png)

## 2-9 수집 기능 테스트
- SmartCar 로그 시뮬레이터 작동

![image](https://user-images.githubusercontent.com/81672260/134912080-a8e95192-c313-4e9f-8e4f-43fc2164f1c3.png)

## 2-10 카프카 Consumer 작동
![image](https://user-images.githubusercontent.com/81672260/134914858-95492c16-dfd5-4071-be78-90c6546c11b8.png)

# 3. 빅데이터 적재 Ⅰ
- 대용량 로그 파일 적재

## 3-1 SmartCar 에이전트 수정 (Logger Sink -> HDFS Sink)
![image](https://user-images.githubusercontent.com/81672260/135026859-cd95d39f-ef48-48f0-af67-1b437477ec4f.png)

# 4. 빅데이터 적재 Ⅱ
- 실시간 로그/분석 적재

## 4-1 Hbase 설치
![image](https://user-images.githubusercontent.com/81672260/135105093-ff6cad5e-23fa-4a7d-97d2-1a387f3b2896.png)

## 4-2 Redis 설치
![image](https://user-images.githubusercontent.com/81672260/135115395-67936f59-5bb5-4320-ba6a-ef14a274d9c1.png)

## 4-3 Redis 원격 접근 허용후 Redis서버에 데이터를 저장/조회

![image](https://user-images.githubusercontent.com/81672260/135116762-2fed2281-bd8a-4479-885a-992bc5d7f206.png)

## 4-4 Storm 설치
- storm-nimbus, storm-supervisor, storm-ui 3개 파일을 설치하고 정상적으로 구동되었는지 확인
![image](https://user-images.githubusercontent.com/81672260/135207767-b7baaf72-c771-4e00-ab15-dc549acde3ac.png)

## 4-5 실시간 적재 기능 구현
- 카프카 Spout 기능 구현
- Split Bolt 기능 구현
- HBase Bolt 기능 구현
- 에스퍼 Bolt 기능 구현
- 레디스 Bolt 기능 구현

## 4-6 Hbase 테이블 생성
- 파일럿 프로젝트에서 수집한 운전자의 모든 운행 정보는 Hbase에 적재

## 로그 시뮬레이터 작동
![image](https://user-images.githubusercontent.com/81672260/135627229-28046408-ab6e-477e-8758-d2f3d9dba021.png)
