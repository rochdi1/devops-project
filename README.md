# devops-project
# Lokales DevOps-Projekt mit Docker, Jenkins, SonarQube & K3d

## Schnellanleitung für Ubuntu

1. **Virtuellen Speicher erhöhen** (Wichtig für SonarQube):
   ```bash
   sudo sysctl -w vm.max_map_count=262144
   ```

2. **Infrastruktur starten**:
   ```bash
   docker compose up -d
   ```

3. **K3d (Kubernetes in Docker) Cluster erstellen**:
   ```bash
   curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | TAG=v5.6.0 bash
   k3d cluster create mycluster --network devops-project_default -p "80:80@loadbalancer"
   ```

4. **Argo CD installieren**:
   ```bash
   kubectl create namespace argocd
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
   ```

5. **Lokales Git initialisieren (im Ordner java-app)**:
   ```bash
   cd java-app
   git init
   git config user.name "DevOps Admin"
   git config user.email "admin@local.dev"
   git add .
   git commit -m "initial commit"
   ```