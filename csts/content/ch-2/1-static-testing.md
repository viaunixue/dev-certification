## 개요

* 관리 리뷰
* 기술 리뷰
* 인스펙션
* 워크쓰루
* 감사

## 리뷰 프로세스

1. 경영진 준비
2. 리뷰 계획
3. 리뷰 절차 개요 설명
4. 작업물 개요 설명
5. 개별 준비
6. 그룹 검토
7. 재작업
8. 후속 작업

## 관리 리뷰

**관리 스태프들이 참여하며 관리자가 주재한다.**

## 기술 리뷰

**대표 엔지니어가 주재하며 경우에 따라 
관리자가 해결해야 할 이슈가 있으면 관리자도 참가할 수 있다.**

## 인스펙션 (동료 검토)

### 인스펙션 참가자의 역할
작성자가 아닌 사람이 회의 주재자를 맡는다.  <br>
관리자 직책을 담당하는 사람은 팀 멤버로 참여하는 것을 금지한다.  <br> 
- 주재자 : 공식 검토/검토 회의를 운영하며 회의 종료 후 사후 관리 <br>
- 작성자 : 검토 대상 산출물 작성자로 문서에 대한 책임이 있고, 검토 시 해당 산출물에 관해 설명 <br>
- 낭독자 : 작업물에 대한 자신의 이해 및 해석을 바탕으로 회의 참가자들에게 설명 <br>
- 기록자 : 회의에서 논쟁, 모든 질문 및 답변 등을 기록 / 문서화 해야 함 (검토자 입장에서 참가) <br>
- 검토자 : 자료를 충분히 검토하고 회의를 준비, 해결자 입장이 아니므로 간단히 의견만 제시 <br>

### 인스펙션 과정

1. 리뷰 계획 : 리뷰 리더인 중재자가 리뷰 목적 파악해 팀 구성원에게 정보 전달.  <br>
2. 인스펙션 절차 개요 설명 : 중재자는 체크리스트나 역할 할당에 관한 질문에 대답  <br>
3. 인스펙션 작업물에 대한 개요 설명  : 작성자가 검토자들에게 작업물에 대해 설명 (사전 이해도)<br>
4. 준비  : 실제 리뷰 회의 전 구성원은 작업물을 검토, 준비 기간 검출된 문제 중재자에 전달<br>
5. 검토 회의 : 개별적으로 체크리스트를 활용하여 작업물에 대한 개별검토가 완료된 후, <br> 모든 검토자가 참가하는 회의를 시작, 문제 해결에 관한 토의는 하지 않음
   <br>
6. 재작업 : 검출된 문제 목록이 작성자에게 전달되면 작성자는 실제 작업물에서 문제 해결 작업을 수행 <br>
7. 후속 작업  : 주재자나 주재자에게 위임받은 사람이 발견된 모든 문제에 대해 재작업 충분히 이루어지는지 확인<br>

**작성자가 아닌 사람이 회의 주재자를 맡는다.
관리자 직책을 담당하는 사람은 팀 멤버로 참여하는 것을 금지한다.**


```
cf) 퍼실리테이터(Facilitator) : 검토 회의 또는 워크숍 같이 여러 사람이 일정한 목표를 가지고 함께 작업을 할 때 효과적으로 그 목적을 달성할 수 있도록 작업 과정을 설계하고 참여를 유도하여 질 높은 결과물이 나오도록 도움을 주는 사람 (여기서는 주재자) 
```

## 워크 쓰루

> 인스펙션 보다는 비형식적인 결함 검출 방법

작성자 본인이 보통 회의를 주재하며 기록자 역할도 담당할 수 있다.
관리자 직책을 담당하는 사람은 팀 멤버로 참여하는 것을 금지한다.
- 보통은 개발자에 의해 회의가 진행된다.  <br>
- 회의 시작 전 참가자들이 작업물에 대해 철저하게 준비하지 않아도 됨  <br>
- 회의를 주재하기 위해 별도의 훈련을 필요로 하지 않음  <br>
- 회의 결과가 잘 처리되었는지 확인하는 작업을 생략할수 있음

<br>

```
비공식 리뷰 < 워크 쓰루 < 기술 리뷰 < 인스펙션
```

## 감사

**SW 제품 및 프로세스가 규제, 표준, 가이드라인, 계획, 절차를 준수하고 있는지 독립적으로 평가**

## 정적 분석

### 코딩 표준

* 초기화 하지 않고 사용한 코드
* 선언 후 사용하지 않은 함수 또는 변수
#### 코딩 스타일

* BSD

  ```java
  if(...)
  {
	  doSomething();
  }
  ```
* K&R

    ```java
    if(...){
        doSomething();
    }
    ```

* GNU

    ```java
    if(...)
        {
            doSomething();
        }
    ```
<br>

> MISRA-C : C 프로그래밍 언어 코딩 가이드라인

### 복잡도 분석

#### 순환 복잡도 = E (간선들의 개수) - N (노드들의 개수) + 2

* if, while, for, &&, || 를 만나면 +1
* switch 문의 각 case에 +1

### 자료 흐름 분석

<table>
	<tr>
		<td>~d</td>
		<td>처음 정의 됨</td>
		<td>문제 없음</td>
	</tr>
	<tr>
		<td>~u</td>
		<td>처음 사용 됨</td>
		<td>잠재적 결함<br>(자료 정의되지 않고 바로 사용됨) </td>
	</tr>
	<tr>
		<td>~k </td>
		<td>처음 무효화</td>
		<td>잠재적 결함<br>(자료 정의되지 않고 바로 무효화) </td>
	</tr>
	<tr>
		<td>d~ </td>
		<td>제일 나중에 발생한 정의</td>
		<td>잠재적 결함</td>
	</tr>
	<tr>
		<td>u~ </td>
		<td>제일 나중에 발생한 참조</td>
		<td>문제 없음 </td>
	</tr>
	<tr>
		<td>k~</td>
		<td>제일 나중에 발생한 무효화</td>
		<td>문제 없음</td>
	</tr>
	<tr>
		<td>dd </td>
		<td>define - define</td>
		<td>잠재적 결함 (두번 연이어 정의)</td>
	</tr>
	<tr>
		<td>kk </td>
		<td>kill - kill</td>
		<td>잠재적 결함 </td>
	</tr>
	<tr>
		<td>uu</td>
		<td>use - use</td>
		<td>문제 없음</td>
	</tr>
	<tr>
		<td>ku</td>
		<td>kill - use</td>
		<td>심각한 결함</td>
	</tr>
	<tr>
		<td>dk</td>
		<td>define - kill</td>
		<td>잠재적 결함(자료가 전혀 사용 X)</td>
	</tr>
	<tr>
		<td>du</td>
		<td>define-use</td>
		<td>문제 없음</td>
	</tr>
	<tr>
		<td>ud</td>
		<td>use - define</td>
		<td>문제 없음 (자료 사용된 후 다시 정의) </td>
	</tr>
	<tr>
		<td>uk</td>
		<td>use - kill</td>
		<td>문제 없음 </td>
	</tr>
</table>

