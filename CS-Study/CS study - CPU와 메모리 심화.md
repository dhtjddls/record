
- 스케쥴링 
	- CPU에서 작업을 수행할 때 CU(control unit)에서 해당 작업들(프로세스)의 순서를 정하는 것

- 스케쥴링 종류
	- 선점 스케쥴링
		- OS가 스케쥴을 맘대로 지정할 수 있어서, 도중에 멈추고 다른 스케쥴들을 선점시킬 수 있는 방식
		1. 우선순위 스케쥴링
			1. 우선 순위를 부여해서 우선 순위가 높은 것부터 처리!
			2. 우선 순위가 낮은 친구들은 무한정 기다리는 기아 현상 발생!
			3. Aging방식으로 기다리는 시간에 따라 우선 순위를 높여주는 방식을 더해서 완화 가능
		2. 라운드로빈
			1. 정해진 시간 만큼만 동작을 수행하고, 작업이 남은 프로세스들은 맨 뒤로가서 재할당을 기다리는 방식 (회전식)
			2. 시간 할당이 짧으면 문맥전환(지금 작업에서 다음작업으로의 변경, 이것도 코스트야!)이 너무 잦게 일어나서 문제가 될 수 있음
		3. 다단계 큐
			1. 큐를 여러개 만들어서 각 큐마다 다른 스케쥴링 전략을 사용하여 상황에 맞게 배정하여 사용하는 방식
	- 비선점 스케쥴링
		- 프로세스가 실행되면 프로세스의 종료 혹은 I/O이벤트가 있을 때까지 실행을 보장하는 방식(도중에 멈추기 없기!, 처리시간 예측이 용이, 문맥 교환 비용이 적고 대신 처리 시간이 긴 프로세스가 들어오면 대기 시간이 길어질 수 있음)
		1. FCFS(FirstCome, FirstServe)
			1. 큐에 도착한 순서대로 CPU 할당
			2. 처리시간이 긴 프로세스가 앞에 있으면 대기시간이 길어진다.
		2. SJF (Shorted Job First)
			1. 처리시간이 제일 짧은 작업 먼저 수행
			2. 평균 대기 시간이 감소하고, 짧은 작업에 유리하다.
		3. HRN (Highest Response-ratio Next)
			1. 우선순위를 계산하여 점유 불평등 보완
			2. 우선순위 = (대기시간 + 실행시간) / 실행시간
	- 스케쥴링 동작지점
		![[스크린샷.png]]

- 메모리 (레지스터 -> 캐시 -> 주기억장치(RAM) -> 보조기억장치(HDD))
	- 캐시란? 
		- 데이터를 미리 복사해 놓는 임시 저장소
		- 계층과 계층 사이에서 속도차이를 해결하기 위한 임시 저장소
	- 캐시 히트와 캐시미드
		- 캐시 히트는 캐시에 원하는 데이터를 찾는 것
		- 캐시 미스는 캐시가 없을 때 주메모리에서 데이터를 찾아 오는 것
	- 메모리 할당 (메모리에 연속적으로 공간을 할당)
		- 연속할당
			1. 고정 분할 방식
				1. 메모리를 미리 나누어 관리하는 방식
				2. 내부 단편화 발생(나누어 놓은 공간보다 작은 프로세스가 들어오면 공간이 남는다.)
			2. 가변 분할 방식
				1. 매 시점 프로그램의 크기에 맞게 동적으로 메모리를 나눠서 사용하는 방식
				- 최초적합: 위에서부터 보이는 공간에 바로 할당
				- 최적적합: 가장 크기에 맞는 공간부터 채우고 나머지를 할당
				- 최악적합: 가장 크기가 큰 공간부터 채우고 나머지 할당
				2. 내부 단편화 X 외부 단편화 O 남겨진 공간보다 들어갈 프로세스가 더 커서 못들어가!
		- 불연속할당 (OS는 여러 작업을 효율적으로 처리해야하기 때문에 불연속할당 사용!)
			- 링크드 리스트
			- 비트맵
			- 페이지 테이블
				- 메모리를 동일한 크기의 페이지(가상구분)으로 나누고 페이지에 맞게 할당
				1. 페이징
					1. 동일한 크기의 페이지 단위
				2. 세그멘테이션
					1. 의미 단위인 세그먼트로 나누는 방식
				3. 페이지드 세그멘테이션
					1. 공유나 보안은 세그먼트로 나누고
					2. 물리적 메모리는 페이지로 나누는 방식
			- 페이지 교체 알고리즘
				1. 오프라인 알고리즘
					1. 입력 데이터가 모두 주어진 상태에서 실행되는 알고리즘
					2. 실행 중 새로운 입력이 들어오지 않습니다. 
					3. 미래의 프로세스를 알 수 없어서 실제로 사용되지는 않고, 다른 알고리즘들에 대한 기준을 제공
				2. 시간기반 알고리즘
					1. FIFO(First In First Out)
						1. 가장 먼저 온 페이지를 교체 영역에 가장 먼저 놓는 방법
					2. LRU(Least Recently Used)
						1. 참조가 가장 오래된 페이지를 교체하는 방법
						2. 가장 최근에 사용한 데이터를 먼저 사용할 가능성이 높기 때문에 캐시 히트율을 높일 수 있다.
						3. 누가 제일 최근인지를 저장해야 하기 때문에 추가적인 비용이 발생한다.
					3. NUR(Not Used Recently)
						1. 최근 사용여부를 0, 1로 표시하여 교체하는 방법
				3. 빈도기반 알고리즘
					1. LFU(Least Frequently Used)
						1. 가장 참조 횟수가 적은 페이지를 교체
						2. 일부 데이터가 빈번하게 사용되는 경우에는 성능 저하가 발생할 수 있음
