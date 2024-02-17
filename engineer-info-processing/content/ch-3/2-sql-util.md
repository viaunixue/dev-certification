# SQL 활용

## 기본 SQL 작성

### 집합 연산자 유형
#### 유유인마
1. UNION
2. UNION ALL
3. INTERSECTION
4. MINUS

## 고급 SQL 작성

### DDL 대상
| DDL 대상 | 설명 |
|:--------:|:----:|
|  도메인  | **하나의 속성이 가질 수 있는 원자값들의 집합**<br>속성의 데이터 타입과 크기, 제약조건 등 정보     |
|  스키마  | DB 구조, 제약 조건 등 정보를 담고 있는 기본적인 구조<br>1. 외부 스키마 : 사용자나 개발자 관점에서 필요로하는 DB 논리적 구조<br>2. 개념 스키마 : 데이터베이스 **전체적인** 논리적 구조<br>3. 내부 스키마 : 물리적 저장장치 관점에서 보는 DB 구조     |
|  테이블  | 데이터 저장 공간     |
|    뷰    | 하나 이상의 물리 테이블에서 유도되는 가상 테이블     |
|  인덱스  | 검색 빠르게 하기 위한 데이터 구조     |

| 보기 | 설명 |
| ---- | ---- |
| 인덱스 | DB 성능에 많은 영향을 주는 DBMS 구성요소로 <br>테이블과 클러스터에 연관되어 독립적인 저장 공간을 보유하며, <br>DB에 저장된 자료를 더욱 빠르게 조회하기 위해 사용 |
| 트랜잭션 | DB 시스템에서 하나의 논리적 기능을 정상적으로 수행하기 위한 <br>작업의 기본 단위 |
| 역정규화 | 정규화 된 엔티티, 속성, 관계에 대해 성능 향상/개발운영 단순화를 위해<br>**중복, 통합, 분리** 등을 수행하는 데이터 모델링 기법 |
| 트리거 | DB 시스템에서 **삽입, 갱신, 삭제 등 이벤트 일어날 때마다 <br>관련 직업이 자동으로 수행**됨 |

### 트랜잭션 특징
#### ACID
|              특징              |                                                   설명                                                    |                             주요 기법                              |
|:------------------------------:|:---------------------------------------------------------------------------------------------------------:|:------------------------------------------------------------------:|
|     원자성<br>(**Atomicity**)      | 트랜잭션 구성 연산 전체가 모두 정상적으로 실행되거나<br>모두 취소되어야 하는 성질. 전체 성공 or 전체 실패 |                Commmit/<br>Rollback<br>회복성 보장                 |
|    일관성<br>(**Consistency**)     |        시스템이 가지고 있는 고정 요소는 트랜잭션 수행 전과<br>수행 완료 후 상태가 같아야 하는 성질        |                   무결성 제약조건<br>동시성 제어                   |
| 격리성 = 고립성<br>(**Isolation**) |                <br>동시에 실행되는 트랜잭션들이 서로 영향을 미치지 <br>않아야 한다는 성질                 | Read Uncomitted<br>Read Committed<br>Repeated Read<br>Serializable |
|     영속성<br>(**Durability**)     |                 성공이 완료된 트랜잭션의 결과는 영속적으로<br>DB에 저장되어야 한다는 성질                 |                             회복 기법                              |

### 트랜잭션 상태
| 상태 | 설명 |
| ---- | ---- |
| 활동 상태<br>(Active) |  |
| **부분 완료 상태<br>(Partially Committed)** | 마지막 명령문 실행된 후 가지는 상태로 모든 연산 처리 끝났지만<br>트랜잭션이 수행한 최종 결과를 DB에 반영하지 않은 상태 |
| 완료 상태<br>(Committed) |  |
| 실패 상태<br>(Failed) |  |
| **철회 상태<br>(Aborted)** | 트랜잭션 취소되고 DB가 트랜잭션 시작 전 상태로 환원된 상태<br>트랜잭션 수행이 실패하여 Rollback 연산을 실행한 상태 |

### Phase Commit
| 단계 | 설명 |
| ---- | ---- |
| 1단계<br>(준비 단계) | 트랜잭션 수행 결과를 다른 분산 시스템에 알리는 과정 |
| 2단계<br>(커밋 단계) | 모든 분산 시스템에서 트랜잭션 수행 결과가 일치하는지 확인<br>트랜잭션 성공적으로 수행했다면 커밋을 수행하고 그렇지 않다면 롤백을 수행 |

### 고립화 수준
| 종류 | 설명 |
| ---- | ---- |
| Read Uncommitted | 한 트랜잭션에서 갱신 중인(아직 커밋 X) 데이터를 다른 트랜잭션이 <br>읽는 것을 허용하는 수준<br>연산 중인 데이터에 대한 연산은 불허 |
| Read Committed | 한 트랜잭션에서 갱신을 수행할 때 연산이 완료될 때까지 <br>연산 대상 데이터에 대한 읽기 제한하는 수준 |
| Repeatable Read | 선행 트랜잭션이 특정 데이터를 읽을 때,<br>**트랜잭션 종료 시까지 해당 데이터에 대한 갱신/삭제를 <br>제한**하는 수준 |
| Serialization Read | 선행 트랜잭션이 특정 데이터의 영역을 순차적으로 읽을 때 <br>해당 데이터 영역 전체에 대한 접근 제한하는 수준 |


### 병행 제어 기법의 종류
#### 로 낙타다 (록(로) 콘서트에서 낙타를 타다)
|                     기법                     |                                                                                                                                                                                     설명                                                                                                                                                                                      |
|:--------------------------------------------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|              <br><br>**로킹**<br>(Locking)               | 같은 자원 액세스하는 다중 트랜잭션 환경에서 DB의 일관성과 무결성을<br>유지하기 위해 **트랜잭션 순차적 진행을 보장하는 직렬화 기법**<br>1. DB, 파일, 레코드 등 로킹 단위가 될 수 있음<br>2. **로킹 단위 작아지면 DB 공유도 증가**<br>3. **로킹 단위 작아지면 로킹 오버헤드 증가**<br>4. 한꺼번에 로킹할 수 있는 객체 크기를 로킹 단위라고 함<br>5. **로킹 단위 작아지면 병행성 수준이 낮아짐** |
|  낙관적 **검증**<br>(Optimistic<br> Validation)  |                                                                                                                            트랜잭션이 어떠한 검증도 수행하지 않고 일단 트랜잭션을 수행하고<br>트랜잭션 종료 시 검증을 수행하여 DB에 반영하는 기법                                                                                                                             |
| **타임 스탬프 순서**<br>(Time Stamp<br>Ordering) |                                                                                                         트랜잭션과 트랜잭션이 읽거나 갱신한 데이터에 대해 <br>트랜잭션이 실행을 시작하기 전에 타임 스탬프를 부여하여<br>부여된 시간따라 트랜잭션 작업을 수행하는 기법<br>동시성 제어를 위한 직렬화 기법<br>트랜잭션 간의 순서를 미리 정하는 방법                                                                                                         |
|             다중버전 동시성 <br>제어<br>(MVCC; Multi<br>Version<br>Concurrency <br>Control)             | <br>**트랜잭션의 타임스탬프와 접근하려는 데이터의 타임스탬프를<br>비교**하여 직렬 가능성이 보장되는 적절한 버전을 선택하여<br>접근하도록 하는 기법                                                                                                                                                                                                                                                                                                                                                                              |

### 회복 기법 종류 (영속성 주요 기법)
#### 회로체그(크) (무전기의 회로를 체크해봐라)
| 기법 | 설명 |
| :--: | :--: |
| 로그 기반<br>회복 기법 | 1. **지연 갱신 회복 기법** : 트랜잭션 완료 전까지 DB에 기록하지 않는 기법<br>2. **즉각 갱신 회복 기법** : 트랜잭션 수행 중 갱신 결과 바로 DB에 반영하는 기법 |
| 체크 포인트 회복 | 장애 발생 시 검사점 이후 처리된 트랜잭션에 대해서만<br>장애 발생 이전의 상태로 복원시키는 회복 기법 |
| 그림자 페이징<br>회복 기법 | DB 트랜잭션 수행 시 복제본을 생성하여 DB 장애 시<br>이를 이용해 복구하는 기법 |
### 테이블 관련 용어
| 용어 | 설명 |
| :--: | :--: |
| 튜플 (Tuple) / 행 (Row) | 테이블 내의 행을 의미하며 레코드 라고도 함<br>튜블은 릴레이션에서 같은 값을 가질 수 있음 |
| 애트리뷰트(Attribute)/<br>열(Column) | 테이블 내의 열을 의미<br>열의 개수를 Degree 라고 함 |
| 식별자 (Identifier) | 여러 개의 집합체를 담고 있는 관계형 DB에서<br>각각의 구분할 수 있는 논리적인 개념 |
| 카디널리티(Cardinality) | 튜플(Tuple)의 개수 |
| 차수(Degree) | 애트리뷰트(Attribute) 개수 |
| 도메인(Domain) | 하나의 애트리뷰트가 취할 수 있는 같은 타입의 원자값들의 집합 |
### 뷰의 장점과 단점
| 장점 | 설명 |
| :--: | :--: |
| 논리적 독립성 제공 | 뷰는 논리 테이블 |
| 사용자 데이터 관리 용이 | 단순 질의어 사용이 가능 |
| 데이터 보안 용이 | 중요 보안 데이터 저장 중인 테이블에는 접근 불허 |

| 단점 | 설명 |
| :--: | :--: |
| **뷰 자체 인덱스 불가** | **인덱스는 물리적 저장 데이터를 대상**으로 하기에<br>논리적 구성인 뷰 자체는 인덱스를 가지지 못함 |
| 뷰 정의 변경 불가 | **뷰 정의를 변경하려면 뷰를 삭제하고 재생성** |
| 데이터 변경 제약 존재 | 뷰 내용에 대한 삽입, 삭제, 변경, 제약이 있음 |

### 뷰 특징
1. 뷰(View) 삭제 시 DROP 명령을 사용함
2. 뷰는 정의된 기본 테이블이 삭제되면 자동으로 삭제됨
3. 뷰 정의는 ALTER 문을 이용해 변경할 수 없음
4. **뷰는 변경이 불가하므로 DROP -> CREATE 해야 함**

### 집합 연산자 유형
1. UNION : 중복행 제거된 쿼리 결과 집합
2. UNION ALL : **중복 행 제거되지 않은** 쿼리 결과 집합
3. INTERSECT : 교집합
4. MINUS : 첫 쿼리 있고 두번째 쿼리에는 없는 집합

