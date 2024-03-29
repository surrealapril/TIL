- 면접을 위한 CS전공 지식 노트 2022.10.23



# 📌 네트워크

노드와 링크가 서로 연결되어 있거나 연결되어 있지 않은 집합체. 네트워크를 구성할 때 좋은 네트워크로 만드는 것이 중요. 

> 좋은 네트워크란 ? 많은 **처리량**을 처리할 수 있으며 **지연 시간**이 짧고 장애 빈도가 적으며 좋은 보안을 갖춘 네트워크
> 

[image]

- 노드 : 서버, 라우터, 스위치 등 네트워크 장치
- 링크 : 유선 또는 무선
- 처리량 : 링크를 통해 전달되는 단위 시간당 데이터양. 사용자들이 많이 접속할 때마다 커지는 트래픽, 네트워크 장치 간의 대역폭(주어진 시간동안 네트워크 연결을 통해 흐를 수 있는 최대 비트 수), 네트워크 중간에 발생하는 에러, 장치의 하드웨어 스펙에 영향을 받음. → 단위 : bps(bits per second) 초당 전송 또는 수신되는 비트 수.
- 지연 시간 : 요청이 처리되는 시간. 어떤 메시지가 두 장치 사이를 왕복하는 데 걸리는 시간. 매체타입(무선,유선), 패킷 크기, 라우터의 패킷 처리 시간에 영향을 받음

## 🌞 네트워크 토폴로지

네트워크 설계 시 고려. 노드와 링크가 어떻게 배치되어 있는지에 대한 방식이자 연결 형태

- **트리 토폴로지** - 계층형 토폴로지. 트리 형태로 배치한 네트워크 구성.
    - 장점 : 노드 추가,삭제가 쉬움.
    - 단점 : 특정 노드에 트래픽이 집중될 때 하위 노드에 영향을 끼칠 수 있음.
- **버스 토폴로지** - 중앙 통신 회선 하나에 여러 개의 노드가 연결되어 공유하는 네트워크 구성. 근거리 통신망(LAN)에서 사용.
    - 장점 : 설치 비용이 적고 신뢰성 우수, 중앙 통신 회선에 노드 추가 삭제가 쉬움.
    - 단점 : 스푸핑이 가능함.
- **스타 토폴로지** - 중앙에 있는 노드에 모두 연결된 네트워크 구성.
    - 장점 : 노드 추가, 에러 탐지가 쉽고 패킷 충돌 발생 가능성이 적음. 어떠한 노드에 장애가 발생해도 쉽게 에러를 발견할 수 있고, 장애 노드가 중앙 노드가 아닐 경우 다른 노드에 영향을 끼치는 것이 적음
    - 단점 : 중앙 노드에 장애가 발생하면 전체 네트워크를 사용할 수 없고 설치 비용이 고가.
- **링형 토폴로지** -  각각의 노드가 양 옆의 두 노드와 연결하여 전체적으로 고리처럼 하나의 연속된 길을 통해 통신하는 망 구성 방식. 데이터는 노드에서 노드로 이동하며, 각각의 노드는 고리 모양의 길을 통해 패킷을 처리.
    - 장점 : 노드 수가 증가되어도 네트워크상의 손실이 거의 없고, 충돌 발생 가능성도 적음, 노드의 고장 발견이 쉬움.
    - 단점 : 네트워크 구성 변경이 어렵고, 회선에 장애가 발생하면 전체 네트워크에 영향을 크게 미침.
- **메시(망형) 토폴로지** - 그물망처럼 연결되어 있는 구조. 한 단말 장치에 장애가 발생해도 여러 개의 경로가 존재.
    - 장점 : 네트워크를 계속 사용할 수 있고 트래픽 분산 처리 가능.
    - 단점 : 노드의 추가가 어렵고, 구축 비용과 운용 비용이 고가.

> 스푸핑? LAN 상에서 송신부의 패킷을 송신과 관련 없는 다른 호스트에게 가지 않도록 하는 스위칭 기능을 마비시키거나 속여서 특정 노드에 해당 패킷이 오도록 처리하는 것.
> 

### 🌞 네트워크 병목 현상

전체 시스템의 성능이나 용량이 하나의 구성 요소로 인해 제한 받는 현상. 토폴로지가 중요한 이유는 병목 현상을 찾을 때 중요한 기준이 됨. 애플리케이션 코드 상 문제가 없는데 사용자가 서비스로부터 데이터를 가져오지 못하는 상황 → 네트워크 병목 현상일 가능성.

- 병목 현상 주된 원인
    - 네트워크 대역폭
    - 네트워크 토폴로지
    - 서버 CPU, 메모리 사용량
    - 비효율적인 네트워크 구성

네트워크 관련 테스트, 네트워크와 무관한 테스트를 통해 네트워크로부터 발생한 문제점일 경우 네트워크 성능 분석 시 사용하는 명령어

- ping - 네트워크 상태를 확인하려는 대상 노드를 향해 일정 크기의 패킷을 전송하는 명령어. 해당 노드의 패킷 수신 상태와 도달하기까지의 시간, 해당 노드까지 네트워크가 잘 연결되어 있는지 확인. TCP/IP 프로토콜 중 ICMP 프로토콜을 통해 동작하기 때문에, ICMP 프로토콜을 지원하지 않거나 차단하는 경우 실행할 수 없다.
    - ping IP주소또는도메인주소
- netstat - 접속되어 있는 서비스들의 네트워크 상태. 네트워크 접속, 라우팅 테이블, 네트워크 프로토콜 등 리스트를 보여줌, 서비스의 포트가 열려있는지 확인용.
- nslookup - DNS에 관련된 내용 확인. 특정 도메인에 매핑된 IP를 확인하기 위해 사용.
- tracert (리눅스 : traceroute) - 목적지 노드까지 네트워크 경로를 확인할 때 사용. 목적지 노드까지 구간들 중 어느 구간에서 응답 시간이 느려지는지 확인 가능.
- 이 외 ftp를 통해 대형 파일 전송 테스팅, tcpdump를 통해 노드로 오고가는 패킷 캡쳐, 네트워크 분석 프로그램 wireshark, netmon.

## 🌞 네트워크 분류

- LAN(Local Area Network) - 근거리 통신망. 전송속도가 빠르고 혼잡하지 않음.
- MAN(Metropolital Area Network) - 대도시 지역 네트워크. 전송속도 평균, LAN보다 혼잡.
- WAN(Wide Area Network) - 광역 네트워크. 전송속도 낮음, MAN보다 혼잡

네트워크 프로토콜 - 다른 장치들끼리 데이터를 주고받기 위해 설정된 공통된 인터페이스. IEEE 또는 IETF 표준화 단체가 정함.

## 🌞 TCP/IP 4계층 모델

인터넷 프로토콜 스위트(internet protocol suite)는 인터넷에서 컴퓨터들이 서로 정보를 주고받는 데 쓰이는 프로토콜의 집합 → TCP/IP 4계층 또는 OSI 7 계층으로 설명.

TCP/IP 4계층 모델이란 ?

> 네트워크에서 사용되는 통신 프로토콜의 집합으로 계층들은 프로토콜의 네트워킹 범위에 따라 네 개의 추상화 계층으로 구성.
> 

이 계층들은 특정 계층이 변경되어도 다른 계층이 영향받지 않도록 설계.

- 애플리케이션 계층 - FTP, HTTP, SSH, SMTP, DNS 등 응용 프로그램이 사용되는 프로토콜 계층. 웹 서비스, 이메일 등 서비스를 실질적으로 사람들에게 제공하는 층.

- 전송 계층 - 송신자와 수신자를 연결하는 통신 서비스 제공. 연결 지향 데이터 스트림 지원, 신뢰성, 흐름 제어 제공. 애플리케이션과 인터넷 계층 사이의 데이터가 전달될 때 중계 역할.
    - TCP - 패킷 사이의 순서 보장, 연결 지향 프로토콜을 사용해서 연결 하여 신뢰성 구축, 수신 여부 확인 → **가상 회선 패킷 교환 방식**
        - 가상 회선 패킷 교환 방식
            - 각 패킷에 가상회선 식별자를 포함하여 패킷을 전송하면 가상회선이 해제되고 전송 된 순서대로 도착하는 방식.
        - 신뢰성 확보를 위한 3-Way Handshake ***재정리 필요***
    - UDP - 순서를 보장하지 않고, 수신 여부를 확인하지 않음. 단순히 데이터만 주는 **데이터그램 패킷 교환 방식**.
        - 데이터그램 패킷 교환 방식
            - 패킷이 독립적으로 이동하며 최적의 경로를 선택, 하나의 메시지에서 분할된 여러 패킷은 서로 다른 경로로 전송될 수 있으며 도착 순서가 다를 수 있음.

- 인터넷 계층 - 장치로부터 받은 네트워크 패킷을 IP주소로 지정된 목적지르 전송하기 위해 사용되는 계층. 패킷을 수신해야할 상대의 주소를 지정해 데이터 전달. 비연결형적인 특징(상대방이 제대로 받았는지에 대해 보장하지 않음
    - IP
    - ARP
    - ICMP
    
- 링크 계층(네트워크 접근 계층) - 전선, 광섬유, 무선 등으로 실질적으로 데이터를 전달, 장치 간에 신호를 주고받는 ‘규칙’을 정하는 계층. 물리 계층과 데이터 링크 계층으로 나누기도 함.
    - 물리 계층 - 무선 LAN과 유선 LAN을 통해 0과 1로 이루어진 데이터를 보내는 계층
    - 데이터 링크 계층 - 이더넷 프레임을 통해 에러 확인, 흐름 제어, 접근 제어를 담당하는 계층
    
    /유선LAN 전이중화 통신 다시 정리 88p~93p
    

### 🌞 계층 간 데이터 송수신 과정

애플리케이션 계층에서 전송 계층으로 데이터를 보낼 때 캡슐화 과정을 거쳐 전달, 링크 계층을 통해 서버와 통신, 서버의 링크 계층으로부터 애플리케이션까지 비캡슐화 과정을 거쳐 데이터 전송.

- 캡슐화 과정 - 상위 계층의 헤더와 데이터를 하위 계층의 데이터 부분에 포함시키고, 해당 계층의 헤더를 삽입하는 과정
- 비캡슐화 과정 - 하위 계층에서 상위 계층으로 가며 각 계층의 헤더 부분을 제거하는 과정

- 용어 정리
    - FTP - 장치와 장치 간의 파일을 전송하는데 사용하는 표준 통신 프로토콜
    - SSH - 보안되지 않은 네트워크에서 네트워크 서비스를 안전하게 운영하기 위한 암호화 네트워크 프로토콜
    - HTTP - World Wide Web을 위한 데이터 통신의 기초이자 웹 사이트를 이용하는데 쓰는 프로토콜
    - SMTP - 전자 메일 전송을 위한 인터넷 표준 통신 프로토콜
    - **DNS** - 도메인 이름과 IP주소를 매핑해주는 서버. IP주소가 바뀌어도 똑같은 도메인 주소로 서비스. ***재정리 필요***
    - PDU - Protocol Data Unit 네트워크의 어떠한 계층에서 계층으로 데이터가 전달될 때 한 덩어리 단위. 제어 관련 정보들이 포함된 ‘헤더’, 데이터를 의미하는 ‘페이로드’로 구성되어 있으며 계층마다 부르는 명칭이 다름. PDU 중 아래 계층인 비트로 송수신하는 것이 모든 PDU 중 가장 빠르고 효율이 좋음. 애플리케이션 계층에서 문자열 기반으로 송수신 하는데 그 이유는 헤더에 authorization 값 등 다른 값들을 넣는 확장이 쉽기 때문.
        - 애플리케이션 계층 - 메시지
        - 전송 계층 - 세그먼트(TCP), 데이터그램(UDP)
        - 인터넷 계층 - 패킷
        - 링크 계층 - 프레임(데이터 링크 계층), 비트(물리 계층)