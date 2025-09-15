## Ingress
 
Ingress는 L7(HTTP/HTTPS) 트래픽 라우팅 리소스
Servicve는 L7(포트 기반)까지만 해주지만, Ingress는 도메인/경로 기반 라우팅을 가능하게 함

### 구성 요소 

Ingress Controller
- 트래픽를 처리하는 실제 구현체
- Ingress 리소스를 해석하고 실제 로드밸런서를 구성

Ingress Resource
- 라우팅 규칙 정의 