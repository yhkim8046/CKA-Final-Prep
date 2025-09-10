# 자주 나오는 Control Plane Failure 유형

## 1. **etcd 장애**

증상:

  `kubectl get pods` → etcd Pod만 CrashLoopBackOff 또는 NotReady.
  `kubectl` 명령어들이 동작 안 함.
자주 묻는 것:

  etcd Pod의 `command`/`args` 확인 (경로, 데이터 디렉토리, 인증 cert, key 오타).
  `/etc/kubernetes/manifests/etcd.yaml` 수정.
  `etcdctl` 사용해서 health 체크, snapshot 복원.
예시 문제:

   etcd 데이터 디렉토리 권한이 잘못됨 → 고쳐서 etcd 기동.
   snapshot이 주어짐 → 복원 후 클러스터 정상화.

---

 2. kube-apiserver 장애:

증상:

  - `kubectl` 자체가 아예 동작하지 않음.
  - `kubectl get componentstatuses` → apiserver NotReady.
  - Control plane node에서 `docker ps` / `crictl ps` 보면 `kube-apiserver` container가 CrashLoop.
자주 묻는 것:

  `/etc/kubernetes/manifests/kube-apiserver.yaml` 오타 수정 (image tag, cert path, command flag).
  TLS 인증서 만료 여부 확인 (`openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout`).

---

 3. kube-scheduler 장애

 증상:

  - Pod는 생성되지만 Scheduling이 안 됨 → Pending 상태 고착.
  - `kubectl get pod -n kube-system` → scheduler Pod CrashLoop.
자주 묻는 것:

  - `/etc/kubernetes/manifests/kube-scheduler.yaml` 안의 command 오타 (`kube-schedulerr` 같은).
  - config 파일 경로(`/etc/kubernetes/scheduler.conf`) 잘못 지정된 경우 수정.

---

## 4. kube-controller-manager 장애

증상:

  - Deployment → ReplicaSet → Pod 생성이 안 됨.
  - Node 상태 관리 안 됨.
  - kube-controller-manager Pod CrashLoop.
자주 묻는 것:

  - `/etc/kubernetes/manifests/kube-controller-manager.yaml` 파일 확인.
  - 인증서·kubeconfig 경로 문제 수정.

---

## 5. kubelet / static pod 이슈

증상:

  - control plane 컴포넌트 Pod 자체가 생성 안 됨.
  - 노드 NotReady 상태.
자주 묻는 것:

  - `/var/lib/kubelet/config.yaml` 에 오타 있거나, `systemctl status kubelet` 확인.
  - kubelet 서비스 재시작 (`systemctl restart kubelet`).
  - `/etc/kubernetes/manifests` 안의 static pod yaml 잘못된 경우 고침.

---

# 시험에서 자주 나오는 패턴

1. “Pod CrashLoop → yaml 열어서 command 오타 찾기” (가장 자주 나옴)

   예: `kube-scheduler` → `kube-schedulerrrr`
   예: cert 경로 `/etc/kubernetes/pki/apiserver.crt` → `apiserver.crtt`

2. “인증서 만료 / 잘못된 경로”

   특히 apiserver와 etcd.
   `openssl`로 만료일 확인하고, 잘못된 cert path 수정.

3. “etcd snapshot 복원”

   시험에서 거의 반드시 한 번은 등장.
   절차: etcd Pod 중지 → 데이터 디렉토리 지우기 → snapshot 복원 → etcd 재시작.

4. “kubelet 서비스 죽음”

   systemctl로 상태 확인 후 재시작.
   config 파일 수정.
---

반드시 연습해야 할 명령어:

  ```bash
  # 컨트롤 플레인 로그 보기
  kubectl -n kube-system logs <pod>
  crictl ps
  crictl logs <id>

  # kubelet 서비스 상태
  systemctl status kubelet
  journalctl -u kubelet -f

  # etcd health check
  ETCDCTL_API=3 etcdctl --endpoints=https://127.0.0.1:2379 \
    --cacert=/etc/kubernetes/pki/etcd/ca.crt \
    --cert=/etc/kubernetes/pki/etcd/server.crt \
    --key=/etc/kubernetes/pki/etcd/server.key \
    endpoint health
  ```

* 기본 원칙:
  `/etc/kubernetes/manifests` 안을 먼저 확인하고 → systemctl 확인 → cert 경로 확인 → etcd snapshot 복원 연습.
