# NET

## 개요

[NET](net.md)는 트랜잭션을 실행하기 위하여 필요한 자원의 기본요소 3가지\( [CPU](https://eosdev.wiki/keywords/c/cpu) , [NET](https://eosdev.wiki/keywords/n/net) , [RAM](https://eosdev.wiki/keywords/r/ram) \) 중 하나이다.

## NET stake/unstake의 개념

![account : eos \( site : eoscanner.io \)](https://github.com/bon-k/eosdev-wiki/tree/792c592946e9831dff65a18ded8dc5cb5733bd8a/.gitbook/assets/eos_scanner.png)

[NET](net.md)를 할당받기 위해서는 stake 라는 행위를 해야 한다. 여기서 stake의 뜻은 "지분" 이라는 의미로 사용된다. 구매라는 표현을 쓰지않고 지분이라고 표현한 이유는, 21개의 [BP](https://eosdev.wiki/keywords/b/bp)의 컴퓨터 성능에 따라서 총 [NET](net.md) 성능이 계산되고 EOS 토큰 비율만큼 지분을 할당받기 때문이다.

staking을 하게 되면 내가 가지고 있는 EOS 토큰 만큼 [NET](net.md) 지분을 할당받게 되며 내가 staking 한 토큰은 더 이상 송금을 할 수 없는 홀딩 상태가 된다. 물론 반대로 unstaking을 통하여 할당받은 지분을 포기하고 홀딩 시킨 나의 **EOS 토큰을 돌려받을 수** 있다. 다만 이 경우는 3일이 지나야 한다. 여기서 핵심은 돌려받을 수 있다는 점이다. 이더리움이나 비트코인같이 수수료로 지불한 금액을 돌려 받지 못하는것이 아니다. 그래서 타 블록체인에 비해서 수수료가 저렴하다는 의미가 전혀 틀린말은 아니라고 볼 수 있다.

### NET를 stake/unstake 할 수 있는 방법

#### 1. 직접 stake 하기

메인 플랫폼 EOS 토큰이 필요하다. [cleos](../c/cleos.md) 커맨드라인 툴을 이용해서 직접 할당 받을 수도 있고, 누군가가 쉽게 구현 해놓은 외부 어플리케이션을 이용하는 방법도 있다. 둘다 내부적으로 동작하는 방법은 동일하다고 보면 된다. [eosio.system](../e/eosio.system.md) 페이지를 참고하면 [cleos](../c/cleos.md) 로 직접 할당 받는 방법에 대해서 확인할 수 있다.

#### 2. 다른사람에게 delegate 하기

직접 할당 받는것이 아닌 임대받는 방법도 있다. [cleos](../c/cleos.md) 커맨드라인 툴을 이용해서 다른사람에게 임대를 할 수 있고, 외부 어플리케이션을 이용하는 방법도 있다. 둘다 내부적으로 동작하는 방법은 동일하다고 보면 된다. [eosio.system](../e/eosio.system.md) 페이지를 참고하면 [cleos](../c/cleos.md) 로 직접 임대 하는 방법에 대해서 확인할 수 있다.

#### 3. 직접 unstake 하기

[cleos](../c/cleos.md) 커맨드라인 툴을 이용해서 직접 unstake를 할 수 있고, 외부 어플리케이션을 이용하는 방법도 있다. 둘다 내부적으로 동작하는 방법은 동일하다고 보면 된다. [eosio.system](../e/eosio.system.md) 페이지를 참고하면 [cleos](../c/cleos.md) 로 직접 할당을 취소 하는 방법에 대해서 확인할 수 있다.

#### 2. undelegate 하기

[cleos](../c/cleos.md) 커맨드라인 툴을 이용해서 직접 delegate를 취소 할 수 있고, 외부 어플리케이션을 이용하는 방법도 있다. 둘다 내부적으로 동작하는 방법은 동일하다고 보면 된다. [eosio.system](../e/eosio.system.md) 페이지를 참고하면 [cleos](../c/cleos.md) 로 직접 임대를 취소 하는 방법에 대해서 확인할 수 있다.

## NET를 측정하는 단위

![net \( site : eoscanner.io \)](https://github.com/bon-k/eosdev-wiki/tree/792c592946e9831dff65a18ded8dc5cb5733bd8a/.gitbook/assets/net_scanner.png)

[NET](net.md)의 단위를 보게되면 byte / MB 으로 미루어 보아 데이터 용량 단위라는것을 알수 있다.

이오스에서 [NET](net.md)를 측정 하는 기준은 최종적으로 [BP](https://eosdev.wiki/~/drafts/-LWOzA0TPlO9v01J7Tec/primary/keywords/b/bp) 에게 전달된 트랜잭션 데이터 사이즈를 의미한다. 원래 여기서 의미하는 [NET](net.md)란 bandwidth 대역폭을 의미하지만 이는 정확하게 측정할 수 있는 방법이 없기 때문에 이오스에선 단순히 트랜잭션에 차지하는 데이터 사이즈를 기준을 판단한다.

## NET 사용량 초기화 기준

사용량이 최대치에 도달했다고 해서 더 이상 사용을 못 하는 것은 아니다. [NET](net.md) 사용량 측정 기준은 최근 3일 이내의 [NET](net.md)평균 사용량을 가지고 현재 사용한 [NET](net.md)를 측정한다. 쉽게 설명하자면 3일 동안 트랜잭션을 한 건도 발생시키지 않았다면 사용한 [NET](net.md)는 0이 된다. 이러한 이유 때문에 무료로 쓸 수 있다는 말을 하는 것이다. 참고로 이 사용량 기준은 실시간으로 갱신이 이루어지는 것은 아니고, 트랜잭션을 발생시킬 때마다 갱신이 이루어지기 때문에 최소 1건 이상의 트랜잭션을 전송해야 실제로 갱신된 값을 확인할 수 있다. 아무래도 실시간으로 계속해서 변경한다면 서버에 부담이 될테니까 말이다.

