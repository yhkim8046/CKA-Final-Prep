# 📅 CKA 시험 준비 종합 플래너 
---
> 하루 3시간 학습 기준 (1h 실습, 1h 문제풀이, 1h 오답정리)
### Day 1 (Cluster & CRI-dockerd)
- [V] CRI-dockerd 설치 및 상태 확인
- [V] 커널 네트워크 설정 (`net.bridge.bridge-nf-call-iptables=1`, `net.ip_forward=1`)
- [V] kubeadm init/upgrade 실습
- [V] etcd 백업 및 복구 1회

### Day 2 (Helm & CRD)
- [V] Helm 설치 및 `helm repo add`, `helm install` 연습
- [V] `helm get values`, `helm upgrade`, `helm rollback` 실습
- [ ] CRD 생성 및 확인

### Day 3 (Gateway API, Ingress, Patch)
- [V] Gateway API 설치 및 HTTPRoute 실습
- [V] Ingress 생성 및 curl 테스트
- [V] `kubectl patch`로 Deployment 이미지 교체 및 replica 수정
- [V]  jsonpath 손에 익도록 연습

### Day 4 (HPA & Troubleshooting)
- [V] HorizontalPodAutoscaler(HPA) 생성 및 부하 테스트
- [ ] kubelet 로그 (`journalctl -u kubelet`) 분석
- [ ] CNI/TLS 문제 트러블슈팅

---

### 개념 연습 (9.9 ~ 9.10)
- [V] HPA, Sidecar pod
- [V] CNI, Ingress, HTTP Route, Gateway
- [V] PV, PVC, Taint
- [ ] TLS, RBAC
- [V] JSONpath
- [V] cluster update, etcd backup/restore 1회 연습
- [ ] PSA, Security Context
- [V] 모의고사 1번 맛보기 

## 모의고사 3번 복습 및 오답 노트 (9.11 ~ 9.16)

- [V] 모의고사 1 3번 복습 및 오답노트 / 부족한 개념정리 (9.11 ~ 9.12) - 7번 정도함
- [ ] 모의고사 2 3번 복습 및 오답노트 / 부족한 개념정리 (9.13 ~ 9.14)
- [ ] 모의고사 3 3번 복습 및 오답노트 / 부족한 개념정리 (9.15 ~ 9.16)

## Killersh 모의고사 (9.18 ~ 21)

- [ ] 모의고사 1회독 및 오답노트 
- [ ] 모의고사 2회독 및 오답노트
- [ ] 모의고사 3회독 및 오답노트

### 💡 추가 메모 (시험 팁)
- 유사 문제에서 주의할 점:  
- 기억해야 할 단축 명령어/옵션:  

---

## 📊 최종 체크리스트 (시험 직전)
- [V] etcd 백업/복구 가능
- [V] kubeadm upgrade 가능
- [V] Helm 설치/실습 가능
- [V] Gateway API & Ingress 생성 가능
- [V] HPA 구성 및 확인 가능
- [V] `kubectl patch` 활용 가능
- [ ] Troubleshooting (kubelet, CNI, TLS 등) 빠르게 해결 가능
- [ ] Killercoda 환경에서 3회 모의고사 완료


