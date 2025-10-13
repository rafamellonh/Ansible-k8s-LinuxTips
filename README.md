# Ansible-k8s-LinuxTips
Project Cluster Kubernetes
rm -rf /etc/kubernetes/admin.conf /etc/kubernetes/pki/* /root/.kube/config 

TASK [join-workers : Reset and clean Kubernetes worker] ***************************************************************************************************************************************************************************
fatal: [52.170.62.237]: FAILED! => {"changed": true, "failed_when_result": "The conditional check 'reset_worker.rc not in [0]' failed. The error was: error while evaluating conditional (reset_worker.rc not in [0]): 'dict object' has no attribute 'rc'", "msg": "Unsupported parameters for (ansible.legacy.command) module: warn. Supported parameters include: _raw_params, _uses_shell, argv, chdir, creates, executable, expand_argument_vars, removes, stdin, stdin_add_newline, strip_empty_ends."}
