## TLS

- TLS는 클라이언트와 서버 간의 통신을 암호화 하고 인증하는 프로토콜
- 쿠버네티스에서 API Server, Kubelet, etcd, Controller Manager, Scheduler 등 여러 컴포넌트가 서로 통신할 때 TLS 인증서를 사용

TLS 인증서는 다음과 같은 목적을 지님 
- 기밀성
- 무결성
- 인증 

### TLS가 사용되는 예시 

1. API Server <-> ectd
- ectd는 데이터를 암호화된 채널로만 API Server와 통신함
- /etc/kubernetes/pki/etcd 경로에 관련 인증서 위치

2. API Server <-> Kubelet 
- Kubelet은 API 서버와 연결할 때 TLS 클라이언트 인증서를 사용
- 일반적으로 /var/lib/kubelet/pki/kubelet-client.crt 에 위치

3. API Server <-> Kubectl 사용자
- ~/.kube/config 파일에 들어있는 client-certificate, client-key, ca.crt로 인증

4. Contorller Manager / Scheduler <-> API Server 
- /etc/kubernetes/controller-manager.conf
- /etc/kubernetes/scheduler.conf 같은 kubeconfig 안에 TLS정보가 들어 있음. 

### TLS 관련 주요 파일위치
- 기본 위치: /etc/kubernetes/pki/  
    - ca.crt, ca.key: 클러스터 전체 CA
    - apiserver.crt, apiserver.key: API 서버 인증서 
    - apiserver-kubelet-client.crt, apiserver-kubelet-client.key
    - front-proxy-ca.crt, front-proxy-client.crt
    - etcd/ 디렉토리: etcd용 인증서

### TLS 문제 유형 (CKA)
- ETCD 백업/복구 
- API 서버가 인증서 문제로 기동 실패 
    - /etc/kubernetes/manifests/kube-apiserver.yaml 안에서 cert, key 경로 확인 및 수정
- 사용자 인증 
    - 새 사용자/CSR 생성 -> CA로 서명 -> Kubeconfig 업데이트
    - CSR 관련 문제에서 singerName: Kubernetes.io/kube-apiserver-client가 필요

### 관련 명령어 
- 인증서 만료일 확인:
```
openssl x509 -in /etc/kubernetes/pki/apiserver.crt -noout -text | grep Not
```

- kubeconfig 안 TLS 정보 보기: 
```
kubectl config view --raw
```

