# 패키지 도구로 설치하기

## 0. 설치하기 전

* [EOS 설치하기](./) 페이지에서 지원되는 OS를 미리 확인한다.
* [https://github.com/eosio/eos/releases](https://github.com/eosio/eos/releases) 페이지를 통해 패키지 도구가 지원하는 버전을 확인한다. 

해당 페이지 생성 기준 최신 버전은 [v1.5.1](../../document/release-notes/v1.5.1.md) 이다.

## 1. Mac OS

### Install

```text
brew tap eosio/eosio
brew install eosio
```

### Uninstall

```text
brew remove eosio
```

* EOSIO 설치 후 해당 폴더의 위치는 usr/local/cellar 안에 있습니다. usr 폴더는 MAC에서 사용하는 라이브러리 폴더인데 기본적으로 숨김으로 설정이 되어 있어서 특정 커맨드를 입력하여 진입 가능합니다. Finder에서 \[Command + Shift + G\] 키 입력으로 usr/local/cellar를 입력하여  경로로 이동합니다.

## 2. Ubuntu

### Ubuntu 18.04 Install

```text
wget https://github.com/eosio/eos/releases/download/v1.5.1/eosio_1.5.1-1-ubuntu-18.04_amd64.deb
sudo apt install ./eosio_1.5.1-1-ubuntu-18.04_amd64.deb
```

### Ubuntu 16.04 Install

```text
wget https://github.com/eosio/eos/releases/download/v1.5.1/eosio_1.5.1-1-ubuntu-16.04_amd64.deb
sudo apt install ./eosio_1.5.1-1-ubuntu-16.04_amd64.deb
```

### Unintall

```text
sudo apt remove eosio
```

## 3. **Centos**

### **Install**

```text
wget https://github.com/eosio/eos/releases/download/v1.5.1/eosio-1.5.1-1.el7.x86_64.rpm
sudo yum install ./eosio-1.5.1-1.el7.x86_64.rpm
```

### **Uninstall**

```text
sudo yum remove eosio.cdt
```

## 4. **Fedora**

### Install

```text
wget https://github.com/eosio/eos/releases/download/v1.5.1/eosio-1.5.1-1.fc27.x86_64.rpm
sudo yum install ./eosio-1.5.1-1.fc27.x86_64.rpm
```

### Uninstall

```text
sudo yum remove eosio.cdt
```

