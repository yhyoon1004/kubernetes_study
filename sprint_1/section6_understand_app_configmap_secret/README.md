# Application 기능으로 이해하기 - Configmap, Secret

> 개요  
> 1.Configmap 확인하기  
> 2.Secret 확인  
> 3.컨테이너 내부 확인
> 4.API 정보 확인
> 5.Configmap 변경
> 6.Secret 변경

---

## 1.Configmap 확인
- 대시보드에서 보기 
  ![img.png](img.png)
  ![img_1.png](img_1.png)
  

- 서버에서 보기  
  ```shell
  // Configmap 확인
  kubectl describe -n anotherclass-123 configmaps api-tester-1231-properties
  kubectl get -n anotherclass-123 configmaps api-tester-1231-properties -o yaml
  kubectl get -n anotherclass-123 configmaps api-tester-1231-properties -o jsonpath='{.data}'
  ```  
  ![img_2.png](img_2.png)
  
---
## 2. Secret 값 확인
- 대시보드에서 보기 (실제로는 base64로 인코딩되었지만 대시보드에서 디코딩해서 보여줌)
  ![img_3.png](img_3.png)
  ![img_4.png](img_4.png)
  

- 서버에서 보기
  ```shell
  // Secret 확인
  kubectl get -n anotherclass-123 secret api-tester-1231-postgresql -o yaml
  kubectl get -n anotherclass-123 secret api-tester-1231-postgresql -o jsonpath='{.data}'
  
  // Secret data에서 postgresql-info가 Key인 Value값만 조회 하기
  kubectl get -n anotherclass-123 secret api-tester-1231-postgresql -o jsonpath='{.data.postgresql-info\.yaml}'
  
  // Secret data에서 postgresql-info가 Key인 Value값을 Base64 디코딩해서 보기
  kubectl get -n anotherclass-123 secret api-tester-1231-postgresql -o jsonpath='{.data.postgresql-info\.yaml}' | base64 -d
  ```
  ![img_5.png](img_5.png)  
  ![img_6.png](img_6.png)

---

## 3. 컨테이너 내부 확인
- 대시보드의 컨테이너 쉘에서 보기
![img_7.png](img_7.png)  

- `env` 명령어로 `환경변수` 출력
  ![img_8.png](img_8.png)  
  

- `secret` 출력
  ```shell
  // Secret 파일 확인
  ls /usr/src/myapp/datasource
  cat /usr/src/myapp/datasource/postgresql-info.yaml
  ```
  ![img_9.png](img_9.png)
  
  ```shell
  // java 실행 인자 확인
  jps -v
  ```
  ![img_10.png](img_10.png)


- kubectl에서 확인하는 법
  ```shell
  // 사용 포맷
  kubectl exec -n <namespace-name> -it <pod-name> -- <command>
  
  kubectl exec -n anotherclass-123 -it api-tester-1231-5c9f87b99c-4bdx6 -- env
  kubectl exec -n anotherclass-123 -it api-tester-1231-5c9f87b99c-4bdx6 -- cat /usr/src/myapp/datasource/postgresql-info.yaml
  kubectl exec -n anotherclass-123 -it api-tester-1231-5c9f87b99c-4bdx6 -- jps -v
  ```
---
  
## 4. API 정보 확인
- 브라우저에서 app에 http 호출로 정보확인  
`http://192.168.56.30:31231/info`  
![img_11.png](img_11.png)  
`http://192.168.56.30:31231/info`  
![img_12.png](img_12.png)

---
## 5. Configmap 변경
- 대시보드에서 접속
![img_13.png](img_13.png)  
  

- `application_role` 을 `ALL`에서 `GET`으로 변경
![img_14.png](img_14.png)
- Pod에 들어가서 환경변수를 보면 기존 값이 그대로 있는 것을 확인 가능  
(환경변수는 Pod 생성때 주입됨, 그러므로 아래와 같이 변경되지 않는게 **`정상`** )
![img_15.png](img_15.png)
- 콘솔에서 직접 변경 (하지만 app 실행시에 초기 환경변수 값으로 들어가서 효과없음)
  ```shell
  export application_role=GET
  ```
  ![img_16.png](img_16.png)
---
## 6. Secret 변경
- 대시보드에서 변경
  - 일반 편집은 인코딩되서 변경이 힘듬
    ![img_17.png](img_17.png)
    ![img_18.png](img_18.png)
  - 시크릿 상세보기를 클릭하여 편집   
    `dev` -> `test`, `dev123` -> `test123`
    ![img_19.png](img_19.png)
    ![img_20.png](img_20.png)
  - `test`로 변경되었는 지 확인하기
    ```shell
    cat /usr/src/myapp/datasource/postgresql-info.yaml
    ```
    ![img_21.png](img_21.png)
    


`환경변수로 주입` or `볼륨으로 연결` 하느냐에 따라 실시간으로 app의 값을 반영할 수 있고 없고에 영향