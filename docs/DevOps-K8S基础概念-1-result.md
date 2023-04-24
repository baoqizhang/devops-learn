### 熟悉并掌握pod核心概念及作用
- 编写Kubernetes Pod YAML文件(容器使用官方的Nginx镜像)且副本数为1
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
    - name: nginx
      image: nginx
      ports:
        - containerPort: 80

```
- 为该Pod加上Lables（“app: nginx”和“env: {对应的环境}”）
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
    env: dev
spec:
  containers:
    - name: nginx
      image: nginx
      ports:
        - containerPort: 80
```
- 为该Pod加上存活探针
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
    env: dev
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
    livenessProbe:
      httpGet:
        path: /
        port: 80
      initialDelaySeconds: 15
      periodSeconds: 20
```
- 在集群中运行该Pod至dev、prod namespace
```shell
kubectl create namespace dev
kubectl create namespace prod
kubectl create -f pod.yaml --dry-run=client -o yaml --namespace=dev | kubectl apply -f -
kubectl create -f pod.yaml --dry-run=client -o yaml --namespace=prod | kubectl apply -f -
```
- 按照Pod名称删除
```shell
kc delete pod nginx -n dev
```
- 使用标签选择器删除Pod
```shell
kubectl get pods --show-labels --all-namespaces
kubectl delete pods -l app=nginx -n dev
kubectl delete pods -l app=nginx,env=dev -n dev
```
- 通过删除整个命名空间来删除Pod
```shell
kubectl get pods --all-namespaces
kubectl get ns
kubectl delete namespace dev
```
- 删除命名空间所有的Pod，但保留命名空间
```shell
kubectl get pods --all-namespaces
kubectl get ns
kubectl delete pods --all --namespace=dev
```
### 熟悉并掌握Deployment核心概念及作用
- 改写Kubernetes Pod YAML文件为Kubernetes Deployment YAML文件，且副本数为2
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx-deployment
    env: dev
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx-deployment
      env: dev
  template:
    metadata:
      labels:
        app: nginx-deployment
        env: dev
    spec:
      containers:
        - name: nginx
          image: nginx
          ports:
            - containerPort: 80
          livenessProbe:
            httpGet:
              path: /
              port: 80
            initialDelaySeconds: 15
            periodSeconds: 20
```
- 为该Deployment加上滚动升级策略
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx-deployment
    env: dev
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx-deployment
      env: dev
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1
      maxSurge: 1
  template:
    metadata:
      labels:
        app: nginx-deployment
        env: dev
    spec:
      containers:
        - name: nginx
          image: nginx
          ports:
            - containerPort: 80
          livenessProbe:
            httpGet:
              path: /
              port: 80
            initialDelaySeconds: 15
            periodSeconds: 20
```
- 为该Deployment加上就绪探针
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx-deployment
    env: dev
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx-deployment
      env: dev
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 1
      maxSurge: 1
  template:
    metadata:
      labels:
        app: nginx-deployment
        env: dev
    spec:
      containers:
        - name: nginx
          image: nginx
          ports:
            - containerPort: 80
          livenessProbe:
            httpGet:
              path: /
              port: 80
            initialDelaySeconds: 15
            periodSeconds: 20
          readinessProbe:
            httpGet:
              path: /index.html
              port: 80
            initialDelaySeconds: 5
            periodSeconds: 10
```
- 在集群中运行该Pod至dev namespace
```shell
kubectl create -f deployment.yaml --dry-run=client -o yaml --namespace=dev | kubectl apply -f -
```
- 将Deployment中的Nginx容器升级至Nginx:1.21，并通过命令观察升级过程
```shell
kubectl rollout status deployment/nginx-deployment -n dev
```
- 尝试调整滚动升级策略，再次将Nginx:1.21升级至Nginx:1.22，并通过命令观察升级过程
```yaml
    rollingUpdate:
      maxUnavailable: 0
      maxSurge: 1
```
```shell
kubectl create -f deployment.yaml --dry-run=client -o yaml --namespace=dev | kubectl apply -f -
kubectl rollout status deployment/nginx-deployment -n dev
```
- 尝试将Nginx:1.22回滚到Nginx:1.21，并观察回滚过程
```shell
kubectl rollout undo deployment/nginx-deployment
--
kubectl rollout history deployment/nginx-deployment
kubectl rollout undo deployment/nginx-deployment --to-revision=2
kubectl rollout status deployment/nginx-deployment -n dev
```