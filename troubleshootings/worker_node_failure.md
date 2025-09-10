```
k get nodes
```

```
service kubelet status
```

```
journalctl -u kubelet -f
```

/etc/kubenetes/kubelet.conf -> systemctl restart kubelet 

/var/lib/kubelet/config.yaml

1. 노드 상태 확인
2. kubelet 서비스 확인
   ```
   service kubelet status
   ```
3. kubelet 로그 확인
   ```
   journalctl -u kubelet -f
   ```
4. 디버깅

주요 파일 위치: 
/etc/kubernetes/kubelet.conf
/var/lib/kubelet/config.yaml 

kubelet.conf 파일 변경후에 재시작 하기 
```
systemctl restart kubelet
```
