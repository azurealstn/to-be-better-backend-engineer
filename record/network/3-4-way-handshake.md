# TCP 3, 4 way handshake

TCP 3 Way Handshake는 TCP/IP프로토콜을 이용해서 통신을 하는 응용프로그램이 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해 연결을 진행한다.

## TCP의 연결 및 연결 해제 과정

### TCP의 3-way Handshaking 연결 과정

![3-way-handshake-1](/record/network/images/3-way-handshake-1.png)

1. Client -> Server: 데이터 전송이 잘 갔는지 SYN을 보낸다.
2. Server -> Client: 잘왔다는 응답과 함께 SYN+ACK을 보낸다.
3. Client -> Server: 마무리 ACK 응답

- 3-way Handshaking는 물리적으로 연결된 것이 아닌 논리적으로 연결되었다.

> SYN(synchronize sequence numbers): 연결 확인을 보내는 무작위의 숫자 값  
> ACK(acknowledgements): Client 혹은 Server로부터 받은 SYN에 1을 더해 SYN을 잘 받았다는 ACK

### TCP의 4-way Handshaking 연결 해제 과정

![3-way-handshake-2](/record/network/images/3-way-handshake-2.png)

1. Client -> Server : FIN(연결 끊자!)을 보낸다.
2. Server -> Client : ACK로 응답
3. Server -> Client : 잠시 후 FIN을 보낸다.
4. Client -> Server : 마무리 ACK로 응답

## References

- https://dev-coco.tistory.com/144
- https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake
