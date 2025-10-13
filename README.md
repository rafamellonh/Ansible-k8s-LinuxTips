# Ansible-k8s-LinuxTips
Project Cluster Kubernetes


azureuser@instance-1:~$ kubectl get nodes
E1012 15:58:42.565439   20036 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
E1012 15:58:42.565741   20036 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
E1012 15:58:42.567045   20036 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
E1012 15:58:42.567274   20036 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
E1012 15:58:42.568580   20036 memcache.go:265] couldn't get current server API group list: Get "http://localhost:8080/api?timeout=32s": dial tcp 127.0.0.1:8080: connect: connection refused
The connection to the server localhost:8080 was refused - did you specify the right host or port?

TASK [join-workers : join node to cluster] *************************************************************************************************************************************************************************************************
fatal: [40.71.191.208]: FAILED! => {"changed": true, "cmd": "kubeadm join 192.168.1.4:6443 \\\n--token 1bg4ef.z4cb8jdd6i8rp5a5 \\\n--discovery-token-ca-cert-hash sha256:skipped, since /etc/kubernetes/pki/ca.crt exists", "delta": "0:00:00.026489", "end": "2025-10-13 02:02:16.567467", "msg": "non-zero return code", "rc": 1, "start": "2025-10-13 02:02:16.540978", "stderr": "accepts at most 1 arg(s), received 4\nTo see the stack trace of this error execute with --v=5 or higher", "stderr_lines": ["accepts at most 1 arg(s), received 4", "To see the stack trace of this error execute with --v=5 or higher"], "stdout": "", "stdout_lines": []}
