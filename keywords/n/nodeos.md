# nodeos

## 개요

실질적으로 이오스 블록체인을 구동하는 데몬이다.

속도를 비약적으로 향상시키기 위하여 내부적으로 웹어셈블리를 사용한다. 그리고 `nodeos` 는 다양한 플러그인으로 구성되어 있는 거대한 인터페이스라고 보면 된다. `nodeos` 자체는 사실 껍데기 이며 실질적인 처리는 모두 플러그인에서 담당한다.

## 파일 위치

[Github로 설치하기](../../tutorial/eos-install/github.md) 방법으로 설치를 했을경우 파일 위치는 아래와 같다. 위에도 언급했지만 `nodeos` 는 플러그인을 구동시키기 위한 인터페이스 역할만 담당하며 실질적인 처리는 모두 플러그인에서 처리한다.

### 1. build 전

EOS를 홈 디렉터리에 설치 했다면 위치는 아래와 같다.

```text
~/eos/programs/nodeos/main.cpp
```

### 2. build 후

EOS를 홈 디렉터리에 설치 했다면 위치는 아래와 같다.

```text
~/eos/build/programs/nodeos/nodeos
```

## 플러그인 종류

* `bnet_plugin` : 
* `history_plugin` : trasnaction 모든 기록을 저장하는 플러그인
* `history_api_plugin` : 외부에서 history\_plugin에 접근할수 있도록 정의된 플러그인
* `chain_plugin` : blockchain을 구동하기 위한 플러그인
* `chain_api_plugin` : 외부에서 chain\_plugin에 접근할수 있도록 정의된 플러그인
* `faucet_testnet_plugin` : 
* `http_plugin` : http-rpc로 전달받는 데이터를 각 api 플러그인으로 핸들링 하는 플러그인
* `net_api_plugin` : 외부에서 net\_plugin에 접근할수 있도록 정의된 플러그인
* `net_plugin` : 노드들끼리 서로 통신할 수 있는 플러그인
* `producer_plugin` : block을 생성할때 동작되는 플러그인
* `txn_test_gen_plugin` : TPS를 테스트하기 위하여 트랜잭션을 발생시켜주는 플러그인
* `mongo_db_plugin` : 파일로저장된 블록 데이터를 몽고DB에 함께 저장시켜주는 플러그인

## 블럭 복구 옵션

