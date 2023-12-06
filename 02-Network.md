## 도커 네트워크 

도커는 컨테이너에 내부 IP를 순차적으로 할당하며, 이 IP는 컨테이너를 재시작 할 때마다 변경된다.

외부와 통신해야할 경우 사용자의 선택에따라 여러 네트워크 드라이버를 쓸 수 있다.

사용할 수 있는 네트워크 목록을 확인 

```bash
docker network ls
```

### 브리지 네트워크

```bash
docker network inspect bridge
```

브리지 네트워크는 사용자 정의 브리지를 새로 생성하여 각 컨테이너에 연결하는 네트워크 구조이다.

다음 명령어를 이용하여 새로운 브리지 네트워크를 생성한다.

```bash
docker network create --driver bridge mybridge
```

```bash
docker run -i -t --name mynetwork_container \
--net mybridge \
ubuntu:14.04
```

이후 컨테이너 내부에서 ifconfig 로 새로운 IP 대역이 할당된 것을 알 수 있다.

사용자 정의 브리지 네트워크는 connect, disconnect 를 통해 유동적으로 붙이고 뗄 수 있다.

```bash
docker network disconnect mybridge mynetwork_container
docker network connect mybridge mynetwork_container
```

