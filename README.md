# Docker 설치
curl -fsSL https://get.docker.com | sh

# KinD 설치 (Mac OSX - Arm)
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.20.0/kind-darwin-arm64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind

# KinD 클러스터 구성하기

kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
  - role: worker
networking:
  apiServerAddress: "127.0.0.1"
  apiServerPort: 6443
  disableDefaultCNI: false
  kubeProxyMode: "iptables"

## 클러스터 생성 실행
  kind create cluster --config kind.config.yaml --name my-cluster

  kubectl get nodes

#### App 배포
helm install my-postgres bitnami/postgresql -f helm/postgres/postgres-values.yaml --namespace postgres-ns

# postgres
kubectl get secret my-postgres-postgresql -n postgres-ns -o jsonpath="{.data.postgres-password}" | base64 --decode
aPU29VOCsV%                                                                                         
# postgresql - port forwarding# kind
