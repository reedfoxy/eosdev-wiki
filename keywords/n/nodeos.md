# nodeos

## 개요

실질적으로 이오스 블록체인을 구동하는 데몬이다.

쉽게 말해 블록체인 서버다. 개별적인 단위의 의미로 노드 라고 한다.  `nodeos`는 다양한 플러그인으로 구성되어 있는 거대한 인터페이스 이며 실질적인 처리는 모두 플러그인에서 담당한다. 플러그인의 목록을 알고 싶다면 [하단 참조](nodeos.md#undefined-3).

아키텍처 부분에서 `nodeos`를 플러그인 형태로 구현한 것은 칭찬 할 만한 부분이다. 원래 유지 보수 및 업데이트를 하게 되면 스파게티 코드가 되는 일이 매우 흔한데, `EOS`는 플러그인 형태로 깔끔하게 구분을 해 두었다. 특히 내부적으로 HTTP 프로토콜을 사용하는데 무조건 `http_plugin`을 통하여 각 플러그인으로 전달되는 점과 기능별로 플러그인을 구현해 두어 원하는 기능이 어느 플러그인에 포함되어 있는지 쉽게 파악할 수 있다. 또한 노드에 필요한 플러그인을 직접 제작해서 사용하기에도 편리하다. 실제로 [`BP`](../b/bp.md) 들의 경우 내장되어 있지 않은 특별한 기능을 사용하기 위하여 직접 구현한 플러그인을 붙여서 사용하기도 한다.

## 모듈간의 관계

[EOS Github](https://github.com/EOSIO/eos) 에서 코드를 다운받으면 대표적으로 3가지 모듈이 포함되어 있다. `nodeos`, `cleos`, `keosd` 이다. 3가지의 모듈에 대해 쉽게 표현하자면

* [`nodeos`](nodeos.md) : 노드 서버
* [`cleos`](../c/cleos.md) : 클라이언트
* [`keosd`](../k/keosd.md) : 지갑 서버

으로 나타낼 수있다. 노드 서버는 말 그대로 실제 블록체인을 구동하는 노드를 의미하고, 클라이언트는 노드서버와 월렛서버에 접근하여 명령을 내리고 결괏값을 받는 행위를 한다. 다만 위에서 언급한 `cleos` 와 `keosd`는 개발자나 [BP](../b/bp.md)가  편리하게 사용하기 위하여 만들어놓은 모듈이고, 실제 일반 사용자가 사용할 일은 전혀 없다. 그렇기에 휴대폰 앱에 깔려있는 지갑이나 Scatter 같은 지갑은  `cleos` + `keosd`의 역할을 하는 어플리케이션이다.

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

## nodeos 환경설정

[nodeos/config.ini](nodeos-config.ini.md) 페이지 참고

## 구동 옵션

nodeos를 구동할때 사용되는 옵션이다. 일반적으로 아래와 같이 노드를 구동할때 옵션으로 뒤에 붙여 입력한다.

```text
nodeos --genesis-json genesis.json 
```

### 옵션 리스트

* --genesis-json : 
* --genesis-timestamp : 
* --print-genesis-json : 
* --extract-genesis-json :
* --fix-reversible-blocks
* --force-all-checks
* --disable-replay-opts
*  --replay-blockchain
* --hard-replay-blockchain
* --delete-all-blocks
* --truncate-at-block
* --import-reversible-blocks
* --snapshot



