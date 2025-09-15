## Gateway API 

Gateway API는 Ingress의 차세대 대안으로 더 유연하고 확장 가능한 라우팅을 지원

### 구성 요소
1. GatewayClass
- 어떤 Controller가 트래픽을 처리할지 정의 (nginx, istio)

2. Gateway
- 실제 LB/프록시 인스턴스 정의 
- 어떤 Port/Protocol로 listen할지 정의

3. HTTPRoute/TCPRoute/TLSRoute/GRPCRoute
- 실제 라우팅 규칙 정의 
- 예: /foo -> foo-svc , /bar -> /bar-svc
