# Deploying your first application

## 1. Deploying a Kubernetes cluster

### 1.1. Running a local cluster using `kind` (Kubernetes in Docker)

#### 1.1.1. Install `king`
```
go install sigs.k8s.io/kind@v0.17.0
```

#### 1.1.2. Create a cluster with one node
```
kind create cluster
```

#### 1.1.3. Create a multi-node cluster
Firstly you should create a configuration file `[kind-multi-node.yaml](./kind-multi-node.yaml)`
```
kind create cluster --config kind-multi-node.yaml
```

#### 1.1.4. Listing all nodes
```
kind get nodes
```
or
```
docker ps
```

#### 1.1.5. Logging into cluster nodes provisioned by kind
```
docker exec -it kind-control-plane bash
```

Listing containers inside a cluster node provisioned with kind
```
crictl ps
```



## 2. Interacting with Kubernetes

### 2.1. Setting up a short alias for `kubectl`
Add the following line to your `.bashrc` or `.zshrc` file:
```
alias k=kubectl
```

### 2.2. Using `kubectl`
#### 2.2.1. Verifying if the cluster is up and `kubectl` can talk to it
```
kubectl cluster-info
```

#### 2.2.2. Listing cluster nodes
```
kubectl get nodes
```

#### 2.2.3. Retrieving additional information of an object
```
kubectl describe node kind-worker
```


## 3. Running your first application on Kubernetes

### 3.1. Deploying your application
#### 3.1.1. Create deployment
Create deployment object named `kubia`
```
kubectl create deployment kubia --image=alisktl/kubia:1.0
```

#### 3.1.2. Listing deployments
```
kubectl get deployments
```

#### 3.1.3. Listing pods
```
kubectl get pods
```

#### 3.1.4. Detailed information about pods
```
kubectl describe pod
```

### 3.2. Exposing your application to the world


#### 3.2.1. Creating a service
```
kubectl expose deployment kubia --type=LoadBalancer --port 8080
```

#### 3.2.2. Listing services
```
kubectl get services
```

### 3.3. Horizontally scaling the application

#### 3.3.1. Increasing the number of application instances
```
kubectl scale deployment kubia --replicas=3
```

#### Displaying the pods' host node when listing pods
```
kubectl get pods -o wide
```
