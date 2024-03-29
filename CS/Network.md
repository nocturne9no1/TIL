# [Network]

## 1 네트워크

### 컴퓨터 네트워크

* 컴퓨터 간의 연결
* `컴퓨터 네트워크` 라는 말이 정확함
* 컴퓨터가 두 대 이상 연결되어 컴퓨터 네트워크가 되고, 컴퓨터 간 필요한 데이터를 서로 주고 받을 수 있음
* `인터넷`: 전 세계의 큰 네트워크부터 작은 네트워크까지를 연결하는 거대한 네트워크



### 패킷

* 네트워크나 인터넷에서 데이터를 주고받으려면 `규칙` 이 필요함
* 이 규칙에 `패킷(packet)` 을 사용
* 패킷
  * 컴퓨터 간 데이터를 주고받을 때 네트워크를 통해 전송되는 데이터의 작은 조각
  * 큰 데이터가 있더라도 작게 나누어 보내는게 규칙임
  * 왜 작게 나누나???
  * 큰 데이터를 그대로 보내면 네트워크의 `대역폭(bandwidth)` 를 너무 많이 점유
    * 대역폭: 네트워크에서 이용 가능한 최대 전송 속도, 단위 시간당 전송량
  * 다른 패킷 흐름을 막게할 위험
  * 큰 데이터를 작은 조각으로 나누어 보냈다면
  * 원래 데이터대로 되돌리는 작업을 해야 함
  * 순서대로 도착하지 않았을 수 있음
  * 네트워크 지연으로 인해 늦게 도착하거나 패킷 누락될 가능성도 있음
  * 따라서, 송신측에서 수신측으로 패킷 보낼 때는 각 패킷에 **순서대로 번호**를 붙여 보냄



### 정보 양의 단위

* Digital Data: 0과 1의 2진법으로 이루어진 데이터 집합
* 여기서 0 1의 정보를 나타내는 최소 단위를 `bit` 라고 함
* bit 8개를 모아서 `byte` 가 됨
* `8bit` = `1byte`
  * 2^8 = 256 종류의 정보를 나타낼 수 있어서 영어 알파벳 + 특수 문자를 표현 할 수 있음
  * 하지만 모든 라틴 문자를 표현하기에는 부족하여 유니코드가 등장하게됨
  * 한글의 경우에도 1바이트로는 어림도 없기때문에 한글 한글자당 2바이트를 할당함
  * 완성형 한글의 경우 3바이트를 차지하는 경우도 있음
* 키보드로 문자를 표현할 때 각 숫자 & 문자의 대응표를 미리 만들어 놨음
* 이 대응표를 `문자 코드(character code)` 라고 부름
* ASCII 코드
  * American Strandard Code for Information Interchange
  * 알파벳, 기호, 수자 등을 다룰 수 있는 기본적인 문자 코드
  * A = 65, B = 66, C = 67 ... 등의 대응표를 가지고 있음
* 네트워크에 데이터를 전송하는 경우 비트 정보를 전기 신호로 변환하여 보냄



### LAN & WAN

* LAN
  * Local Area Network
  * 건물 안이나 특정 지역을 범위로 하는 네트워크
  * 가정이나 빌딩 안의 사무실과 같이 지리적 제한이 있는 곳에서 컴퓨터, 프린터 등을 연결할 수 있는 네트워크
* WAN
  * Wide Area Network
  * 지리적으로 넓은 범위에 구축된 네트워크
  * `인터넷 서비스 제공자(ISP)` 가 제공하는 서비스를 사용하여 구축된 네트워크
    * ISP: Internet Service Provider
    * 인터넷 상용 서비스 사업을 하고 있는 KT, U+, SK브로드밴드와 같은 사업자들(통신회사)
  * 랜과 랜을 연결하는 것으로 생각해도 무방
* LAN과 WAN은 연결 거리에 따라 신호의 세기, 오류의 빈도, 인터넷 속도 등의 차이가 있음



### 집에서의 LAN

* 가정에서는 컴퓨터, 스마트폰, 프린터 등이 인터넷 공유기에 연결되어 있고 공유기가 ISP로 연결되는 구조
* 인터넷 개통시에는 일반적으로 ISP와 인터넷 회선 두 가지를 결정해야 함



### 회사의 LAN

* 가정 LAN과 다른 점은 DMZ라는 네트워크 영역이 있다는 점
* DMZ
  * DeMilitarized Zone
  * 네트워크 구성 중 인터넷인 외부 네트워크와 내부 네트워크 사이에 위치한 중간 지대(서브넷)을 말함
  * 외부 공격자가 내부 네트워크에 침투하는 것을 막는 역할
  * 외부에 서버를 공개하기 위한 네트워크
    * 주로 웹 서버, 메일 서버, DNS 서버
* 회사에서의 서버 운영 방법
  * 사내 서버 설치
  * 데이터 센터에 설치
    * 위 두 가지 방법은 `온-프레미스(on-premise)` 라고 부름
  * 클라우드에 설치
* 각 서버는 스위치와 연결하여 서로 통신 가능





## 네트워크 기본 규칙

### Protocol

* `Protocol`: 통신하기 위한 규칙

### OSI Model

* 옛날 옛적 같은 회사의 컴퓨터끼리만 통신이 가능했던 시절이 있었음
* 이런 문제를 해결하기 위해 `표준 규격` 을 정해야만 했음
* `ISO` 라는 국제 표준화 기구가 `OSI Model` 이라는 표준 규칙을 제정
* OSI Model
  * 네트워크 기술의 기본이 되는 모델
  * 데이터의 송수신은 컴퓨터 → 컴퓨터 데이터 전송
  * 이 때 컴퓨터는 여러가지 일을 하는데, 이런 일을 7계층으로 나눠서 진행함
  * 계층 대신 `레이어` 라 부르기도 함
  * 7계층
    * 응용 계층: 애플리케이션에 대한 서비스 제공
    * 표현 계층: 문자 코드, 압축, 암호화 등의 데이터를 변환
    * 세션 계층: 세션 체결, 통신 방식 결정
    * 전송 계층: 신뢰할 수 있는 통신 구현
    * 네트워크 계층: 다른 네트워크와 통신하기 위한 경로 설정 및 논리 주소 결정
    * 데이터 링크 계층: 네트워크 기기 간 데이터 전송 및 물리 주소 결정
    * 물리 계층: 시스템 간의 물리적 연결과 전기 신호를 변환 및 제어
  * 각 계층은 독립적
  * 데이터 전달되는 동안 다른 계층 영향 받지 않음
* TCP/IP
  * 7계층을 4계층으로 바꿔서 생각한 4계층 모델을 TCP/IP라 부름
  * 구성
    * 응용 계층 (응용, 표현, 세션)
    * 전송 계층
    * 인터넷 계층 (= 네트워크 계층)
    * 네트워크 접속 계층 (데이터 링크, 물리)

### 캡슐화 & 역캡슐화

* 컴퓨터에서 데이터를 보낼 때 데이터 앞부분에 전송하는 데 필요한 정보를 붙여 다음 계층으로 보내야 함
* 이때 붙이는 정보를 `헤더` 라고 부름
* 헤더에는 데이터를 전달받을 상대방에 대한 정보도 포함
* 이처럼 헤더를 붙이는 것을 `캡슐화` 라고 부름
* 데이터 받는 쪽에서 헤더를 하나씩 제거하는 걸 `역캡슐화` 라고 부름

#### 데이터의 흐름

* 송신 측 컴퓨터에서 웹사이트에 접속하려 하면
* `응용 계층` 에서 웹 사이트 접속을 위한 `요청 데이터` 가 만들어짐
* 이 데이터는 `전송 계층` 으로 전달되어 신뢰할 수 있는 통신이 이루어지도록 응용 계층에서 만들어진 데이터에 `헤더` 를 붙임
* 다음으로 다른 네트워크워 통신하기 위해 `네트워크 계층` 에서 `헤더` 를 붙임
* 물리적인 통신 채널을 연결하기 위해 `데이터 링크 계층` 에서 `헤더` 와 `트레일러` 를 붙임
  * 트레일러: 데이터 전달 시 데이터 마지막에 추가하는 정보
* 데이터 링크 계층에서 만들어진 데이터는 최종적으로 전기 신호로 변환돼어 수신 측에 도착
* 이러한 일련의 과정을 `캡슐화` 라고 부름
* 수신측엥서는 반대로 데이터 링크 계층부터 순서대로 상위 계층으로 전달됨
* 각 계층에서 헤더 or 트레일러를 제거하며 응용 계층까지 도달함



# 3. 물리 계층

## 물리 계층의 역할

### 전기 신호

* 0과 1로만 이루어진 비트열을 전기 신호로 변환하기 위해서는 OSI 모델 맨 아례 계층인 `물리 계층`의 기술이 필요
* 전기 신호의 종류
  * 아날로그 신호
  * 디지털 신호
* 아날로그 신호
  * 물결 모양
  * 전화 회선이나 라디오 방송에 사용
* 디지털 신호
  * 막대 모양
* 데이터 전송시에 송신 측 컴퓨터가 전송하는 비트열 데이터는 전기 신호로 변환되어 네트워크를 통해 수신 측 컴퓨터에 도달
  * 수신 측 컴퓨터는 전기 신호를 비트열 데이터로 복원

### 랜 카드

* 컴퓨터는 네트워크를 통해 데이터를 송수신할 수 있도록 랜 카드가 메인보드(내장형 랜카드) or 별도의 랜 카드 가짐
* 비트열 데이터는 랜 카드를 통해 전기 신호로 바뀌는 것
* 물리 계층은
  * 컴퓨터와 네트워크 장비를 연결
  * 전송되는 데이터를 전기 신호로 변환하는 계층



## 케이블의 종류 및 구조

### 트위스트 페어 케이블

* 전송 매체
  * 데이터가 흐르는 물리적인 선로
  * 크게 유선 / 무선으로 나뉨
  * 유선: 트위스트 페어 케이블, 광케이블 등
  * 무선: 라디오파, 마이크로파, 적외선 등
* 트위스트 페어 케이블 종류
  * UTP 케이블
  * STP 케이블
* UTP 케이블
  * Unshielded Twist Pair - 비차폐 연선
  * 구리 선 여덟 개를 두 개씩 꼬아 만든 네 쌍의 전선
  * `실드`로 보호되어 있지 않은 케이블
    * 실드: 금속 호일이나 금속의 매듭과 같은 것
    * 외부에서 발생하는 노이즈를 막는 역할
  * UTP 케이블은 `실드`로 보호되어 있지 않아 `노이즈`의 영향을 받기 쉬움
  * 하지만 `저렴`
* STP 케이블
  * Shielded Twist Pair - 차폐 연선
  * 두 개씩 꼬아 만든 선을 실드로 보호한 케이블

