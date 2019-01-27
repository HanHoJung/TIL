# Chapter03 케이블의 앞은 LAN 기기였다.

[TOC]

## STORY 01 케이블과 리피터 허브속에 신호가 흘러간다

> 중계 장치

이 장의 상황은 클라이언트의 LAN어댑터에서 패킷이 나가는 상황 입니다. 패킷은 허브, 라우터(중계장치)를 거쳐서 원하는 목적지에 패킷이 도착합니다.



![LAN2](./Img/LAN2.PNG)

cf)

보통, 리피터 허브 또는  스위칭 허브가 내장된 라우터를 사용 합니다. 그러나 단일 기능의 기기 하나 하나 살펴보며 설명하겠습니다.





> LAN 케이블의 신호

이 장의 상황은 클라이언트의 LAN어댑터에서 패킷이 나가는 상황 입니다.

(LAN 어댑터의 PHY(MAU) 회로에서 전기 신호로 형태를 바꾼 패킷이 RJ-45 커넥터를 통해 트위스트 페어 케이블에 흘러 들어가게 됩니다. 더불어, 이더넷의 신호는 +, -의 전압 입니다.)

![](https://t1.daumcdn.net/cfile/tistory/23344140529FCD3204)

- RJ-45커넥터에서 송출된 신호는 케이블을 통과하는 사이에 신호의 에너지가 조금씩 떨어집니다.

  (즉, 케이블의 길이가 길어질수록 신호가 약해 집니다.)

- 주파수가 높을 수록(송신측의 원래 신호에서 각진 부분은 주파수가 높음) 에너지가 떨어지는 성질 때문에 해당 부분이 뭉개짐

- 잡음이 없는 경우에도 신호가 변형되는데 잡음의 영향까지 더해지면 더욱 신호가 약해져 0과 1을 잘못 판독할  있게 되어 이것이 통신 오류의 원인이 됩니다.



> '꼼'을 통한 잡음 방지

우선, 잡음이 발생하는 원인은 다음과 같습니다.

- 신호선은 금속(도전체) 으로 만들어 졌다.

- 잡음의 원인은 케이블 주위에 발생하는 전자파 입니다.
- 금속 등의 도전체(전기가 통하기 쉬은 재료)  주위에 전자파가 있으면 신호(송·수신측이 보내는 신호)와는 다른 전류가 케이블안에 흐르게 됩니다.
- 신호도 전압에 의해 생기는 일종의 전류
- 신호와 잡음의 전류(전자파)가 뒤썩여서 신호의 파형이 변형 됩니다. 이것이 잡음 입니다.





**외부에서 오는 전자파**

- 모터, 형광등, CRT 모니터 같은 기기에서 누설되는 전자파

- 위와 같은 전자파는 케이블의 밖에서 오는 것 입니다.
- 트위스트 페어 케이블을 ''꼼"을 통해 해결할 수 있습니다.
- 신호선은 금속으로 만들어 졌고 전자파가 닿으면 전자파의 진행 방향의 오른쪽으로 전류가 생깁니다. 이 전류가 파형을 무너뜨리는 원인이 됩니다.
- 신호선을 마주 꼬면 나선형이 되어 꼰 옆의 선에서 전류가 흐르는 방향이 반대가 됩니다.
- 그 결과, 잡음에서 생긴 전류가 서로 상쇄되어 잡음에 의한 전류는 약해 집니다.



**내부에서 오는 전자파**

- 신호선 안에는 신호라는 전류가 흐르므로 전류에 의해 주위에 전자파가 생깁니다. 이것이 신호선에 대한 잡음이 됩니다. 이러한 잡음을 **크로스토크(crosstalk)**라 합니다.
- 이 잡음은 강한 것은 아니지만 거리가 가까우면 문제가 됩니다. 
- 전자파는 발생 근원에서 떨어지면 확산되어 약해지는데 한 개의 케이블 안에 있는 신호선은 거리가 가까우므로 전자파가 약해지기 전에 인접 신호선에 도달해 버립니다.
- 신호선에서 나오는 약간의 전자파가 주위의 신호선에 닿아 여기에서 전류를 발생시킴
- 이것도 신호선의 꼬는 간격을 미묘하게 변화시켜 해결할 수 있습니다.



> 리피터 허브는 연결되어 있는 전체 케이블에 신호를 송신한다.

신호가 리피터 허브에 도달하면 LAN 전체에 신호가 전달 됩니다. 

이것은 리피터 허브 이더넷의 기본원리(전체에 패킷의 신호를 뿌리고 mac 주소에 해당하는 기기만 패킷을 수신한다.)를 실현한 것입니다. (그림p198 참조)



리피터 회로의 기본 성질을 정리하자면,

- 신호를 그대로 뿌려주는 역할만 함 
- 잡음의 영향을 받은 신호도 그대로 흘려보냄
- 다음 기기(스위칭 허브, 라우터 서버 등)에 도착하여 FCS를 검사하는 곳에세 데이터가 변화가 판명된 패킷을 폐기 시킴





## STORY 02 스위칭 허브의 패킷 중계 동작

> 스위칭 허브는 주소 테이블로 패킷을 중계

스위칭 허브는 이더넷의 패킷을 그대로 목적지를 향해 전달 합니다.

<스위칭 허브의 동작>

**스위칭 허브에 리피터 허브가 접속된 경우**(현재는 이 방식 사용 안함,현재 방식 반이중 모드)

1. 스위칭 허브에 신호가 들어오면 PHY(MAU) 회로에서는 케이블의 흐르는 신호의 형식을 공통의 신호 형식으로 변환한 후에 MAC 회로로 전달한다.

2. MAC 회로에서 디지털 데이터로 변환한 후 패킷의 맨 긑에 있는 FCS를 대조하여 오류의 유무를 검사하고 오류가 발생하면 패킷을 버립니다.  오류가 발생하지 않으면 버퍼 메모리에 디지털 데이터를 저장합니다.

   (LAN 어댑터와 유사)

3. MAC 주소표를 통하여 수신한 패킷의 MAC 주소와 일치한 행을 찾고 해당 PORT 번호로 패킷을 전송해 줍니다.

   전송 전에 이더넷의 규칙을 적용하여 신호 송 수신 회로의 수신 부분에 신호가 흘러들어 오는지 아닌지 확인 합니다. 만약, 아무도 송신하지 않으면 디지털 데이터에서 신호로 변환하여 송신 합니다. 만약, 송신 동작 중에 다른 기기가 보낸 신호가 수신측에 들어오면 패킷이 충돌하므로 재밍 신호를 보낸 후 송신 동작을 중지하고 잠시 기다렸다가 패킷을 다시 전송합니다.

   



스위칭 허브 커넥터 안쪽에 있는 회로 부분을 **포트**라고 부릅니다.

- 스위칭 허브는 수신처 MAC 주소를 검사하지 않고 모든 패킷을 수신하여 버퍼 메모리에 저장합니다.
- LAN 어댑터는 MAC주소가 할당되어 있어서 수신한 패킷의 수신처 MAC 주소가 자신에게 해당하지 않는 경우에는 패킷을 폐기 합니다.
- 스위칭 허브의 포트에는 LAN어댑터와 달리 MAC 주소가 할당되어 있지 않습니다.

cf)

관리 기능 등을 수행하기 위해 프로세서를 내장한 스위칭 허브는 스위칭 허브와 컴퓨터가 들어 있어서 MAC과 IP주소가 할당되어 있습니다.

cf)

PC에 아래 같이 3가지 조건을 맞추면 스위칭 허브가 된다.

- 다수의 LAN 어댑터 장착
- 모든 패킷을 수신하는 특수한 동작 모드인 promiscuous mode(프로미스큐어스 모드)로 동작함
- 스위칭 허브와 같이 패킷을 중계하는 소프트웨어 실행



정리하자면, 스위칭 허브는 MAC 주소표에서 MAC 주소를 조사하고 해당하는 포트에서 신호를 송신 합니다.





> MAC 주소 테이블 등록 및 갱신

스위칭 허브는 패킷을 중계할 때 다음과 같은 작업을 수행 합니다.



**갱신 동작(1)**

MAC주소 테이블 등록

```
패킷을 전달 받을 때, 송신처(보낸 사람) MAC주소와 입력 포트 번호를 MAC 주소표에 등록합니다.
-송신처 MAC 주소(보낸이의 주소)
-입력 포트 번호

```



**갱신 동작(2)**

MAC주소 테이블 삭제

```
자신의 책상에서 사용하고 있던 노트북 PC를 다른 장소로 이동하여 사용한다고 가정해봅시다.
스위칭 허브에 접속된 노트북 PC는 더 이상 해당 허브에 연결되어 있지 않는 상황 입니다.
이 상태에서 누군가 노트북에게 패킷을 보낸다면 보낼 수 없게 됩니다.(해당 포트에 없으니까)
따라서, 스위칭 허브는 MAC 주소표에 등록한 정보는 그대로 두는 것이 아니라 일정 시간이 지나면 삭제 합니다.
```





>예외동작

P214 질문

주소표에 등록되어 있는 송신포트(보낸 사람 포트) 패킷을 수신한 포트가 같음

주소표에 등록되어 있는 

송신 포트 == 패킷을 수신한 포트

(보낸 사람의 포트)



어느정도 시간이 지나서 MAC 주소표에서 **삭제된 경우**와 해당 주소의 기기가 스위칭 허브에 **한 번도 패킷을 보낸지 없는** 경우 어느 포트로 전송해야 할지 모르는 상황이 옵니다.

이 때 다음과 같은 동작을 합니다.

- 패킷을 수신한 포트 이외의 전체 포트에서 패킷을 송신 합니다.(브로드 캐스트)

  (수신처 패킷은 어딘가 존재할 것이므로 이 방법을 통해 패킷이 도착 합니다.



cf)

수신처 MAC 주소가 브로드캐스트 주소인 경우에도 수신 포트를 제외하고 모든 포트에서 패킷을 송신 합니다.

브로드캐스트란, 주소를 수신처 주소로 지정하여 패킷을 보내면 네트워크에 접속된 모든 기기에 패킷이 도착한다믄 특별한 주소입니다. LAN에서 사용하는 MAC 주소는 FF:FF:FF:FF:FF:FF(255.255.255.255.255)가 브로드캐스트 주소가 됩니다.



> 전이중 모드

스위칭 허브

- 송신과 수신을 동시에 수행할 수 있습니다.(리피터 허브는 불가능)
- 전이중 모드는 송신할 때 신호가 흐르고 있어도 이것이 끝나기를 기다릴 필요가 없으므로 반이중 모드 보다 빠릅니다.
- 이더넷 자체는 다른 누군가가 신호를 보낼때 보내면 안되는 규칙이 있습니다. 그러나 전이중 모드는 이것을 위배하고 있습니다. 그래서 이더넷 규칙을 개정하여 신호가 흐르고 있어도 상관하지 않고 송신해도 좋다는 동작 모드를 새로 추가하였습니다.








