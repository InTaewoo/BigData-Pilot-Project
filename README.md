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

## 2-7 카프카 Producer사용
![image](https://user-images.githubusercontent.com/81672260/134909967-3e18052c-d9a7-45d4-bfc7-a8c0ffb1e1e6.png)

## 2-8 카프카 Consumer 사용
- Server02에 새로 SSH터미널을 2개 열어서 각각 카프카 Consumer명령을 실행하여 수신된 메세지를 
![image](https://user-images.githubusercontent.com/81672260/134910652-814a8012-6cdb-485d-847e-7a52c77f1c00.png)

## 2-9 수집 기능 테스트
- SmartCar 로그 시뮬레이터 작동

![image](https://user-images.githubusercontent.com/81672260/134912080-a8e95192-c313-4e9f-8e4f-43fc2164f1c3.png)

## 2-10 카프카 Consumer 작동
![image](https://user-images.githubusercontent.com/81672260/134914858-95492c16-dfd5-4071-be78-90c6546c11b8.png)

## 2-11 카프카 - 플럼 수집기능 점검
![image](https://user-images.githubusercontent.com/81672260/137128450-f3cf2281-4abf-4af5-9a93-253aeb4fae51.png)


# 3. 빅데이터 적재 Ⅰ
- 대용량 로그 파일 적재

## 3-1 SmartCar 에이전트 수정 (Logger Sink -> HDFS Sink)
![image](https://user-images.githubusercontent.com/81672260/135026859-cd95d39f-ef48-48f0-af67-1b437477ec4f.png)


## 3-2 Flume 이벤트 작동, 명령어 확인
![image](https://user-images.githubusercontent.com/81672260/135724949-811bf100-5838-4f17-b094-368fe83dfab6.png)

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

## 4-5 Storm UI 
URL = http://server02.hadoop.com:8088
![image](https://user-images.githubusercontent.com/81672260/135725186-02ac8314-d23c-4422-bc58-718e743fa914.png)

## 4-6 실시간 적재 기능 구현
- 카프카 Spout 기능 구현
- Split Bolt 기능 구현
- HBase Bolt 기능 구현
- 에스퍼 Bolt 기능 구현
- 레디스 Bolt 기능 구현

## 4-7 Hbase 테이블 생성
![image](https://user-images.githubusercontent.com/81672260/137434187-fe12779a-c5ca-48ea-a433-a18eab2bf95e.png)

- 파일럿 프로젝트에서 수집한 운전자의 모든 운행 정보는 Hbase에 적재

## 4-8 Storm Topology배포
![image](https://user-images.githubusercontent.com/81672260/137434489-b50072e9-f051-494d-9772-7fa6bb445338.png)

![image](https://user-images.githubusercontent.com/81672260/135725725-175c08b3-6259-4320-968a-7f8fefb93af0.png)

## 4-9 로그 시뮬레이터 작동
![image](https://user-images.githubusercontent.com/81672260/135627229-28046408-ab6e-477e-8758-d2f3d9dba021.png)

## 4-10 Hbase에 적재 확인
![image](https://user-images.githubusercontent.com/81672260/135725822-17291103-4ea0-4cbd-a77c-21bd09e174bc.png)

## 4-11 운행 기록
- car_number:UOOO7 -> 스마트카 차량 번호가 U0007인 운전자의
- date L 20160301010000 -> 2016년 3월 1일 01시 00분 00초 운행정보는
- speed: 25 -> 시속 25km/h로 주행
- speed_pedal :1 -> 가속 페달을 1단계 진행
- steer_angle : F -> 핸들은 직진중
- break_pedal : 0 -> 브레이크는 밟지 않는 상태
- direct_light : N -> 깜빡이는 켜지 않은 상태
- area_number: D04 -> D04지역을 운행
![image](https://user-images.githubusercontent.com/81672260/135848033-3a162ced-76d3-452f-861b-68cb99fa0d4a.png)

## 4-12 레디스에 적재된 데이터 확인
![image](https://user-images.githubusercontent.com/81672260/137451534-f0e205c4-dcab-434d-993f-71fe44bde43e.png)

## 4-13 레디스 클라이언트 애플리케이션 작동
![image](https://user-images.githubusercontent.com/81672260/137451730-38033cac-2c78-4998-af52-57621be472c7.png)

 차량번호 - 날짜
- K0002-20160103020050
- B0001-20160103015054
- I0010-20160103003056
3대가 과속위반차량으로 발견됌

## 4-12 Eclipse개발환경 구성
![image](https://user-images.githubusercontent.com/81672260/135858249-ef6067fe-78a2-4303-9db6-b3e3eb1a0020.png)

#  빅데이터 탐색
## 5-1 빅데이터 탐색 소개
- 빅데이터 탐색개요
- 빅데이터 탐색에 사용되는 기술(Hive, Spark, Oozie, Hue)
- 탐색 파일럿 실행 1단계 - 탐색 아키텍처
- 탐색 파일럿 실행 2단계 - 탐색 환경 구성
- 탐색 파일럿 실행 3단계 - Hue를 이용한 데이터 탐색
- 탐색 파일럿 실행 4단계 - 데이터 탐색 기능 구현 및 테스트

## 5-2 Hive 설치
![image](https://user-images.githubusercontent.com/81672260/136022517-8b65d0a8-c51d-460b-be4b-421cb3e16ca0.png)

## 5-3 Oozie 설치

## 5-4 Hue 설치
- Hue를 설치하기 위해서는 Python2.7이 설치되어 있어야한다


- psycopg2설치
 ![image](https://user-images.githubusercontent.com/81672260/137485936-bdd0bd24-5812-420b-800b-96c8d2945aac.png)

## 5-5 Spark설치
![image](https://user-images.githubusercontent.com/81672260/137487104-b7af93fc-cfd4-4fcc-be79-35d123b1cd1a.png)

# Hive, Oozie, hue, spark 설치 완료
![image](https://user-images.githubusercontent.com/81672260/137487173-39d783aa-d942-4c3c-8b1f-f85511a47c3d.png)

## 5-6 Hue를 이용해 HDFS에적재된 스마트카 상태 정보 파일 확인
![image](https://user-images.githubusercontent.com/81672260/137487658-81834fb7-e875-44d3-a5f1-c0f937a8e964.png)

![image](https://user-images.githubusercontent.com/81672260/137487708-4af57ce3-fb13-442c-8322-789952bac7fe.png)

## 5-7 HBase에 적재된 데이터 확인
![image](https://user-images.githubusercontent.com/81672260/137487904-9a1af476-ece2-4f45-ae33-5f732f842109.png)

## 5-8 Hive를 이용한 External 데이터 탐색
![image](https://user-images.githubusercontent.com/81672260/137488214-d47c07f1-9a6d-4fe7-9119-df37edbec7d7.png)

## 5-9 스마트카 상태정보 테이블을 조회한 결과
![image](https://user-images.githubusercontent.com/81672260/137488900-6a1b138c-e62a-46fe-b595-326100883ff7.png)

## 5-10 스마트카 상태 정보 테이블에 대한 조건 조회
- 스마트카의 배터리 상태가 '60'이하였던 차량을 찾고 배터리 평균값을 구해본다.
![image](https://user-images.githubusercontent.com/81672260/137489200-b9e75e52-ea28-4de7-8944-d9acf75d9b59.png)

### 하이브의 특징
1. 하이브 쿼리는 맵리듀스로 변환되어 실행
2. 대화형 온라인 쿼리 사용에 부적합
3. 데이터 부분적인 수정(Update/Delete)불가
4. 대규모 병렬분산 처리가 불가능한 경우
5. 트랜잭션 관리 기능이 없어 롤백 처리 불가

## 5-11 Hive를 이용한 HBase 데이터 탐색
![image](https://user-images.githubusercontent.com/81672260/137492147-0ff44e75-322c-4edb-920b-f6e30a1d79d7.png)
* 11번째 줄에서 저장방식을 HBaseStorageHandler로 정의했고, 13번째줄부터 21번째 줄까지는 Hbase의 DriverCarInfo 테이블과 칼럼 패밀리에 해당하는 필드 정보를 하이브 테이블과 매핑에 생성함

## 5-12 Spark를 이용한 추가 데이터셋 탐색
![image](https://user-images.githubusercontent.com/81672260/137494003-6f615bac-6893-4ecc-9e48-33c772e01dfa.png)
* spark-sql로 age가 18이상으로 만들어진 dataframe출력

## 5-13 스마트카 상태 정보 데이터 생성
1. 스마트카 상태 정보 데이터 생성
![image](https://user-images.githubusercontent.com/81672260/137497249-7e5e0c2f-4e2b-47d1-bb31-611e631e08b4.png)

2. 스마트카 상태 정보 데이터 적재
![image](https://user-images.githubusercontent.com/81672260/137497451-5fa34fc0-4904-4a88-be04-344b2a8548a0.png)
* 스마트카 상태정보 데이터를 플럼의 수집 디렉터리로 옮긴다. 플럼이 수집 작업을 시작한다.

3. 스마트카 상태 정보 데이터 적재 확인
![image](https://user-images.githubusercontent.com/81672260/137498363-1be112aa-d6e0-4406-9e13-23796713928c.png)

4. 스마트카 운전자 운행 로그 생성
 ![image](https://user-images.githubusercontent.com/81672260/137498767-ac7ec1f2-eaf3-4fef-8abd-f1cf2b5e89b8.png)
* 플럼, 카프카, 스톰 레디스, Hbase시작

5. 스마트카 운전자의 운행 로그 확인
![image](https://user-images.githubusercontent.com/81672260/137499255-0fdec90d-994b-4c74-b0b5-bb41a7efe549.png)
* 로그는 24시간을 기준으로 지속적으로 생성된다

6. 스마트카 운전자의 운행 데이터 적재 확인
 ![image](https://user-images.githubusercontent.com/81672260/137504824-cb629d6e-eb90-437a-adbd-07b4b80e2427.png)

## 5-14 2021-10-15 날짜로 과속한 스마트카 차량 정보 redis
![image](https://user-images.githubusercontent.com/81672260/137504985-750e01e3-8027-4568-9382-a33e6047589b.png)

