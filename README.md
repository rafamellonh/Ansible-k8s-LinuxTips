# Ansible-k8s-LinuxTips
Project Cluster Kubernetes


azureuser@instance-1:~$ kubectl get nodes
E1012 15:58:42.565439   20036 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
E1012 15:58:42.565741   20036 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
E1012 15:58:42.567045   20036 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
E1012 15:58:42.567274   20036 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
E1012 15:58:42.568580   20036 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
The connection to the server localhost:8080 was refused - did you specify the right host or port?


fatal: [52.191.69.232]: FAILED! => {"changed": true, "cmd": "kubeadm join  --token=dmrx9k.62wj3ec3ohp32d9u \\\n--discovery-token-ca-cert-hash=sha256:73987dcb40a0644922ea7f0af6e88eac7ea1d1b68731b55279af72c02e6679b1 \\\n52.191.69.215:6443", "delta": "0:05:00.132507", "end": "2025-10-12 23:02:07.342107", "msg": "non-zero return code", "rc": 1, "start": "2025-10-12 22:57:07.209600", "stderr": "error execution phase preflight: couldn't validate the identity of the API Server: failed to request the cluster-info ConfigMap: Get \"https://52.191.69.215:6443/api/v1/namespaces/kube-public/configmaps/cluster-info?timeout=10s\": context deadline exceeded\nTo see the stack trace of this error execute with --v=5 or higher", "stderr_lines": ["error execution phase preflight: couldn't validate the identity of the API Server: failed to request the cluster-info ConfigMap: Get \"https://52.191.69.215:6443/api/v1/namespaces/kube-public/configmaps/cluster-info?timeout=10s\": context deadline exceeded", "To see the stack trace of this error execute with --v=5 or higher"], "stdout": "[preflight] Running pre-flight checks", "stdout_lines": ["[preflight] Running pre-flight checks"]}