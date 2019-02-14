# nodeos/config.ini

## 개요

nodeos 환경설정 파일

블록체인 네트워크를 구성하고 있는 노드의 환경설정을 할 수 있는 파일이다. 한번이라도 [nodeos](nodeos.md)를 구동해야지만 자동 생성된다. 

## 파일 위치

[Github로 설치하기](../../tutorial/eos-install/github.md) 방법으로 설치를 했을경우 환경설정 파일의 주소는 아래와 같다. 다만 최초로 설치하고 나서 한번이라도 [nodeos](nodeos.md) 를 구동한적이 있어야 환경설정 파일이 자동으로 생성 되므로 참고하자.

### 1. Linux

리눅스 경우 따로 패스를 설정해 두지 않았다면 디폴트 저장소 위치는 으로 아래와 같다. 

```text
~/.local/share/eosio/nodeos/config/config.ini
```

### 2. Mac os

맥OS 패스를 따로 설정해 두지 않았다면 디폴트 저장소 위치는 으로 아래와 같다. 

```text
~/Library/Application\ Support/eosio/nodeos/config/config.ini
```

## 기능 파헤치기

아래에 표시된 기능들은 [v1.5.1](../../document/release-notes/v1.5.1.md) 기준으로 작성 되었음. 버전에 따라서 환경설정 내용이 조금 틀릴 수 있다.



