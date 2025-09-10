## 파드 상태확인

```
k get po -A
```

네트워크 CNI 파드가 안보일 때: 
```
kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
```

