# grafana-loki-study

Este repositório contém um ambiente configurado para estudar o Grafana e o Loki utilizando Docker, k3d e Helm.

## Pré-requisitos

Antes de começar, certifique-se de ter os seguintes itens instalados no seu sistema:

- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [k3d](https://k3d.io/) (para criar clusters Kubernetes locais)
- [kubectl](https://kubernetes.io/docs/tasks/tools/) (para gerenciar o cluster Kubernetes)
- [Helm](https://helm.sh/) (para gerenciar pacotes no Kubernetes)

## Passos para iniciar o ambiente

### 1. Abra o Docker Desktop
Certifique-se de que o Docker Desktop está em execução antes de continuar.

### 2. Crie o cluster k3d
Execute o seguinte comando para criar um cluster Kubernetes local com o k3d:

```bash
k3d cluster create grafana-loki-cluster --port 8080:80@loadbalancer --agents 2
```

- Este comando cria um cluster chamado `grafana-loki-cluster` com 2 nós de agente e expõe a porta 80 do balanceador de carga na porta 8080 do host.

### 3. Verifique o cluster
Após criar o cluster, verifique se ele está funcionando corretamente:

```bash
kubectl cluster-info
kubectl get nodes
```

## Como subir com Helm o Grafana Loki

### 1. Adicione o repositório Helm do Grafana
Adicione o repositório oficial do Grafana ao Helm:

```bash
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
```

### 2. Crie um namespace para o Grafana e Loki
Crie um namespace no Kubernetes para organizar os recursos:

```bash
kubectl create namespace monitoring
```

### 3. Instale o Loki com o Helm
Use o Helm para instalar o Loki no namespace `monitoring`:

```bash
helm install loki grafana/loki-stack --namespace monitoring
```

### 4. Verifique os pods
Certifique-se de que os pods estão em execução:

```bash
kubectl get pods -n monitoring
```

### 5. Acesse o Grafana
O Grafana será exposto como um serviço no cluster. Para acessá-lo:

1. Liste os serviços para encontrar o Grafana:
   ```bash
   kubectl get svc -n monitoring
   ```

2. Exponha o serviço do Grafana localmente:
   ```bash
   kubectl port-forward svc/loki-grafana 3000:80 -n monitoring
   ```

3. Acesse o Grafana no navegador em [http://localhost:3000](http://localhost:3000).

4. As credenciais padrão são:
   - Usuário: `admin`
   - Senha: `prom-operator`

### 6. Configure o Loki como fonte de dados no Grafana
1. No Grafana, vá para **Configuration > Data Sources**.
2. Adicione uma nova fonte de dados do tipo **Loki**.
3. Configure a URL como `http://loki:3100`.

### 7. Próximos passos
- Crie dashboards no Grafana para visualizar os logs coletados pelo Loki.
- Configure alertas baseados nos logs.
- Explore as configurações do `values.yaml` para ajustar o comportamento do Loki e do Grafana.

Bom estudo!