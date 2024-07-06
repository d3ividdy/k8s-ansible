# K8s Ansible

Criação e Configuração Base de um cluster k8s

## Apply

```sh
# create local files
cp hosts.example hosts
cp vars.example.yml vars.yml

# apply cluster
ansible-playbook site.yml

# local
mkdir -p ~/.kube && cp k8s/files/admin.conf ~/.kube/config

# set labels workers
kubectl label node $(kubectl get nodes | grep "<none>" | awk '{print $1}') node-role.kubernetes.io/worker=true
```

## K8s

Pasta de arquivos ansible para o cluster k8s

- [k8s/containerd](k8s/containerd.yml)
  - [x] instalação dos pre requisitos
  - [x] chave gpg e repositorio docker
  - [x] instalação containerd

- [k8s/all](k8s/all.yml)
  - [x] importação do play containerd.yml
  - [x] desabilitar o swap
  - [x] instalação dos pre requisitos k8s
  - [x] instalação e fixar versão dos pakages k8s
  - [x] habilitar e inicializar o kubelet

- [k8s/master](k8s/master.yml)
  - [x] inicializa o cluster
  - [x] gera o arquivo join.sh
  - [x] gera o arquivo admin.conf
  - [x] aplica o Flannel (pod network)

- [k8s/worker](k8s/worker.yml)
  - [x] copia o arquivo join.sh para os workers
  - [x] executa o arquivo join.sh

- [k8s/post](k8s/post.yml)
  - [ ] definição de labels Master/Workers

- [k8s/firewall]
  - [ ] adicionar a permissão explicita para 0.0.0.0 na porta 22 para continuar com o acesso
  - [ ] abrir portas de acordo com a documentação: https://kubernetes.io/docs/reference/networking/ports-and-protocols/
  - [ ] definir regra padrão para todas as tabelas como negar acesso

## Service

Deployments de aplicações opcionais para o funcionamento do cluster

- [ ] [service/ingress](service/ingress.yml)
- [ ] [service/portainer](service/portainer.yml)
- [ ] [service/nginx-test](service/nginx.test.yml)
