# 논리 데이터 베이스 설계

## 관계 데이터 베이스 모델

### 순수 관계 연산자
|        연산자         | 설명 |
|:---------------------:|:----:|
|  *셀렉트*<br>(Select)   | 릴레이션 R에서 조건(밑)을 만족하는 튜플 반환     |
| *프로젝트*<br>(Project) | 릴레이션 R에서 주어진 속성들의 값으로만 구성된 튜플 반환<br>**릴레이션 일부 속성만 추출하여 중복 튜플을 제거한 후 새로운 릴레이션 생성 연산자**     |
|    *조인*<br>(Join)     | **공통 속성**을 이용해 R,S 튜플들을 연결해 만들어진 튜플 반환     |
| *디비전*<br>(Division)  | 릴레이션 S의 모든 튜플과 관련있는 R의 튜플 반환     |

### 관계 대수와 관계 해석 비교
> 대절해비

| 구분 | 관계 대수 | 관계 해석 |
| :--: | :--: | :--: |
| 특징 | **절차적 언어**(순서 명시) | 비 절차적 언어(계산 수식의 유연적 사용),<br>**프레디킷 해석** 기반 |
| 목적 | 어떻게 유도하는가? (How) | 무엇을 얻을 것인가 |
| 종류 | 순수 관계 연산자, 일반 집합 연산자 | 튜플 관계 해석, 도메인 관계 해석 |
| 특징 | 릴레이션 조작 위한 연산의 집합으로<br>피연산자와 결과가 모두 릴레이션이다 | 관계 DB에 적용할 수 있도록 설계 |

### 관계 해석 논리 기호
![[Pasted image 20240212234236.png]]


### 카티션 프로덕트
1. 차수는 각 릴레이션의 차수의 합
2. 카디널리티는 는 각 릴레이션 카디널리티의 곱
ex) R 차수가 4, 카디널리티 5 / S 차수가 6, 카디널리티 7 
-> 새로운 릴레이션 차수 (4+6), 카디널리티 (5x7)

### 시스템 카탈로그
1. 일반 사용자는 조회는 가능하나 갱신은 할 수 없음
2. 자료 사전이라고부름 (Data Dictionary)
3. 저장된 정보를 메타 데이터(Metadata)라고 부름
4. INSERT, DELETE, UPDATE 문으로 카탈로그 갱신 허용되지 않음
5. 카탈로그는 DBMS가 스스로 생성하고 유지
6. 사용자가 SQL문을 실행시켜 기본 테이블, 뷰, 인덱스 등에 변화를 주면 시스템이 자동으로 갱신

## 데이터 모델링 및 설계

### 데이터 모델에 표시해야 할 요소
1. 구조 (Structure)
2. 연산 (Operation)
3. 제약조건 (Constraint)

### 데이터 모델 절차
> 요개논물 (요괴(개)의 눈(논)물)

|            단계             |           모델           |                                                                                                                                                      설명                                                                                                                                                       |
|:---------------------------:|:------------------------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|     요구 조건 <br>분석      |            -             |                                                                                                  도출된 요구사항 간 상충 해결하고, 범위 파악해 <br>외부 환경과의 상호 작용을 분석 통해 데이터에 대한 요구 분석                                                                                                  |
|     <br>개념적 <br>설계     | <br>개념적<br>데이터<br>모델 |                    *사용자의 요구에 대한 트랜잭션을 모델링 하는 단계*<br>현실세계 인식을 추상적, 개념적 구조를 도출하는 데이터 모델<br>- 트랜잭션 모델링, View 통합 방법 및 Attribute 합성 고려<br>- 개념적 데이터 모델은 DB 종류와 관계 없음<br>- 주요 산출물을 **개체관계 다이어그램**이 있음                     |
|     <br>논리적 <br>설계     | <br>논리적<br>데이터<br>모델 |                                                        *트랜잭션 인터페이스를 설치하는 단계*<br>**DBMS에 맞는 논리적 스키마를 설치**하는 단계<br>- 논리적 설계 단계에서 정규화를 수행<br>- **스키마의 평가 및 정제**<br>- 논리적 DB구조로 매핑<br>- 관계형 DB에서는 테이블을 설계하는 단계                                                        |
| <br><br><br>  물리적 <br>설계 | <br><br>물리적<br>데이터<br>모델 | 논리 데이터 모델을 특정 DBMS의 특성 및 성능을 고려하여 <br>물리적인 스키마를 만드는 단계<br>- 테이블,인덱스,뷰,파티션 등 객체를 생성<br>- **응답시간, 저장공간 효율화, 트랜잭션 처리 고려해 설계**<br>- 성능 측면에서 반 정규화 수행<br>- **레코드 집중의 분석 및 설계**<br>- **저장 레코드 양식 설계**<br>- **접근 경로 설계** |

### 논리적 데이터 모델링 종류
|         종류         |                                                           설명                                                            |
|:--------------------:|:-------------------------------------------------------------------------------------------------------------------------:|
| <br>관계 데이터 모델 | 논리적 구조가 2차원 테이블 형태로 구성<br>기본키와 이를 참조하는 외래키로 관계 표현<br>1:1, 1:N, N:M 관계를 자유롭게 표현 |
| <br>계층 데이터 모델 |                           논리적 구조가 트리 형태로 구성<br>상하 관계가 존재<br>1:N 관계만 허용                           |
| <br>**네트워크 데이터 모델** |                              논리적 구조가 그래프 형태로 구성<br>**CODASYL DBTG 모델**이라 불림<br>상/하위 레코드 사이 다대다(N:M)관계 만족하는 구조                               |
### 개체 관계 다이어그램 기호
| 구성 | 기호 |
| :--: | :--: |
| 개체 | (사각형) |
| 관계 | (마름모) |
| 속성 | (타원) |
| 다중 값 속성 | (이중 타원) |
| 관계-속성 연결 | (선) |

### 함수 종속 표시 
Y는 X에 함수 종속 : X -> Y

### 이상 현상(Anomaly) 정의/종류
릴레이션 조작 시 데이터들이 불필요하게 중복되어 예기치 않게 발생하는 곤란한 현상
1. 삽입 이상 (Insertion Anomaly) 
2. 삭제 이상 (Deletion Anomaly)
3. 갱신 이상 (Update Anomaly)

### 데이터 베이스 정규화 단계
> 원부이 **결다조**

1. 1 정규형 (1NF) : **원자 값**으로 구성
2. 2 정규형 (2NF) : **부분 함수** 종속 제거 (완전 함수적 종속 단계)
3. 3 정규형 (3NF) : **이행 함수** 종속 제거 
4. 보이스-코드 정규형 (**BCNF**) : 결정자가 **후보 키가 아닌 함수** 종속 제거
5. 4 정규형 (4NF) : **다치 (다중 값)** 종속성 제거
6. 5 정규형 (5NF) : **조인** 종속성 제거

ex. 어떤 릴레이션 R의 모든 조인 종속성 만족이 R의 후보키를 통해서만 만족된다.

이 릴레이션 R은 어떤 정규형의 릴레이션인가? 5 정규형