# K8s Ansible

Criação e Configuração Base de um cluster k8s

## TODO

- [ ] Definição de como os hosts irá ser passados (env?)
- [ ] Arquivo admin.conf para o kubectl
- [ ] Aplicação Manual dos service (com kubectl)
- [x] Ordem de aplicação
  - k8s/all.yml
  - k8s/master.yml
  - k8s/worker.yml
- [ ] Comando unico de execução

## K8s

Pasta de arquivos ansible para o cluster k8s

- [k8s/docker](k8s/docker.yml)
  - [x] instalação dos pre requisitos
  - [x] chave gpg e repositorio
  - [x] instalação docker e containerd

- [k8s/all](k8s/all.yml)
  - [x] importação do play docker.yml
  - [ ] instalação dos pre requisitos k8s
  - [ ] instalação dos pakages k8s
  - [ ] instalação do docker-cni

- [k8s/master](k8s/master.yml)
  - [x] inicializa o cluster
  - [x] gera o arquivo join.sh
  - [x] gera o arquivo adm.conf
  - [x] aplica o Flannel (pod network)

- [k8s/worker](k8s/worker.yml)
  - [ ] copia o arquivo join.sh para os workers
  - [ ] executa o arquivo join.sh

## Service

Deployments de aplicações opcionais para o funcionamento do cluster

- [ ] [service/ingress](service/ingress.yml)
- [ ] [service/portainer](service/portainer.yml)
