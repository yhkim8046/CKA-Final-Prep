k get pv --sort-by=.spec.capacity.storage -o=custom-columns=NAME:.metadata.name,CAPACITY:.spec.capacity.storage > /opt/outputs/pv-and-capacity-sorted.txt


```
controlplane ~ ✖ k config view --kubeconfig=my-kube-config -o json
{
    "kind": "Config",
    "apiVersion": "v1",
    "preferences": {},
    "clusters": [
        {
            "name": "development",
            "cluster": {
                "server": "KUBE_ADDRESS",
                "certificate-authority": "/etc/kubernetes/pki/ca.crt"
            }
        },
        {
            "name": "kubernetes-on-aws",
            "cluster": {
                "server": "KUBE_ADDRESS",
                "certificate-authority": "/etc/kubernetes/pki/ca.crt"
            }
        },
        {
            "name": "production",
            "cluster": {
                "server": "KUBE_ADDRESS",
                "certificate-authority": "/etc/kubernetes/pki/ca.crt"
            }
        },
        {
            "name": "test-cluster-1",
            "cluster": {
                "server": "KUBE_ADDRESS",
                "certificate-authority": "/etc/kubernetes/pki/ca.crt"
            }
        }
    ],
    "users": [
        {
            "name": "aws-user",
            "user": {
                "client-certificate": "/etc/kubernetes/pki/users/aws-user/aws-user.crt",
                "client-key": "/etc/kubernetes/pki/users/aws-user/aws-user.key"
            }
        },
        {
            "name": "dev-user",
            "user": {
                "client-certificate": "/etc/kubernetes/pki/users/dev-user/developer-user.crt",
                "client-key": "/etc/kubernetes/pki/users/dev-user/dev-user.key"
            }
        },
        {
            "name": "test-user",
            "user": {
                "client-certificate": "/etc/kubernetes/pki/users/test-user/test-user.crt",
                "client-key": "/etc/kubernetes/pki/users/test-user/test-user.key"
            }
        }
    ],
    "contexts": [
        {
            "name": "aws-user@kubernetes-on-aws",
            "context": {
                "cluster": "kubernetes-on-aws",
                "user": "aws-user"
            }
        },
        {
            "name": "research",
            "context": {
                "cluster": "test-cluster-1",
                "user": "dev-user"
            }
        },
        {
            "name": "test-user@development",
            "context": {
                "cluster": "development",
                "user": "test-user"
            }
        },
        {
            "name": "test-user@production",
            "context": {
                "cluster": "production",
                "user": "test-user"
            }
        }
    ],
    "current-context": "test-user@development"
}
```

```
kubectl config view --kubeconfig=my-kube-config -o jsonpath="{.contexts[?(@.context.user=='aws-user')].name}" > /opt/outputs/aws-context-name
```

k config view --kubeconfig=my-kube-config -o jsonpath="{.contexts[?(@.contexts.user=='aws-user')].name}"

k config view --kubeconfig=my-config -o jsonpath="{.contexts[?(@.contexts.user=='aws-user')].name}"

k config view --kubeconfig=my-config -o jsonpath="{.contexts[?(@.contexts.user=='aws-user)].name}"