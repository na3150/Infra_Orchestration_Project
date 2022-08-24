## 1. 프로젝트 목적
AWS의 컴퓨팅 서비스인 EC2 인스턴스에 CI/CD를 위한 Jenkins 환경을 구축하고,
AWS의 관리형 쿠버네티스 서비스인 EKS를 이용해 클러스터를 구성하고 오케스트레이션 함으로써 
개발자는 자동화된 빌드 및 테스트 환경을 사용할 수 있다.
<br><br>
## 2. 시스템 아키텍처
![아키텍처](https://raw.githubusercontent.com/shinsohui/Infra_Orchestration_Project/8bfc31f8bf56cd6f63fbdba9c32d79ec8db22997/architecture.svg)
<br><br>
### 시스템 플로우
1. 개발자가 github에 소스 코드를 push한다. 
2. github에 연결된 Jenkins는 github 레포지토리에 commit된 내용을 감지한다.
3. Pipeline을 생성하고 github의 소스 코드를 자동 빌드하게 설정한다.
4. Dockerfile을 참조해 Docker 이미지를 빌드한뒤 push한다.
5. Jenkins에서 manifest를 업데이트해 이미지 tag를 수정한다.
6. ArgoCD에서 이미지 tag의 변경을 감지한다.
7. ArgoCD는 Dockerhub에서 이미지를 pull한다.
8. ArgoCD에서 소스 코드 변경 부분을 반영하여 업데이트하거나 파드를 재생성한다.
<br><br>
## 3. 사용 도구
![사용도구](https://github.com/shinsohui/Infra_Orchestration_Project/blob/main/image/%EC%82%AC%EC%9A%A9%EB%8F%84%EA%B5%AC.PNG?raw=true)
