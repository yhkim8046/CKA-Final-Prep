## etcd Backup & Restore 
### Backup etcd Data
```bash
ETCDCTL_API=3 etcdctl snapshot save /tmp/backup.db \
  --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key
```

### Restore etcd from Backup
```bash
ETCDCTL_API=3 etcdctl snapshot restore /tmp/backup.db --data-dir /var/lib/etcd-backup
```

---

## RBAC (Role-Based Access Control)
### Check User Permissions
```bash
kubectl auth can-i create pod --as=user1
kubectl auth can-i list pods --as=user1
```

### Create a Role & RoleBinding
```bash
kubectl create role pod-reader --verb=get,list --resource=pods --namespace=default
kubectl create rolebinding pod-reader-binding --role=pod-reader --user=user1 --namespace=default
```