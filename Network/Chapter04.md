# Chapter04 액세스 회선을 통해 인터넷 내부로

[TOC]

## STORY 01 ASDL 기술을 이용한 액세스 회선의 구조와 동작

> 가정·회사 LAN과 인터넷

가정·회사 LAN과 인터넷은 규모의 차이가 있지만, 공통적으로 라우터를 거쳐서 원하는 도착지점으로 패킷을 전송하는데 있습니다.

그러나  다음과 같은 차이점이 있습니다.

- **거리의 차**

  가정이나 회사의 LAN의 경우, 중계 장치간의  거리가 수백미터 정도 되지만 인터넷의 중계장치의 거리는 수 킬로미터가 넘습니다. 예를들어 대한민국과 미국을 연결한다면 단순히 이더넷 케이블로 연결하기 어렵습니다.

  

- **경로정보의 등록방법의 차이**

  기본적으로, 경로 정보에 기초하여 목적지에 패킷을 보내는 것의 같으나, 경로표에 정보를 등록하는 부분이 다릅니다.



> 액세스 회선

이 챕터에서 설명할 상황은 다음과 같습니다.

Client=>스위칭 허브=>이더넷 라우터=>인터넷=>목적지 서버

인터넷 라우터에 접속할 때 라우터의 패킷 송신 동작은 이더넷의 패킷 송신 동작과는 다른 부분이 있습니다.



즉, 먼거리에 대하여 정보를 전송해야 하기 때문에, 인터넷 접속용 라우터는 액세스 회선을 사용합니다.

액세스 회선은, 가정·회사의 LAN과 인터넷을 연결해주는 통신 회선을 의미합니다. 따라서, 액세스 회선 규칙을 따라야 합니다.

- 가정:ADSL, FTTH,CATV,전화회선, ISDN 등 (액세스 회선 종류)
- 회사:전용회선(액세스 회선 종류)



> ASDL

1. **사용자측 PC에서 패킷을 전송**

2. **사용자측 라우터=>ASDL모뎀 또는 전화 케이블**

   인터넷 접속용 라우터는 패킷을 ASDL모뎀에 보낼 때

   MAC헤더, PPPoE 헤더, PPP 헤더 세 가지를 붙이고 ASDL 모뎀에 패킷을 전송합니다.

   (PPPOE 경우)

​     < 패킷의 모습>

​       MAC헤더, PPPoE 헤더, PPP 헤더,IP헤더,데이터

3. **ASDL모뎀**

   패킷을 작게 분할하여 셀에 저장하고 전기신호로 바꾸어 스플리터에 송신

4. **스플리터에서 DSLAM로 패킷 전송**

   전화국에서는 다수의 사용자로부터 패킷을 전송받기 때문에 여러개의 ASDL 모뎀이 필요합니다. 때문에 DSLAM을 사용합니다.

   DSLAM이란, 다수의 ASDL 모뎀에 해당하는 기능을 묶어서 하나의 케이스에 넣은 장치 입니다.

   전기신호->셀

5. **DSLAM에서 BAS(광대역 액세스 서버)로 전송**

   - BAS는 ATM셀을 2번에서 보낸 형태의 모습으로 변환(즉, PPPoE헤더,MAC헤더 버림)

     PPoE,MAC헤더는 이전 단계에서 BAS로 도착할 때 사용되었으므로 현재 필요 없음

   - 터널링용 헤더를 붙여 터널링용 라우터에 패킷 송신(L2TP터널링 경우)

6. **BAS(광대역 액세스 서버)에서 터널링용 라우터 도착**

   - 터널링용 라우터는 터널리용 헤더를 분리하고 IP패킷 추출
   - 인터넷 라우터에 패킷을 중계



cf)

BAS

- Broadband Access Server. 라우터의 일종



PPP

- Point-to-Point protocol
- 전화회선이나 ISDN 등의 통신회선을 사용하여 통신할 때 사용하는 구조
- 본인 확인, 설정값 통지, 데이터 압축, 암호화 등 다양한 기능 사용 가능

   

