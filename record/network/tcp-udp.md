# TCP와 UDP

TCP와 UDP는 전송 계층(Transport Layer)에 해당된다.

## TCP 특징

- TCP(Transmission Control Protocol)는 연결 지향형 프로토콜이다.
- 상태를 유지한다. (Stateful)
- 데이터 전달 보장: IP를 통해 전달하는 패킷을 안전하게 해당 주소지까지 전달한다.
- 순서 보장

즉, TCP는 신뢰성 있는 프로토콜이다. 대부분 어플리케이션은 TCP 프로토콜을 사용한다.

> TCP가 신뢰성 있는 프로토콜인 이유는 바로 TCP 3, 4 way handshake가 동작하기 때문이다.

## UDP 특징

- UDP(User Datagram Protocol)는 비연결형 프로토콜이다.
- 상태를 유지하지 않는다. (Stateless)
- 데이터 전달 보장 X
- 순서 보장 X
- TCP 3, 4 way handshake 과정을 거치지 않기 때문에 빠르다.
- IP와 거의 같고 PORT와 체크섬 정도만 추가된다.

## TCP와 UDP의 차이

![tcp-udp-1](/record/network/images/tcp-udp-1.png)

- TCP는 신뢰성 있는 전송이 중요할 때 사용되는 프로토콜이지만 3-way-handshake로 인해 속도가 느리다는 단점이 있다.
- UDP는 TCP보다 빠르고 네트워크 부하가 적다는 장점이 있지만, 신뢰성 있는 데이터 전송을 보장하지는 않는다. 그렇기 때문에 신뢰성보다는 연속성이 중요한 실시간 스트리밍과 같은 서비스에 자주 사용된다.

## References

- https://dev-coco.tistory.com/144
