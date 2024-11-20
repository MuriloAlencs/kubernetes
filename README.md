
# Guia de Configuração do Ambiente Kubernetes com Minikube  
Aluno: Murilo de Alencar Silva  
Matéria: Containers e Orquestração  

## Introdução  
Este guia fornece instruções para configurar um ambiente de orquestração de contêineres usando Minikube, Docker Desktop e Kubernetes. Inclui também os passos para implantar e acessar uma aplicação com Frontend, Backend e Banco de Dados.

## 1. Pré-requisitos  
- **Sistema Operacional**: Windows 10 Pro  
- **Ferramentas Necessárias**:
  - WSL (Windows Subsystem for Linux)
  - Docker Desktop
  - Minikube
  - Git
  - kubectl

## 2. Instalação das Ferramentas  

### 2.1 Docker Desktop  
1. Acesse o site oficial do Docker Desktop: [Link para Instalação](https://docs.docker.com/desktop/setup/install/windows-install/).
2. Siga as instruções do instalador.

### 2.2 Minikube e kubectl  
1. Baixe o Minikube no [site oficial](https://minikube.sigs.k8s.io/docs/start/).  
2. Instale usando o arquivo executável.  
3. Inicie o Minikube:  
   ```bash
   minikube start --driver=docker
   ```
4. Instale o kubectl usando o comando:  
   ```bash
   minikube kubectl -- get po -A
   ```

### 2.3 Git  
1. Baixe o Git no [site oficial](https://git-scm.com/downloads).  
2. Siga as instruções do instalador.

## 3. Clonar o Repositório  
1. Clone o repositório:  
   ```bash
   git clone https://github.com/MuriloAlencs/kubernetes.git
   cd kubernetes
   ```

## 4. Aplicação dos Arquivos YAML  
1. Acesse os diretórios clonados e aplique os arquivos YAML:  
   ```bash
   cd ./backend/
   kubectl apply -f .
   cd ../frontend/
   kubectl apply -f .
   cd ../postgres/
   kubectl apply -f .
   ```
2. Verifique os recursos:  
   ```bash
   kubectl get all
   ```

## 5. Acessando a Aplicação  

### 5.1 Usando Port-Forward  
1. Use o comando:  
   ```bash
   kubectl port-forward svc/frontend-service 8080:3000
   ```
2. Acesse: `http://localhost:8080`.

### 5.2 Usando Minikube Service  
1. Use o comando:  
   ```bash
   minikube service frontend-service
   ```

## 6. Solução de Problemas  

### 6.1 Minikube não inicia  
1. Solução:  
   ```bash
   minikube delete
   minikube start --driver=docker
   ```

### 6.2 Porta do serviço inacessível  
1. Verifique a configuração do serviço:  
   ```bash
   kubectl describe svc frontend-service
   ```
