# 데브옵스 정리
>1. 전체 프로세스
>2. 직무 별 구분
>3. 3. DevOps 외 Ops

---

## 1. 전체 프로세스
- 전체 프로세스
![devops_process.png](devops_process.png)
- `Develop` : `로컬PC`에서 `IDE`를 통해 소스코드를 개발  
    그림으로는 `IntelliJ` 환경에 `SpringBoot(Java)` 어플리케이션 개발  
    완성된 소스코드를 컴파일하여 `로컬PC`의 `JDK` 환경에서 실행 및 확인(`IntelliJ`가 다 해줌)
   

- `CICD` : 로컬PC 자원을 `VirtualBox` 를 통해 OS 레벨로 가상화하여  
    `GuestOS` 로 `RockyLinux`를 올린 `cicd 노드`역할의 `가상머신`
  그 위에  `Jenkins` `docker`, `JDK`,`Gradle` 설치  
    (Vargrant 파일을 통해 인프라 코드화되어 있음)  
    - `Jenkins` 아이템 목록 
      1. `Source Build Job` : GitHub에서 개발자가 만든 소스를 받아와 빌드
      2. `Docker Image Build Job` : 빌드한 소스를 도커이미지로 만들어 DockerHub 업로드
      3. `Kubernetes Deploy Job` : DockerHub에 올라간 Image를 배포
  

- `Infra` :  로컬PC 자원을 `VirtualBox` 를 통해 OS 레벨로 가상화하여  
  `GuestOS`로 `RockyLinux`를 올린 `마스터 노드`역할의 `가상머신` 

---
## 2. 직무 별 구분
- `Develop` : 개발자
- `CICD`: 개발자 / 데브옵스 엔지니어
- `Operations` : 운영자 / 총괄

---
## 3. DevOps 외 Ops
- `GitOps` : Git으로 파이프라인구성 및 이슈/협업관리/빌드/테스트/배포 역할
- `DevSecOps` : 빠른 배포/보안 역할 
- `MLOps` : 머신러닝 기반 Ops 데이터분석가와 개발자 사이의 역할
- 기타 : `LLMOps`, `FinOps`, 등등..