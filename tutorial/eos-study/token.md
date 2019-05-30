# 토큰 발행하기

## 개요

토큰을 발행하는 방법에 대해서 학습한다.

일반적으로 많은 사람들이 헷갈려 하는 부분이 바로 **코인**과 **토큰**의 **차이점**이다. 이오스에서는 메인 넷에서 CPU나 NET를 구매할 때 실제로 사용되는 화폐 또한 코인이라고 표현하지 않고 토큰이라고 부른다. 이는 이오스 공식 사이트에서도 확인할 수 있다.

## 스마트 컨트랙트 파일 준비하기

이오스의 모든 기능은 [스마트컨트랙트](../../keywords/s/smart-contract.md) 기반으로 동작하며 [스마트컨트랙트](../../keywords/s/smart-contract.md)를 배포함으로써 동작한다. 그 말은 토큰 기능을 사용하기 위해서는 토큰 기능이 구현되어 있는 [스마트 컨트랙트](../../posting/smart_contracts.md)를 배포하여야 한다. 여기서 학습할 토큰은 실제 이오스 네트워크에서 CPU나 NET, RAM을 구매할때 사용되는 메인 토큰이다. 이러한 기능은 Core 부분에 영향을 미치는 특수한 기능이 포함되어 있기 때문에 이런 컨트랙트를 [시스템 컨트랙트](../../keywords/s/system-contract.md)라고 부른다. [시스템 컨트랙트](../../keywords/s/system-contract.md)는 이오스를 설치할때 contract 디렉토리 안에 기본으로 포함되어 있다. 우리가 필요한 컨트랙트 이름은 [eosio.token](../../keywords/e/eosio.token.md) 이다.

### eosio.token PATH 확인

```text
cd ~/eos/build/contracts/eosio.token
ls
```

> ```text
> CMakeFiles           eosio.token.abi      eosio.token.s
> CTestTestfile.cmake  eosio.token.abi.hpp  eosio.token.wasm
> Makefile             eosio.token.bc       eosio.token.wast
> cmake_install.cmake  eosio.token.cpp.bc   eosio.token.wast.hpp
> ```

처음 이오스를 설치하고 난 이후에 특별하게 건드린게 없다면 파일이 위와 같이 있을 것이다. 물론 버전에 따라서 저장되어 있는 파일이 제각각 이겠지만 `.wast` or `.wasm` `.abi` 확장자의 파일만 있다면 배포하는데 문제가 없다.

## 토큰 발행하기

### 1. eosio.token 계정 생성하기

`eosio.token` 이라는 계정을 생성한다. 반드시 계정 이름이 **일치**하여야 한다. 계정명이 일치하지 않으면 특수 기능을 사용할 수 없다. 계정을 생성하는 방법은 이전 페이지의 [계정 생성하기](account.md) 페이지를 참고하자. 특수 기능을 사용하지 않고 자신만의 토큰을 발행하고자 한다면 어떠한 계정 이름이든 상관없다.

### 2. eosio.token 컨트랙트 배포하기

```text
cd ~/eos/build/programs/cleos
./cleos set contract eosio.token ~/eos/build/contracts/eosio.token
```

`./cleos set contract` : 스마트 컨트랙트를 배포할때 사용하는 커맨드 명령어 이다.

`eosio.token` : 해당 스마트 컨트랙트를 배포할 계정명을 입력한다.

`~/eos/build/contracts/eosio.token` : 실제 스마트컨트랙트 파일 \( abi, wasm \) 이 존재하는 디렉토리 위치를 명시한다.

> ```text
> Reading WASM from /eos/build/contracts/eosio.token/eosio.token.wasm...
> Publishing contract...
> executed transaction: c6c8b4d4bf8afd1968ff942dfe879daaeb372ce0bdffacc4042454ba1b11159b  8104 bytes  15087 us
> #         eosio <= eosio::setcode               {"account":"eosio.token","vmtype":0,"vmversion":0,"code":"0061736d01000000017e1560037f7e7f0060057f7e...
> #         eosio <= eosio::setabi                {"account":"eosio.token","abi":"0e656f73696f3a3a6162692f312e30010c6163636f756e745f6e616d65046e616d65...
> ```

위와 같은 메세지가 뜬다면 정상적으로 배포에 성공한 것이다.

### 3. 토큰 최대 공급량 설정하기

토큰 발행하는 코드를 살펴보면 총 3가지의 액션이 있음을 알 수 있다. 바로 create , issue, transfer 이다. 자세한 내용은 [eosio.token](../../keywords/e/eosio.token.md) 페이지를 참고하면 된다. 최대 공급량은 말 그대로 최대로 발행할 수 있는 토큰의 수량이다. 이 한계점에 도달하면 더이상 토큰 발행이 되지 않는다. 참고로 이오스에서 최대 발행 가능한 토큰의 수량은 100조이다. 원하는 금액을 설정 하면 된다. 다만 최소 10억개 이상을 발행을 **권장**한다. 그 이유는 메인넷을 구성할때 설명하도록 하겠다.

```text
./cleos push action eosio.token create '["eosio","1000000000.0000 SYS","memo"]' -p eosio.token
```

`./cleos push action` : 모든 스마트 컨트랙트에서 액션을 실행할 때 사용하는 명령어 이다.

`eosio.token` : 스마트컨트랙트를 배포한 계정명을 입력한다.

`create` : 해당 스마트 컨트랙트의 액션명을 입력한다. 최대 발행량을 설정하기 위한 액션명은 create 이다.

`"eosio"` : 발행할 수 있는 권한을 가진 계정명을 입력한다.

`"1000000000.0000 SYS"` : 최대 발행 수량을 설정한다. SYS는 화폐명칭 이며 디폴트 메인토큰 심볼로 지정되어 있다. 화폐명칭은 마음대로 변경할 수 있으나 디폴트 메인 토큰 심볼이 SYS로 설정되어 있기 때문에 SYS로 발행해야 램 구매나 CPU, NET 자원 구매에 사용할 수 있는 메인 토큰의 기능을 사용할 수 있다. 물론 디폴트로 지정되어있는 SYS를 변경할수도 있는데 `eosio_build.sh` 에서 빌드 전 메인토큰으로 사용할 심볼 이름을 변경할 수 있다. 예를들어 현재 이오스 메인넷에서 사용하고 있는 EOS라는 심볼처럼 말이다. 일단은 지금은 학습 용도로 사용하기 때문에 디폴트값인 SYS로 사용하자.

`"memo"` : 말 그대로 메모이다. 그냥 자신이 원하는 것을 아무거나 입력해도 된다. 이 단계에서는 생략해도 된다.

`-p eosio.token` : -p는 permission의 약자이며 이 트랜잭션을 실행하는 실행자의 계정명을 입력한다.

> ```text
> executed transaction: 4f4dfc3e6f5e6bf1e3eb3e76848ce5a2a303247b3655d418520e40b51689fd48  120 bytes  2024 us
> #   eosio.token <= eosio.token::create          {"issuer":"eosio","maximum_supply":"1000000000.0000 SYS"}
> ```

총 10억개의 최대 공급량이 정해져 있는 SYS 토큰 설정을 완료한 것이다. 그러나 최대공급량만 설정한 것일뿐 실제로 토큰이 발행 된것은 아니다.

### 4. 토큰 발행하기

```text
./cleos push action eosio.token issue '["eosio","1000.0000 SYS","memo"]' -p eosio
```

`./cleos push action` : 모든 스마트 컨트랙트에서 액션을 실행할 때 사용하는 명령어

`eosio.token` : 스마트컨트랙트를 배포한 계정명을 입력한다.

`issue` : 해당 스마트 컨트랙트의 액션명을 입력한다. 발행하기 위한 액션명은 issue 이다.

`"eosio"` : 토큰 발행 권한이 있는 계정명을 입력한다. 3번 토큰 최대 공급량 설정하기에서 입력한 계정명을 입력해야 한다.

`"1000.0000 SYS"` : 실제 발행하고자 하는 토큰 수량을 입력한다.

`"memo"` : 메모를 입력한다. 이 단계에서는 메모를 생략할 수 없고, 반드시 입력해야 한다.

`-p eosio` : -p는 permission의 약자이며 이 트랜잭션을 실행하는 실행자의 계정명을 입력한다. 여기서는 실제 발행하고자 하는 계정은 3번에서 설정해 두었던 eosio 계정이기 때문에 여기서는 eosio.token이 아닌 eosio를 입력하여야 한다.

> ```text
> executed transaction: 0b0a770194c975e64cda0ae5251e2fab6b27544dfb2d657b69d18c9c7cb0a1e5  128 bytes  3163 us
> #   eosio.token <= eosio.token::issue           {"to":"eosio","quantity":"1000.0000 SYS","memo":"memo"}
> ```

총 1000개의 SYS 토큰을 정상적으로 발행하였다.

### 5. 내가 보유중인 토큰 확인하기

실제로 1000.000 SYS 토큰이 발행이 되었는지 확인해보자.

```text
./cleos get currency balance eosio.token eosio sys
```

`./cleos get currency balance` : 현재 보유중인 토큰을 확인하기 위한 명령어

`eosio.token` : 토큰을 배포한 계정 이름을 입력한다.

`eosio` : 실제 토큰을 보유하고 있는지 확인하고 싶은 계정 이름을 입력한다.

`sys` : 토큰의 심볼을 입력한다.

> ```text
> 1000.0000 SYS
> ```

그럼 위와같이 정상적으로 토큰이 발행된 것을 알 수 있다.

### 6. 토큰 송금하기

다른 계정으로 토큰을 송금해보자

```text
./cleos push action eosio.token transfer '["eosio","eosio.token","10.0000 SYS","memo"]' -p eosio
```

`./cleos push action` : 모든 스마트 컨트랙트에서 액션을 실행할 때 사용하는 명령어

`eosio.token` : 스마트컨트랙트를 배포한 계정명을 입력한다.

`transfer` : 해당 스마트 컨트랙트의 액션명을 입력한다. 송금하기 위한 액션명은 transfer 이다.

`"eosio"` : 현재 돈을 보내고자 하는 계정명을 입력한다.

`"eosio.token"` : 돈을 받을 계정명을 입력한다.

`"10.0000 SYS"` : 보낼 액수를 입력한다.

`"memo"` : 메모를 입력한다.

`-p eosio` : 트랜잭션을 실행하고자 하는 계정명을 입력한다. 여기서는 돈을 보내고자 하는 계정명과 일치해야 한다.

> ```text
> executed transaction: e610c45e9f9e60cdeb430dce6938a930e16c1cf2cd45b4a653647e9b0a46521a  136 bytes  2206 us
> #   eosio.token <= eosio.token::transfer        {"from":"eosio","to":"eosio.token","quantity":"10.0000 SYS","memo":"memo"}
> #         eosio <= eosio.token::transfer        {"from":"eosio","to":"eosio.token","quantity":"10.0000 SYS","memo":"memo"}
> ```

`eosio` 계정에서 `eosio.token` 계정으로 성공적으로 토큰을 송금한것을 확인할 수 있다. 실제로 보유중인 토큰을 조회하면 `eosio` 계정은 `990.0000 SYS` 으로 줄어든것을 볼 수 있고, `eosio.token`은 `10.0000 SYS`를 보유중인것을 확인할 수 있다.

여기까지 완료 했다면 토큰 발행과 송금에 관한 내용은 전부 학습한 것이다.

