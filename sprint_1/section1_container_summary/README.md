# 컨테이너 한방 정리
    1. OS 소프트웨어의 흐름
    2. 컨테이너 기술의 흐름



## 1. OS 소프트웨어의 흐름
> [OS 흐름 그림 요약]
> ![OS_img](OS_history.png) 

최초 OS인 UNIX가 있었는데 유료였음  
누가 이 `UNIX`를 기반으로 OS를 설계해서 `Linux`를 만듬,
이 `Linux`는 무료여서 여러 회사에서 사용하게 됨  
이 `Linux` 를 기반으로 여러 배포판이 나오는 데 크게 2가지로 나뉨  
1. 무료 버전인 `Debian` 계열
   - `ubuntu` : `debian`기반 배포판 OS `debian`에 비해 사용자 편의기능이 더 많음, 세계적으로 많이 사용됨
2. 유료 버전인 `RedHat` 계열  
   1.  `fedora` : `RedHat`에소 새로운 기능을 개발하여 적용한 버전, 무료
   2. `RHEL` : RedHatEnterpriseLinux의 약자로, `fedora`에서 개발한게 안정화되어 릴리즈한 버전
   3. `CentOS` : `RHEL`을 복사해서 만든 배포판, 무료
- 2019 RedHat이 IBM에 인수된 후, 
  1. `fedora` :  새기능 개발, 무료 
  2. `CentOS Stream` : `fedora`의 테스트 배포판으로 사용, 무료
  3. `RHEL` : `CentOS Stream`에서 안정화가 되면 `RHEL`로 릴리즈
  4. `Rocky Linux`, `AlmaLinux` : 위의 `RHEL`을 복제한 
 
근데 보통 기업들은 보안과 안정성, 최신기술 등의 이유로 os를 꾸준히 업데이트하는데  
버그나 문제가 생기면 이를 해결해야함, 그러나 큰 기업이 아닌 이상 관리하기 힘듬  

그래서 이를 관리해주는 Redhat 유료 버전으로 많이 사용함.  

---
    요약
    1. 리눅스는 크게 2계열 debian, redhat
    2. 쿠버네티스도 2계열로 지원.
    3. 쿠버네티스 설치시 RockyLinux는 Redhat 계열이다.

---


## 2. 컨테이너 기술의 흐름

> [컨테이너 기술 흐름 요약]
> ![img.png](container_history.png)

### 2-1 Container Orchestration 정리
- `종류` : `kubernetes`, `dockerSwarm`, `nomad` 등이 존재
- `컨테이너 오케스트레이션` : 컨테이너 애플리케이션의 배포, 업데이트, 롤백 및 삭제 과정을 자동화, 다수의 컨테이너를 클러스터에서 조율하며 실행
- `kubernetes` : 아래에서 정리된 컨테이너 기술들을 지원함(`docker`, `container-d`, `cri-o`, `rkt` 등 -> 런타임임, `CRI`) 

### 2-2 Container 정리
- `chroot` : 계정과 파일, 네트워크 환경을 격리 시켜줌
- `cgroup` : 컴퓨터 자원을 격리 시켜줌
- `namespace` : 프로세스 자원을 격리 
- `LXC(LinuXContainer)` :  위의 기술들을 집약한 기술
- `docker` : `LXC`를 기반으로 만들어진 컨테이너 기술  
    - 초기 : 보안이 안좋았음, root권한으로 프로그램을 설치를 하고 실행하게 함
    - 이후 : 이를 보안함, 현재는 rootless 기능을 제공
- `rkt` : 도커의 보안성 문제 없이 대두된 컨테이너 기술, 성능도 더 좋다함 
    - `Rocket` 이라는 컨테이너 사용
    - CoreOS에 대표 런타임
    - `RedHat`이 `cri-o`를 밀고 있어서 입지가 줄어들음

### 2-3 Container OS 정리
- `CoreOS` : 컨테이너 전용 리눅스 OS
- `fedora CoreOS` : CoreOS가 `RedHat`에 인수되면서 바뀜

---
    요약
    
---
