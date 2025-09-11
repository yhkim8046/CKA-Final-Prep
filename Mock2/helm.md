## helm

### 1. 현재 클러스터에 설치된 모든 Helm Release 확인

```bash
helm ls -A
```

* `helm ls` → 릴리스 목록 확인
* `-A` 또는 `--all-namespaces` → 모든 네임스페이스에 배포된 Release 확인

release 이름과 네임스페이스를 먼저 파악해야 함.

### 2. 등록된 Repo 목록 확인

```bash
helm repo ls
```

등록된 Helm 저장소(repository alias) 목록을 출력함.
여기서 `kk-mock1` 같은 repo alias 확인 가능.


### 3. Repo 업데이트

```bash
helm repo update kk-mock1 -n kk-ns
```

`helm repo update <repo-alias>` → 지정한 저장소의 
참고: `-n kk-ns`는 사실 repo update에는 필요 없음 (붙여도 에러는 안 나지만 의미 없음).

---

### 4. 차트 버전 검색

```bash
helm search repo kk-mock1/nginx -l | head -n30
```

`helm search repo <repo-alias/chart>` → repo 안의 차트 목록 검색
`kk-mock1/nginx` → `kk-mock1` repo 안에 있는 `nginx` 차트 의미
`-l` 또는 `--versions` → 사용 가능한 **모든 버전** 출력
`head -n30` → 출력이 너무 많을 수 있으니 앞에서 30줄만 잘라서 확인

여기서 원하는 버전(예: 18.1.15)을 찾을 수 있음.

---

### 5. 차트 업그레이드 (버전 + replicas 변경)

```bash
helm upgrade kk-mock1 kk-mock1/nginx -n kk-ns --version=18.1.15 --set replicaCount=2
```

`helm upgrade <release> <repo/chart>` → 기존 Release를 새 차트 버전/설정으로 업그레이드
`--version=18.1.15` → 차트 버전을 **18.1.15**로 올림
`--set replicaCount=2` → values.yaml에서 replicas=2로 덮어쓰기 조정

---

### 6. 업그레이드 확인

```bash
helm ls -n kk-ns
```

* `-n kk-ns` → 특정 네임스페이스에서 release 목록 확인
* 출력 결과의 **CHART** 컬럼에서 `nginx-18.1.15` 같은 버전 확인


## 정리된 풀이 흐름

1. `helm ls -A` → 어떤 release가 어디 네임스페이스에 설치됐는지 확인
2. `helm repo ls` → repo alias 확인 (kk-mock1 존재 확인)
3. `helm repo update kk-mock1` → repo 최신화
4. `helm search repo kk-mock1/nginx -l` → nginx 차트 최신 버전 확인
5. `helm upgrade kk-mock1 kk-mock1/nginx --version=18.1.15 --set replicaCount=2` → 버전 올리고 replicas 수정
6. `helm ls -n kk-ns` → 최종 확인



