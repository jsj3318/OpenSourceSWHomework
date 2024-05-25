# 오픈소스 SW 과제2

오픈소스SW 01분반   
컴퓨터공학과 20194516 **조승주**

---                    

## 과제 내용

- 리눅스 명령어 조사하기
  - **top**
  - **ps**
  - **jobs**
  - **kill**

---

### top

> top 명령어는 시스템의 실시간 성능을 모니터링하는 데 사용되는 명령어이다. CPU, 메모리 사용량, 프로세스 정보 등의 상태를 확인할 수 있다.

```bash 
top
```

#### top 실행 시

1. **시스템 정보**   
   - **uptime**: 시스템이 작동된 시간, 사용자 수
   - **load average**: 시스템 부하 평균(1분, 5분, 15분)
   - **Tasks**: 총 프로세스 수, 실행 중, 대기 중, 중지됨, 좀비 프로세스
   - **CPU 사용량**: 사용자, 시스템, 낮은 우선순위, 유휴 상태 등의 CPU 사용 비율
   - **메모리 사용량**: 총 메모리, 사용 중, 여유 공간, 버퍼/캐시된 메모리
   - **스왑 사용량**: 총 스왑 메모리, 사용 중, 여유 공간, 캐시된 스왑 메모리
2. **프로세스 정보**
   - **PID**
   - **USER**
   - **PR**: 우선순위
   - **NI**: nice (우선순위 조정 값)
   - **VIRT**: 가상 메모리 사용량
   - **RES**: 실 메모리 사용량
   - **SHR**: 공유 메모리 사용량
   - **S**: 프로세스 상태
   - **%CPU**: CPU 점유율
   - **%MEM**: 메모리 점유율
   - **TIME+**: CPU 사용 시간
   - **command**: 실행 중인 명령어

#### 단축키

- **h**: 도움말
- **k**: 프로세스 종료
- **q**: top 종료
- **z**: 색상 활성화/비활성화
- **1**: CPU 코어별 사용량 표시

#### 옵션

- -d SECONDS: 업데이트 주기 설정
- -p PID: 특정 프로세스 모니터링
- -u USER: 특정 사용자의 프로세스만 표시
- -n ITERATION: 지정한 횟수만큼 업데이트 후 종료

예시: 3초 간격으로 5번 업데이트 후 종료
```bash
top -d 3 -n 5
```

#### top 실행 화면
![image](https://github.com/jsj3318/OpenSourceSWHomework/assets/168888761/782d1e74-2937-4077-a6f6-2d7fec2f4250)

#### top 도움말 화면
![image](https://github.com/jsj3318/OpenSourceSWHomework/assets/168888761/eecc2345-7fbb-4e68-a354-0c05d03b1b7c)

#### top 색상 활성화
![image](https://github.com/jsj3318/OpenSourceSWHomework/assets/168888761/db9ecdfd-dfe1-41e9-887d-fcd830e26a9e)

---

### ps

> ps 명령어는 리눅스에서 현재 실행 중인 프로세스의 상태를 확인한다. 실시간이 아닌 명령어가 실행되는 시점의 상태를 확인한다.

```bash
ps
```

#### 옵션

- -e 또는 -A: 모든 프로세스 나열
- -f: 풀 포맷으로 출력
- -u USER: 특정 사용자의 프로세스 나열
- -p PID: 특정 PID의 프로세스 나열
- -aux: 모든 사용자의 모든 프로세스 상세 표시

예시: 특정 프로세스 찾기
```bash
ps aux | grep process_name
```

#### ps 실행 화면
![image](https://github.com/jsj3318/OpenSourceSWHomework/assets/168888761/cb2b7924-282b-4a1a-84d6-7c4c50489b87)

---

### jobs

> jobs 명령어는 현재 셸 세션에서 실행 중이거나 중지된 작업을 나열한다.

```bash
jobs
```

#### 옵션

- -l: 각 작업의 프로세스 그룹 및 세션 ID를 포함하여 자세한 정보 표시
- -p: 각 작업의 PID만 표시
- -r: 실행 중인 작업만 표시
- -s: 중지된 작업만 표시

#### 작업 제어

- 중지된 작업을 백그라운드에서 계속 실행
```bash
bg %1
```
- 작업을 포그라운드(foreground)로 가져옴
```bash
fg %2
```
- 특정 작업 종료
```bash
kill %1
```

---

### kill

> kill 명령어는 리눅스에서 프로세스를 종료하거나 신호를 보낸다. 기본값으로 종료신호를 보낸다.

```bash
kill [options] <PID>
```

#### 옵션

- -l [signal]: 모든 신호 이름을 나열하거나 특정 신호 번호의 이름 표시
```bash
kill -l
kill -l 5
```

- -s <signal> 신호 지정
```bash
kill -s SIGKILL PID
kill -s 9 PID
```

- -9 또는 -SIGKILL: 강제 종료

#### 주요 신호

신호 이름 | 번호 | 기능
---------| ------ | -------
**SIGTERM** | **15** | 기본 종료 신호. 정리할 시간을 주고 종료
**SIGKILL** | **9** | 강제 종료 신호. 정리할 시간 안 주고 종료
**SIGHUP** | **1** | 종료 후 재시작
**SIGINT** | **2** | 인터럽트 신호. 보통 Ctrl+C로 보냄
**SIGSTOP** | **19** | 프로세스 일시 중단
**SIGCONT** | **18** | 일시 중단된 프로세스 계속 실행

#### jobs와 kill로 백그라운드 작업 확인하고 종료하기
![image](https://github.com/jsj3318/OpenSourceSWHomework/assets/168888761/107d3f18-5e5c-462c-bbac-b00632b0b76f)

---

