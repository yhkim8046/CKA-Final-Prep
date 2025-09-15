## RBAC
- 쿠버네티스의 권한 관리 방식
- API 리소스에 대한 접근을 제어하는 메커니즘

### 주요 리소스 
1. Role / CluterRole
- Role: 네임스페이스 단위 권한 부여
- ClusterRole: 클러스터 전체 단위 권한 부여 (네임스페이스 독립적)

2. RoleBinding / ClusterRoleBinding
- RoleBinding: 특정 네임스페이스에서 Role을 User/Group/ServiceAccount에 연결
- ClusterRoleBinding: ClusterRole을 클러스터 전체에서 연결 

### 동작 흐름
- Subject (User, Group, Service Account)가 요청
- API Server는 해당 요청의 verb(get,list,create 등), resource(pods, secrets)등, namespace를 확인 
- RBAC 규칙과 매칭 -> 허용 or 거부

### Verbs
- get, list, watch -> 조회 
- create, update, patch, delete -> 변경 계열 
- * -> 모든 verb허용

### 명령어 

권한 확인: 
```
kubectl auth can-i create pods --as john -n dev
```

ServiceAccount 생성: 
```
kubectl create serviceaccount my-sa -n dev
```

Role/ClusterRole

- 네임스페이스에 Role 생성:
```
kubectl create role pod-reader \
--verb=get --verb=list --verb=watch \
--resource-pods -n dev
```

- 클러스터 전체에 ClusterRole 생성
```
kubectl create clusterrole secret-reader \
--verb=get,list \
--resource=secrets
```

RoleBinding / ClusterRoleBinding

- RoleBinding (Role <-> User)
```
kubectl create rolebinding read-pods-binding \
--role=pod-reader\
--user=john \ 
-n dev
```

- ClusterRoleBinding (ClusterRole <-> User)
```
kubectl create clusterrolebinding read-secrets-binding \
--clusterrole=secret-reader\
--user=<user>
```