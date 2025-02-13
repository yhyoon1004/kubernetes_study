# Vagrant

>1. Vagrant 란?
>2. 사용법


## 1. Vagrant 란?
가상 머신을 쉽게 만들고 관리해주는 도구  
가상머신은 VirtualBox 같은 소프트웨어가 생성하는 데  
Vagrant 생성과정이나 관리를 편리하게 해주는 도구  
코드로 가상 머신을 구성할 수 있다.

## 2. 사용법

---
**기본 용어**
- box : Vagrant 환경구성 묶음
  - `https://portal.cloud.hashicorp.com/vagrant/discover`   
    여기서 provider에 맞게 필요한 박스 정보를 찾아 설치
- provider : 가상화 가능 제공 소프트웨어 (VirtualBox, Hyper-V, Docker)

---
**기본 명령어**
- `vagrant box list` :  현재 다운받은 box 목록 조회
- `vagrant box add 이름` : 해당 이름의 box를 다운로드
  - ex)  `vagrant box add bento/ubuntu-16.04`
- `vagrant box remove 이름` : 해당 이름의 box 삭제
  - ex) `vagrant box remove bento/ubuntu-16.04`
- `vagrant init bento/ubuntu-16.04` : 해당 박스로 vagrant 환경 초기화
- `vagrant up` : 현재 위치한 vagrant 환경을 기준으로 가상 머신 생성
- `vagrant ssh` : 현재 위치에 생성한 가상머신에 ssh 연결
- `vagrant halt` :  가상 머신 중지
- `vagrant reload` : 가상 머신 재시작
- `vagrant destroy` : 가상 머신 삭제
