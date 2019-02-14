# nodeos

## 개요

실질적으로 이오스 블록체인을 구동하는 데몬이다.

속도를 비약적으로 향상시키기 위하여 내부적으로 웹어셈블리를 사용한다. 그리고 `nodeos` 자체는 플러그인을 구동하기 위한 백엔드이며 그 위에 다양한 플러그인이 상호 동작하여 노드를 구성한다.

## 파일 위치

[Github로 설치하기](../../tutorial/eos-install/github.md) 방법으로 설치를 했을경우 파일 위치는 아래와 같다.

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

## 내부 통신 규약

## 블럭 복구 옵션

