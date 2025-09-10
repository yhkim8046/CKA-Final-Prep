## Cluster Upgrade

1. 업그레이드하고자 하는 노드 스케줄링에서 제외하기

```
k cordon <node>
```
```
k drain <node> --ignore-daemonsets
```

2. 매니페스트 파일을 업그레이드 하고자하는 버전으로 수정하기
위치: /etc/apt/sources.list.d/kubernetes.list

3. kubeadm 업그레이드

```
apt update
apt-cache madison kubeadm
apt-get install kubeadm=1.33.0-1.1
kubeadm upgrade plan v1.33.0
kubeadm upgrade apply v1.33.0
```

4. kubelet 업그레이드

```
sudo apt-mark unhold kubelet kubectl && \
sudo apt-get update && sudo apt-get install -y kubelet='1.33.0-1.1' kubectl='1.33.0-1.1' && \
sudo apt-mark hold kubelet kubectl
```

5. 서비스 재시작

```
systemctl daemon-reload
```

### 쿠버네티스 개념정리

drain vs cordon

drain:
- drain 대상 노드에 있던 파드들이 다른 노드로 재스케줄링
- 단, 파드들은 Replicaset, deployment, daemonset 같이 컨트롤러가 관리하는 파드들이어야 함
- 단일 파드들은 재스케줄링 되지 않고 삭제됨
- --ignore-daemonsets 옵션 필수

Cordon:
- 노드를 스케줄링에서 제외
- 원래 있던 파드들은 그대로 있음

drain에서 --ignore-daemonsets 옵션을 사용하는 이유: 
- daemonsets은 반드시 모든 노드에 최소 1개씩 떠야하는 파드(ex: kube-proxy, fluentd, node-exporter, calico-node)를 보장함
- --ignore-daemonsets 옵션을 사용하지 않을 시 무한 삭제/재생성 무한 루프에 빠지게 됨

systemctl restart kubelet
```
