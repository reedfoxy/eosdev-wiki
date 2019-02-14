# 싱글노드로 구동하기

## 개요

로컬에서 싱글노드로 이오스를 구동하는 방법에 대해 학습한다.

간단한 테스트 및 사용법을 익히기에는 로컬에서 싱글로 동작하는 노드만 있다면 충분하다. 멀티노드로 구성하는 방법은 이후에 서술한다. 지금은 멀티노드에 대해서는 생각을 접어두고, 전반적인 사용방법에 대해서 학습을 하도록 하자.

## 사전 준비

학습 순서를 진행하기 위해서는 EOS를 먼저 설치하여야 한다.

[EOS 설치하기](../eos-install/) 페이지에서 보는 바와 같이 여러가지 설치 방법이 존재한다. 사용법은 비슷하지만 코드를 분석하는데 있어서 [Github로 설치하기](../eos-install/github.md) 가 좀더 편리하고 직관적이기에 해당 페이지에서는 [Github로 설치하기](../eos-install/github.md) 를 기준으로 설명하니 참고하길 바란다. 그리고 학습의 이해를 위해서는 **EOS 저장 directory를 통일할 필요가 있다.** 앞으로 **EOS는 Home Directory \(~/eos\)에 저장을 했다는 가정으로 진행**을 한다. 물론 본인이 저장하고 싶은 곳에 저장을 해도 상관은 없으나 학습하기를 진행할 때 홈 디렉터리 기준으로 서술되어 있기 때문에 헷갈릴 수 있다. 이왕이면 동일하게 홈 디렉터리로 통일하는 것을 **추천**한다.

## 싱글 노드로 구동하기

이오스 공식 홈페이지 [\[ Local Single-node Testnet \]](https://developers.eos.io/eosio-nodeos/docs/local-single-node-testnet) 페이지를 참고해보면 nodeos 뒤에 여러 가지 옵션을 설정하여 동작 시키는 것을 볼 수 있다. 물론 이렇게 구동하여도 상관없지만 이러한 방법은 처음 이오스를 구동할 때 혼란을 가져올 수 있으므로 우리는 환경설정 파일을 직접 수정하여 구동하는 방법에 대해서 알아보도록 한다.

### 1. 최초 nodeos 실행

```text
cd ~/eos/build/programs/nodeos
./nodeos
```

{% hint style="info" %}
[Github로 설치하기](../eos-install/github.md) 페이지에서 sudo ./eosio\_install.sh 스크립트를 실행했었다면 디렉터리로 이동하지 않고 전역으로 nodeos라는 커맨드만 입력해도 동일하게 동작한다. 그러나 초반에는 eos의 PATH를 익히기 위하여 직접 이동하여 동작하는 습관을 기르도록 하자. 자동 쉘 스크립트 기능은 나중에 익숙해진 이후에 사용하자.
{% endhint %}

위와 같이 입력할 경우 아래와 같은 메세지가 출력 될 것이다.

> ```text
> info  2018-12-19T05:29:07.945 thread-0  chain_plugin.cpp:333          plugin_initialize    ] initializing chain plugin
> warn  2018-12-19T05:29:07.947 thread-0  chain_plugin.cpp:615          plugin_initialize    ] Starting up fresh blockchain with default genesis state.
> info  2018-12-19T05:29:07.971 thread-0  http_plugin.cpp:422           plugin_initialize    ] configured http to listen on 127.0.0.1:8888
> info  2018-12-19T05:29:07.971 thread-0  net_plugin.cpp:2898           plugin_initialize    ] Initialize net plugin
> info  2018-12-19T05:29:07.972 thread-0  net_plugin.cpp:2924           plugin_initialize    ] host: 0.0.0.0 port: 9876 
> info  2018-12-19T05:29:07.972 thread-0  net_plugin.cpp:2995           plugin_initialize    ] my node_id is 7768ebeaa9ac5e69cdb0c449f563fc6ed16e22e98fa8552885c5905bcb89a6d2
> info  2018-12-19T05:29:07.974 thread-0  main.cpp:107                  main                 ] nodeos version v1.5.0
> info  2018-12-19T05:29:07.974 thread-0  main.cpp:108                  main                 ] eosio root is /Users/admin/Library/Application Support
> info  2018-12-19T05:29:07.974 thread-0  main.cpp:109                  main                 ] nodeos using configuration file /Users/admin/Library/Application Support/eosio/nodeos/config/config.ini
> info  2018-12-19T05:29:07.974 thread-0  main.cpp:110                  main                 ] nodeos data directory is /Users/admin/Library/Application Support/eosio/nodeos/data
> error 2018-12-19T05:29:07.975 thread-0  controller.cpp:1750           startup              ] No head block in fork db, perhaps we need to replay
> warn  2018-12-19T05:29:07.976 thread-0  controller.cpp:601            initialize_fork_db   ]  Initializing new blockchain with genesis state                  
> info  2018-12-19T05:29:08.598 thread-0  chain_plugin.cpp:724          plugin_startup       ] starting chain in read/write mode
> info  2018-12-19T05:29:08.598 thread-0  chain_plugin.cpp:728          plugin_startup       ] Blockchain started; head block is #1, genesis timestamp is 2018-06-01T12:00:00.000
> info  2018-12-19T05:29:08.598 thread-0  http_plugin.cpp:486           plugin_startup       ] start listening for http requests
> info  2018-12-19T05:29:08.600 thread-0  net_plugin.cpp:3014           plugin_startup       ] starting listener, max clients is 25
> info  2018-12-19T05:29:08.600 thread-0  producer_plugin.cpp:718       plugin_startup       ] producer plugin:  plugin_startup() begin
> info  2018-12-19T05:29:08.601 thread-0  producer_plugin.cpp:752       plugin_startup       ] producer plugin:  plugin_startup() end
> ```

nodeos가 정상적으로 실행은 되었으나 블록을 생성하지 않는 것을 볼 수 있다. 그러나 걱정할 필요는 없다. 이 상황은 당연하기 때문이다. 환경설정 파일을 변경하지 않았기 때문에 정상적으로 실행되지 않은 것이다. 일단 **Control + C를 눌러서 노드를 종료** 시킨다. 

### 2. 환경설정 파일 수정하기

참고로 한번 구동을 해야지만 환경설정 파일이 생성된다. 즉 최초로 설치한 상태에서 위에 1번을 진행하지 않을 경우 환경설정 파일이 없으니 반드시 순서대로 진행하길 바란다. 환경설정 디폴트 저장 위치는 아래와 같다.

Mac OS : `~/Library/Application\ Support/eosio/nodeos/config/`

Linux : `~/.local/share/eosio/nodeos/config/`

위의 경로로 이동하게 되면 [config.ini](../../keywords/n/nodeos-config.ini.md) 라는 파일이 있을 것이다. 이 폴더를 VIM 편집기나 텍스트 에디터 등 자신이 원하는 방법으로 파일을 열어보자. 해당 파일을 열게 되면 정말 많은 옵션이 있을 것이다. 옵션이 너무 많이 때문에 처음부터 **모든 옵션에 대해서 알 필요는 없고** 이중에 노드를 구동하기 위하여 필수적인 요소만  먼저 알아보도록 하자.

환경설정 파일을 열면 아래와 같은 옵션을 찾을 수 있다. 옵션을 아래와 같이 변경하도록 하자.

#### 변경 전

```text
enable-stale-production = false
...
# producer-name = 
...
# plugin = 
```

#### 변경 후

```text
enable-stale-production = true
...
producer-name = eosio
...
plugin = eosio::chain_api_plugin
```

위 3개의 옵션은 이오스를 싱글 노드에서 구현하기 위한 가장 최소한의 옵션이다. 해당 옵션이 어떠한 기능을 가지고 있는지 확인하고 싶다면 [nodeos/config.ini](../../keywords/n/nodeos-config.ini.md) 페이지를 참고하길 바란다. 다시 한번 말하지만 옵션이 많기 때문에 처음부터 모두 알 필요는 없고, 구동하기 위하여 필요한 요소만 파악하고 있으면 된다. 간략히 설명을 하자면 `producer-name` 은 block을 생성하고 sign 하는 계정 이름을 의미하고, `enable-stale-production` 은 내가 블록 생성 권한 여부에 관계없이 블록을 생성할 수 있게 만드는 옵션이다. `plugin` 옵션은 노드를 구성할 때 어떤 플러그인을 동작 시킬 것인가에 대한 옵션이다.

### 3. 다시 nodeos를 실행하기

환경설정 파일을 수정한 이후 다시한번 nodeos를 실행해 보자.

```text
./nodeos
```

#### 성공 화면

> ```text
> info  2018-12-19T06:06:02.445 thread-0  chain_api_plugin.cpp:77       plugin_startup       ] starting chain_api_plugin
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/abi_bin_to_json
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/abi_json_to_bin
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/get_abi
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/get_account
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/get_block
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/get_block_header_state
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/get_code
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/get_code_hash
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/get_currency_balance
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/get_currency_stats
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/get_info
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/get_producer_schedule
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/get_producers
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/get_raw_abi
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/get_raw_code_and_abi
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/get_required_keys
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/get_scheduled_transactions
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/get_table_by_scope
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/get_table_rows
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/get_transaction_id
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/push_block
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/push_transaction
> info  2018-12-19T06:06:02.447 thread-0  http_plugin.cpp:554           add_handler          ] add api url: /v1/chain/push_transactions
> info  2018-12-19T06:06:02.447 thread-0  net_plugin.cpp:3014           plugin_startup       ] starting listener, max clients is 25
> info  2018-12-19T06:06:02.447 thread-0  producer_plugin.cpp:718       plugin_startup       ] producer plugin:  plugin_startup() begin
> info  2018-12-19T06:06:02.447 thread-0  producer_plugin.cpp:740       plugin_startup       ] Launching block production for 1 producers at 2018-12-19T06:06:02.447.
> warn  2018-12-19T06:06:02.454 thread-0  transaction_context.cp:108    deadline_timer       ] Using polled checktime; deadline timer too inaccurate: min:7us max:2541us mean:631us stddev:847us
> info  2018-12-19T06:06:02.461 thread-0  producer_plugin.cpp:752       plugin_startup       ] producer plugin:  plugin_startup() end
> info  2018-12-19T06:06:02.509 thread-0  producer_plugin.cpp:1494      produce_block        ] Produced block 000000028178647e... #2 @ 2018-12-19T06:06:02.500 signed by eosio [trxs: 0, lib: 0, confirmed: 0]
> info  2018-12-19T06:06:03.010 thread-0  producer_plugin.cpp:1494      produce_block        ] Produced block 00000003b4740806... #3 @ 2018-12-19T06:06:03.000 signed by eosio [trxs: 0, lib: 2, confirmed: 0]
> info  2018-12-19T06:06:03.505 thread-0  producer_plugin.cpp:1494      produce_block        ] Produced block 00000004a2aec318... #4 @ 2018-12-19T06:06:03.500 signed by eosio [trxs: 0, lib: 3, confirmed: 0]
> info  2018-12-19T06:06:04.001 thread-0  producer_plugin.cpp:1494      produce_block        ] Produced block 000000053892af10... #5 @ 2018-12-19T06:06:04.000 signed by eosio [trxs: 0, lib: 4, confirmed: 0]
> info  2018-12-19T06:06:04.502 thread-0  producer_plugin.cpp:1494      produce_block        ] Produced block 00000006253861c7... #6 @ 2018-12-19T06:06:04.500 signed by eosio [trxs: 0, lib: 5, confirmed: 0]
> info  2018-12-19T06:06:05.003 thread-0  producer_plugin.cpp:1494      produce_block        ] Produced block 0000000772777174... #7 @ 2018-12-19T06:06:05.000 signed by eosio [trxs: 0, lib: 6, confirmed: 0]
> info  2018-12-19T06:06:05.506 thread-0  producer_plugin.cpp:1494      produce_block        ] Produced block 000000088cb984e1... #8 @ 2018-12-19T06:06:05.500 signed by eosio [trxs: 0, lib: 7, confirmed: 0]
> info  2018-12-19T06:06:06.006 thread-0  producer_plugin.cpp:1494      produce_block        ] Produced block 00000009a1ac89eb... #9 @ 2018-12-19T06:06:06.000 signed by eosio [trxs: 0, lib: 8, confirmed: 0]
> info  2018-12-19T06:06:06.506 thread-0  producer_plugin.cpp:1494      produce_block        ] Produced block 0000000aef7f18be... #10 @ 2018-12-19T06:06:06.500 signed by eosio [trxs: 0, lib: 9, confirmed: 0]
> info  2018-12-19T06:06:07.000 thread-0  producer_plugin.cpp:1494      produce_block        ] Produced block 0000000b57bdeed2... #11 @ 2018-12-19T06:06:07.000 signed by eosio [trxs: 0, lib: 10, confirmed: 0]
> ```

위와 같이 표시가 된다면 정상적으로 노드 구동에 성공한 것이다.

#### 실패한 경우

이전에 노드를 정상적으로 종료하지 않아 정크 데이터가 남아 있는 경우이다. 방법은 간단하다. 기존의 **블록 데이터를 전부 삭제**하고 다시 구동을 하면 된다.

MAC OS

```text
rm -rf ~/Library/Application\ Support/eosio/nodeos/data
```

Linux

```text
rm -rf ~/.local/share/eosio/nodeos/config/data
```

다음과 같이 블록 데이터를 전부 삭제한 이후에 nodeos를 구동하면 정상적으로 구동이 될 것이다. 만약 그래도 구동이 안된다면 환경설정 파일에 **오타**가 났는지 확인하면 된다.

