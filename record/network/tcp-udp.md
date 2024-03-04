# TCP와 UDP

TCP(Transmission Control Protocol)는 연결 지향형 프로토콜이고, 상태를 유지(Stateful)한다. IP를 통해 전달하는 패킷을 안전하게 해당 주소지까지 전달한다.

UDP(User Datagram Protocol)는 비연결형 프로토콜이고, 상태를 유지하지 않는다.(Stateless)

## TCP와 UDP의 차이

![tcp-udp-1](/record/network/images/tcp-udp-1.png)

- TCP는 신뢰성 있는 전송이 중요할 때 사용되는 프로토콜이지만 3-way-handshake로 인해 속도가 느리다는 단점이 있다.
- UDP는 TCP보다 빠르고 네트워크 부하가 적다는 장점이 있지만, 신뢰성 있는 데이터 전송을 보장하지는 않는다. 그렇기 때문에 신뢰성보다는 연속성이 중요한 실시간 스트리밍과 같은 서비스에 자주 사용된다.

## References

- https://dev-coco.tistory.com/144
