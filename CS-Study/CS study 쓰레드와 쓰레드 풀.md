
1. 쓰레드란? 
	- 프로세스는 수술 내용, 쓰레드는 의사(일꾼)
2. 쓰레드의 특징
	- 다른 쓰레드와 공간과 자원을 공유하면서 사용
	- 프로세스 보다 크기가 작은 실행 단위 구현
- 프로세스는 운영체제로부터 별도의 메모리 영역을 할당 받고
- 쓰레드는 Stack 을 제외한 Code/Data/Heap 부분은 공유해 서로 읽고 쓸 수 있게 됩니다. **(공유자원)**

- 독립적인 부분(작업 흐름과 관련됨)
	- **program counter (실행할 명령어)**
	- register set
	- stack space
 - 공유하는 부분(작업 데이터와 관련됨)
	- code section
	- data section
	- OS resources

3. 멀티 프로세스(작업 영역이 멀티)와 멀티 쓰레드(작업자가 멀티)
	1. 멀티 프로세서의 장단점
		- 안정적인 작업(프로세스 하나 죽어도 하나 더 있다!)
		- 프로세스간의 통신이 복잡하고 작업량이 많으면 오버헤드가 🔺 성능저하
	2. 멀티 쓰레드의 장단점
		- 효율적인 작업이 가능(일꾼이 많아! 공유도 해 서로!)
		- 오류 추적이 어렵다.
		- 동기화, 교착 상태가 발생할 수 있습니다!
		- 1. 쓰레드 하나가 프로세스 내 자원을 망쳐버린다면 **모든 프로세스가 종료될 수 있다.**
4. 쓰레드 풀
	- 컴퓨터 프로그래밍에서 쓰레드 풀은 컴퓨터 프로그램에서 실행의 동시성을 달성하기위한 소프트웨어 디자인 패턴
	- 동시에 실행할 수 있도록 여러 스레드를 미리 생성해두고 병렬처리
	- 프로그램 성능 저하를 방지하고, 다수의 요청을 처리하기 위해 사용한다!
	- 쓰레드 풀의 동작 과정
		1. 초기화: 쓰레드 풀을 사용하기 전에 초기화해야 합니다. 이 단계에서는 쓰레드 풀의 크기, 최대 쓰레드 수, 작업 큐 등의 매개변수를 설정합니다.
		2. 작업 수신: 쓰레드 풀은 작업을 수신하고 처리할 준비를 합니다. 작업은 일반적으로 작업 큐에 추가됩니다.
		3. 작업 수행: 쓰레드 풀에서는 미리 생성된 쓰레드들이 작업 큐를 모니터링하고 대기 중인 작업을 가져와 처리합니다. 이때 쓰레드 풀 내의 쓰레드들은 일반적으로 무한 루프를 돌면서 작업을 가져오기 위해 대기합니다.
		4. 작업 처리: 쓰레드 풀의 스레드가 작업을 가져와서 처리합니다. 작업은 일반적으로 작업 큐에서 FIFO(선입선출) 방식으로 가져오게 됩니다.
		5. 작업 완료 및 반환: 작업이 완료되면 해당 결과를 반환하고, 쓰레드는 다시 작업 큐에서 새로운 작업을 가져오기 위해 대기 상태로 돌아갑니다.
		6. 작업 대기: 작업 큐에 새로운 작업이 추가되면 쓰레드 풀의 스레드들은 대기 상태를 벗어나 작업을 가져와 처리합니다. 이를 반복하여 계속적으로 작업을 수행합니다.
		7. 종료: 쓰레드 풀을 더 이상 사용하지 않을 때 종료합니다. 종료할 때는 모든 작업이 완료되었는지 확인하고, 필요에 따라 남은 작업들을 처리하거나 버릴 수 있습니다.
	- 쓰레드 풀의 장단점
		- 효울적인 자원 관리 및 사용
		- 쓰레드 풀에 쓰레드를 너무 많이 생성해두면, 메모리 낭비가 발생 -> 단점 개선: Fork Join Thread Pool
5. 동시성과 병렬성
	1. 동시성
		- 싱글 코어에서 멀티 스레드를 동작시키기 위한 방식
		- 각 스레드들이 병렬적으로 실행되는 것처럼 보이지만 사실은 번갈아가면서 조금씩 실행되고 있는 것
	1. 병렬성
		- 한 개 이상의 스레드를 포함하는 각 코어들이 동시에 실행되는 성질
		- 병렬성은 데이터 병렬성(Data parallelism)과 작업 병렬성(Task parallelism)으로 구분
			1. 데이터 병렬성
				- 데이터 병렬성은 전체 데이터를 쪼개 서브 데이터들로 만든 뒤, 서브 데이터들을 병렬 처리하여 작업을 빠르게 수행하는 것
			2. 작업 병렬성
				- 작업 병렬성은 서로 다른 작업을 병렬 처리하는 것을 말합니다.


