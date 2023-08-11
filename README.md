# KIND
Criando cluster simples para estudos

Primeiro, visite o site que hospeda o KIND, para novidades e atualizações
https://kind.sigs.k8s.io/docs/user/quick-start/

A instalação pode ser seguida no link abaixo:
https://kind.sigs.k8s.io/docs/user/quick-start/#installation

Depois aque o KIND estiver instalado, a configuração do arquivo YAML abaixo, irá criar um cluster com 3 nós, na versão do kubernetes 1.24.

```yaml
# cluster.yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
  image: kindest/node:v1.24.12@sha256:1e12918b8bc3d4253bc08f640a231bb0d3b2c5a9b28aa3f2ca1aee93e1e8db16
- role: worker
  image: kindest/node:v1.24.12@sha256:1e12918b8bc3d4253bc08f640a231bb0d3b2c5a9b28aa3f2ca1aee93e1e8db16
- role: worker
  image: kindest/node:v1.24.12@sha256:1e12918b8bc3d4253bc08f640a231bb0d3b2c5a9b28aa3f2ca1aee93e1e8db16

```
Outras versões de imagens podem ser obtidas no repositório abaixo
https://github.com/kubernetes-sigs/kind/releases

Para subir um cluster com o arquivo criado acima utilize os comandos:
```
kind create cluster --name NOME_DO_CLUSTER --config cluster.yaml
```

Sera criado um control-plane e dois works neste exemplo.

Podemos adicionar um metrics-server no control-plane conforme o comando abaixo via helm:
```
helm repo add metrics-server https://kubernetes-sigs.github.io/metrics-server/
helm repo update
helm upgrade --install --set args={--kubelet-insecure-tls} metrics-server metrics-server/metrics-server --namespace kube-system
```
Bons estudos a todos!
