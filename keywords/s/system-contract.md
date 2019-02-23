---
description: 시스템 컨트랙트
---

# system contract

## 개요

특수한 기능을 수행하는 스마트 컨트랙트이다.

`SYSTEM` + `SMART CONTRACT`의 합성어로 특별한 기능을 수행할 수 있는 스마트 컨트랙트를 편의상 쉽게 구분하기 위하여 부르는 명칭이다. 여기서 말하는 특별한 기능이란, 실제 코어 네트워크 운영에 영향을 주는 투표하기, RAM 마켓, BP 선출과 같은 기능들을 일컫는다.

`시스템 컨트랙트`는 특수한 권한을 가진 계정만 배포할 수 있다. 참고로 일반 사용자가 배포를 하게 되면 기능이 정상적으로 동작하지 않는다.

## 시스템 컨트랙트 종류

* [eosio.bios](../e/eosio.bios.md) - 초기 설정 및 권한을 변경할 수 있다.
* [eosio.msig](../e/eosio.msig.md) - 단일 트랜잭션에 다중 서명을 할수 있도록 하는 계약이다.
* [eosio.sudo](../e/eosio.sudo.md) - 계정의 권한을 변경할 수 있다.
* [eosio.system](../e/eosio.system.md) - BP 선출, 투표, CPU, NET 스테이크 및 RAM 구매등 실제 이오스 메인넷과 동일한 환경을 구축하기 위하여 사용한다.
* [eosio.token](../e/eosio.token.md) - 토큰 발행및 송금을 할 수 있다.





