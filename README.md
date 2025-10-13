# Ansible-k8s-LinuxTips
Project Cluster Kubernetes
rm -rf /etc/kubernetes/admin.conf /etc/kubernetes/pki/* /root/.kube/config 

TASK [install-helm : Install Prometheus] ***************************************************************************************************************************************************************************************
fatal: [52.170.76.185]: FAILED! => {"changed": true, "cmd": "helm install prometheus bitnami/kube-prometheus --namespace monitoring --create-namespace --version 25.7.3 --set alertmanager.persistentVolume.enabled=false,server.persistentVolume.enabled=false\n", "delta": "0:00:02.971241", "end": "2025-10-13 23:04:41.870982", "msg": "non-zero return code", "rc": 1, "start": "2025-10-13 23:04:38.899741", "stderr": "Error: INSTALLATION FAILED: chart \"kube-prometheus\" matching 25.7.3 not found in bitnami index. (try 'helm repo update'): no chart version found for kube-prometheus-25.7.3", "stderr_lines": ["Error: INSTALLATION FAILED: chart \"kube-prometheus\" matching 25.7.3 not found in bitnami index. (try 'helm repo update'): no chart version found for kube-prometheus-25.7.3"], "stdout": "", "stdout_lines": []}
