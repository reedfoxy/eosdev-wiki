# Docker에서 설치하기

## 0. 설치하기 전

해당 페이지는 Docker를 통하여 EOS를 설치하고 빌드 하는 간단한 방법에 대해서 기술한 페이지이다. 즉 Docker 사용법에 관한 상세한 내용은 포함되어 있지 않으므로, Docker가 무엇이고 정확하게 어떻게 사용을 하는지에 관해서는 Docker 공식 홈페이지 문서를 참고하여 직접 학습해야 한다.

## 1. 설치전 준비사항

{% hint style="info" %}

1. docker 17.05 이상
2. docker-compose 1.10.0 이상 \( 선택 \)

Docker에는 세부적으로 2가지 사용 방법이 있는데, 처음부터 Docker로 이미지가 생성된 파일을 다운로드하 실행하는 방법과 Github로 코드를 직접 내려받은 뒤 각 컴포넌트를 실행할 때 Docker를 사용하는 방법이 있다. 전자 같은 경우는 2번을 설치할 필요는 없다. 다시 한번 **강조**하지만 실제 서비스 용도가 아닌 개발 및 테스트 용도라면 직접 코드로 내려받는 것을 **추천**한다.

## 2. 설치 하기

```text
sudo docker pull eosio/eos-dev:v1.3.0
```

Docker 이미지를 다운로드한다. 버전은 원하는 것을 선택하면 된다. github에 올라오는 최신 버전과 약간의 텀이 있다. 참고로 해당 이미지는 이미 빌드가 완료된 상태로 업로드되었기 때문에 추가적으로 빌드를 진행할 필요가 없다. 끝 부분에 버전을 바꾸면 원하는 버전을 설치할 수 있다.

## 3. 네트워크 만들기

```text
docker network create eosdev
```

도커를 동작할때 사용할 네트워크를 만든다.

## 4. 도커로 동작시켜보기

eos는 [nodeos](../../keywords/n/nodeos.md) [keosd](../../keywords/k/keosd.md) [cleos](../../keywords/c/cleos.md) 라는 독립적인 3개의 컴포넌트로 구성이 되어 있다. 자세한 사항은 [EOS 학습순서](../eos-study/) 를 통해 참고하면 된다.

### 1\) nodeos

```text
docker run \
  --name nodeos -d -p 8888:8888 \
  --network eosdev \
  -v /tmp/eosio/work:/work \
  -v /tmp/eosio/data:/mnt/dev/data \
  -v /tmp/eosio/config:/mnt/dev/config \
  eosio/eos-dev \
/bin/bash -c \
  "nodeos -e -p eosio \
    --plugin eosio::producer_plugin \
    --plugin eosio::history_plugin \
    --plugin eosio::chain_api_plugin \
    --plugin eosio::history_api_plugin \
    --plugin eosio::http_plugin \
    -d /mnt/dev/data \
    --config-dir /mnt/dev/config \
    --http-server-address=0.0.0.0:8888 \
    --access-control-allow-origin=* \
    --contracts-console \
    --http-validate-host=false"
```

docker run 뒤에 작성되는 옵션에 대해서는 [nodeos/config.ini](../../keywords/n/nodeos-config.ini.md) 페이지를 참고하면 된다.

### 2\) keosd

```text
docker run -d --name keosd --network=eosdev \
-i eosio/eos-dev /bin/bash -c "keosd --http-server-address=0.0.0.0:9876"
```

docker run 뒤에 작성되는 옵션에 대해서는 [keosd/config.ini](../../keywords/k/keosd-config.ini.md) 페이지를 참고하면 된다.

## 5. 동작하고 있는지 확인하기

### 1\) nodeos check

```text
docker logs --tail 10 nodeos
```

위와 같은 커맨트를 입력한다.

```text
1929001ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 0000366974ce4e2a... #13929 @ 2018-05-23T16:32:09.000 signed by eosio [trxs: 0, lib: 13928, confirmed: 0]
1929502ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 0000366aea085023... #13930 @ 2018-05-23T16:32:09.500 signed by eosio [trxs: 0, lib: 13929, confirmed: 0]
1930002ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 0000366b7f074fdd... #13931 @ 2018-05-23T16:32:10.000 signed by eosio [trxs: 0, lib: 13930, confirmed: 0]
1930501ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 0000366cd8222adb... #13932 @ 2018-05-23T16:32:10.500 signed by eosio [trxs: 0, lib: 13931, confirmed: 0]
1931002ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 0000366d5c1ec38d... #13933 @ 2018-05-23T16:32:11.000 signed by eosio [trxs: 0, lib: 13932, confirmed: 0]
1931501ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 0000366e45c1f235... #13934 @ 2018-05-23T16:32:11.500 signed by eosio [trxs: 0, lib: 13933, confirmed: 0]
1932001ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 0000366f98adb324... #13935 @ 2018-05-23T16:32:12.000 signed by eosio [trxs: 0, lib: 13934, confirmed: 0]
1932501ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 00003670a0f01daa... #13936 @ 2018-05-23T16:32:12.500 signed by eosio [trxs: 0, lib: 13935, confirmed: 0]
1933001ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 00003671e8b36e1e... #13937 @ 2018-05-23T16:32:13.000 signed by eosio [trxs: 0, lib: 13936, confirmed: 0]
1933501ms thread-0   producer_plugin.cpp:585       block_production_loo ] Produced block 0000367257fe1623... #13938 @ 2018-05-23T16:32:13.500 signed by eosio [trxs: 0, lib: 13937, confirmed: 0]
```

위와 같은 메시지가 표시될 경우 정상적으로 블록을 생성하고 있음을 확인할 수 있다.

### 2\) keosd check

```text
docker exec -it keosd bash
```

위와 같은 커맨드를 입력한다.

```text
cleos --wallet-url http://127.0.0.1:9876 wallet list keys
```

wallet으로 커맨드를 날려서 현재 저장되어 있는 키를 불러온다.

```text
Wallets:
[]
```

위와 같은 문구가 뜰 경우 정상적으로 동작하고 있음을 보여준다. 만약 keosd 안에 키를 삽입했다면 삽입한 키의 리스트들이 나타날 것이다.

## 6. 코드에서 직접 docker로 동작시키기

위에 5번까지 진행을 했다면 도커로 설치 및 동작은 끝났다고 보면 된다. 6번부터 기술하는 방법은 github에서 직접 내려 받은 코드를 동작시킬때 각 컴포넌트를 도커로 동작시키는 방법에 대하여 기술한다.

