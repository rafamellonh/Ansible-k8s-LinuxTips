# Ansible‑k8s‑LinuxTips - EN

Automation with **Ansible** to **provision (Azure)** and **install a Kubernetes cluster** on Linux (master + workers), including **Helm** and **monitoring (Prometheus + Grafana via Helm)**. Educational project based on the **LinuxTips** course, organized in reusable roles and playbooks.

## ✨ What this repository does
- **Provisions infrastructure on Azure** (network, public IP, NIC, VM) using `azure.azcollection` (playbook `Cluster-kubernetes/Create-Instances/`).
- **Initializes the cluster** with `kubeadm` on the master node (role `create-cluster`).
- **Automatically joins workers** to the cluster (role `join-workers`).
- **Installs Helm 3** and **deploys Prometheus & Grafana** via charts (role `install-helm`).

> You can use **everything** (provisioning + K8s) or **only the K8s part**, if you already have the VMs.

## 🧱 Prerequisites
- Control machine with **Ansible** and SSH access to the VMs.
- (Optional, to provision) **Azure CLI** authenticated (`az login`) and permissions in the subscription/resource group.
- Required Ansible collections (e.g., `azure.azcollection`).
- Linux on nodes with `sudo` privileges.

## 🚀 How to use (suggested flow)
1. **(Optional) Provision on Azure**
   ```bash
   ansible-playbook Cluster-kubernetes/Create-Instances/main.yml
   ```
   Adjust variables like `resource_group`, `vnet_name`, `subnet_name`, `admin_user`, VM size, etc. in `Cluster-kubernetes/Create-Instances/create/vars/main.yml`.

2. **Install and configure Kubernetes + Helm + monitoring**
   ```bash
   ansible-playbook Cluster-kubernetes/Install_k8s/main.yml
   ```
   This play runs:
   - `create-cluster` on the **k8s_master** group (initializes the cluster with `kubeadm` and exposes token/hash in `k8s_token_holder`)
   - `join-workers` on the **k8s-workers** group (executes `kubeadm join` using the master's token/hash)
   - `install-helm` on the **k8s_master** (installs Helm, adds repositories and deploys **kube-prometheus** and **grafana** in the `monitoring` namespace)

3. **Verify**
   ```bash
   kubectl get nodes -o wide
   kubectl get pods -n kube-system
   kubectl get pods -n monitoring
   ```

## 🗂 Structure (summary)
```
Cluster-kubernetes/
├─ Create-Instances/            # Azure provisioning playbook
│  ├─ create/tasks/{network.yml,instances.yml,...}
│  └─ main.yml
├─ Install_k8s/                 # Main playbook to install and configure K8s
│  ├─ main.yml                  # orchestrates roles
│  └─ roles/
│     ├─ create-cluster/        # kubeadm init, token and CA hash
│     ├─ join-workers/          # kubeadm join on workers
│     └─ install-helm/          # Helm 3, Bitnami/Grafana charts, Prometheus & Grafana
└─ files/, playbooks/           # supporting materials / examples
```

## 🔧 Important variables (examples)
- **Azure/provisioning**: `resource_group`, `vnet_name`, `subnet_name`, `nsg_name`, `size_instances`, `os_image_*`, `admin_user`, SSH keys.
- **Kubernetes**: `k8s_master_node_ip_private`, `k8s_api_secure_port`, `hostvars['k8s_token_holder']` (master token/hash shared).

## 🛡 Notes
- Playbooks include **idempotent checks** at critical points (e.g., Helm and chart installs run only if not already present).
- This repository is intended for **educational/lab** use. For production, evaluate hardening, RBAC, storage, CNI, high availability, backups, observability and security (SAST/DAST/Dependabot/CodeQL).

---

# Ansible‑k8s‑LinuxTips - PT-BR

Automação com **Ansible** para **provisionar (Azure)** e **instalar um cluster Kubernetes** em Linux (master + workers), incluindo **Helm** e **monitoramento (Prometheus + Grafana via Helm)**. Projeto didático baseado no curso **LinuxTips**, estruturado em roles e playbooks reutilizáveis.

## ✨ O que este repositório faz
- **Provisiona infraestrutura no Azure** (rede, IP público, NIC, VM) usando `azure.azcollection` (playbook `Cluster-kubernetes/Create-Instances/`).
- **Inicializa o cluster** com `kubeadm` no nó master (role `create-cluster`).
- **Faz o join automático dos workers** ao cluster (role `join-workers`).
- **Instala o Helm 3** e **deploya Prometheus & Grafana** via charts (role `install-helm`).

> Você pode usar **tudo** (provisionamento + K8s) ou **apenas a parte de K8s**, caso já tenha as VMs prontas.

## 🧱 Pré-requisitos
- Máquina de controle com **Ansible** e acesso SSH às VMs.
- (Opcional, para provisionar) **Azure CLI** autenticado (`az login`) e permissões no subscription/resource group.
- Collections Ansible necessárias (ex.: `azure.azcollection`).
- Linux nos nós com privilégios `sudo`.

## 🚀 Como usar (fluxo sugerido)
1. **(Opcional) Provisionar no Azure**
   ```bash
   ansible-playbook Cluster-kubernetes/Create-Instances/main.yml
   ```
   Ajuste variáveis como `resource_group`, `vnet_name`, `subnet_name`, `admin_user`, tamanho de VM etc. em `Cluster-kubernetes/Create-Instances/create/vars/main.yml`.

2. **Instalar e configurar Kubernetes + Helm + monitoração**
   ```bash
   ansible-playbook Cluster-kubernetes/Install_k8s/main.yml
   ```
   Este play executa:
   - `create-cluster` no grupo **k8s_master** (inicializa o cluster com `kubeadm` e expõe token/hash em `k8s_token_holder`)
   - `join-workers` no grupo **k8s-workers** (executa `kubeadm join` usando token/hash do master)
   - `install-helm` no **k8s_master** (instala Helm, adiciona repositórios e instala **kube-prometheus** e **grafana** no namespace `monitoring`)

3. **Verificar**
   ```bash
   kubectl get nodes -o wide
   kubectl get pods -n kube-system
   kubectl get pods -n monitoring
   ```

## 🗂 Estrutura (resumo)
```
Cluster-kubernetes/
├─ Create-Instances/            # Playbook de provisionamento no Azure
│  ├─ create/tasks/{network.yml,instances.yml,...}
│  └─ main.yml
├─ Install_k8s/                 # Play principal para instalar e configurar K8s
│  ├─ main.yml                  # orquestra as roles
│  └─ roles/
│     ├─ create-cluster/        # kubeadm init, token e CA hash
│     ├─ join-workers/          # kubeadm join nos workers
│     └─ install-helm/          # Helm 3, Bitnami/Grafana charts, Prometheus & Grafana
└─ files/, playbooks/           # materiais de apoio / exemplos
```

## 🔧 Variáveis importantes (exemplos)
- **Azure/provisionamento**: `resource_group`, `vnet_name`, `subnet_name`, `nsg_name`, `size_instances`, `os_image_*`, `admin_user`, chaves SSH.
- **Kubernetes**: `k8s_master_node_ip_private`, `k8s_api_secure_port`, `hostvars['k8s_token_holder']` (token/hash compartilhados do master).

## 🛡 Observações
- Os playbooks têm **checks idempotentes** em pontos críticos (ex.: instalação do Helm e charts só rodam se ainda não instalados).
- Este repositório tem foco **didático/laboratorial**. Para ambientes produtivos, avalie hardening, RBAC, storage, CNI, alta disponibilidade, backups, observabilidade e segurança (SAST/DAST/Dependabot/CodeQL).

