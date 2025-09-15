## Network Policy

- 쿠버네티스에서 Pod간의 네트워크 통신을 제어하는 리소스 
- 어떤 Pod가 누구와 통신할 수 있는지 (Ingress/Egress)를 정의 
- CNI 플러그인(Calico, Cilium 등)이 NetworkPolicy를 지원해야 동작
- 기본값은 모든 Pod가 서로 통신 가능 -> Networkpolicy 적용시 제한 

