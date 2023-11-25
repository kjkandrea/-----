# 시작하세요! 도커/쿠버네티스

## 도커 이미지

컨테이너를 생성할 때 필요한 요소.
컨테이너를 생성하고 실행할 때 읽기 전용으로 사용된다.

## 도커 컨테이너

이미지를 통해 생성 됨.
파일시스템과 격리된 시스템 자원 및 네트워크를 사용할 수 있는 독립된 공간을 생성한다.
특정 컨테이너에 어떤 애플리케이션을 설치하거나 삭제해도 다른 컨테이너와 호스트에는 영향을 주지 않는다.

## 컨테이너 애플리케이션 구축

mysql 이미지를 사용해 데이터베이스 컨테이너를 생성한다.

```bash
docker run -d \
--name wordpressdb \
-e MYSQL_ROOT_PASSWORD=password \
-e MYSQL_DATABASE=wordpress \
--platform linux/amd64 \
mysql:5.7
```

워드프레스 이미지를 사용해 워드프레스 웹 서버 컨테이너를 생성한다.

```bash
docker run -d \
-e WORDPRESS_DB_HOST=mysql \
-e WORDPRESS_DB_USER=root \
-e WORDPRESS_DB_PASSWORD=password \
--name wordpress \
--link wordpressdb:mysql \
-p 80 \
wordpress
```

## -i -t vs -d

* `docker run -i -t` : 표준 입출력이 활성화된 상호작용이 가능한 쉘 환경을 사용한다.
* `docker run -d` : 입출력이 없는 상태로 컨테이너를 실행한다.
