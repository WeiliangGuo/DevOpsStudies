A **Deployment** in Kubernetes is a higher-level controller that builds upon the basic Kubernetes primitives to manage the lifecycle of applications. It sits above ReplicaSets and Pods in the hierarchy of Kubernetes components. 

- **Pods** are the smallest deployable units in Kubernetes, encapsulating one or more containers.
- **ReplicaSets** ensure a specified number of Pod replicas are running at any given time.
- **Deployments** manage ReplicaSets and provide additional functionality, such as rolling updates, rollbacks, and scaling.

In essence, a Deployment allows you to define the desired state of your application (e.g., the number of replicas, the container image version) and handles the orchestration needed to achieve and maintain that state. This makes Deployments a critical tool for continuous delivery and operational management of containerized applications in Kubernetes.


# Kubernetes Commands for Huggingface Transformers Deployment

* Create a Deployment
```
kubectl create deployment transformers-deployment --image=huggingface/transformers:latest
```
* Explanation: This command creates a new Deployment named `transformers-deployment` using the `huggingface/transformers:latest` Docker image. A Deployment ensures that a specified number of replicas of the application are running at all times.

* Output:
```
deployment.apps/transformers-deployment created
```
---
* Get Deployments
```
kubectl get deployments
```
* Output:
```
NAME                    READY   UP-TO-DATE   AVAILABLE   AGE
transformers-deployment 1/1     1            1           5s
```
---
* Describe a Deployment
```
kubectl describe deployment transformers-deployment
```
* Output:
```
Name:                   transformers-deployment
Namespace:              default
CreationTimestamp:      <timestamp>
Labels:                 app=transformers-deployment
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=transformers-deployment
Replicas:               1 desired | 1 updated | 1 total | 1 available | 0 unavailable
...
Events:
  Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
  Normal  ScalingReplicaSet  5s    deployment-controller  Scaled up replica set transformers-deployment-<pod-id> to 1
```
---
* Update a Deployment
```
kubectl set image deployment/transformers-deployment transformers=huggingface/transformers:4.0.0
```
* Output:
```
deployment.apps/transformers-deployment image updated
```
---
* Scale a Deployment
```
kubectl scale deployment transformers-deployment --replicas=3
```
* Output:
```
deployment.apps/transformers-deployment scaled
```
---
* Delete a Deployment
```
kubectl delete deployment transformers-deployment
```
* Output:
```
deployment.apps "transformers-deployment" deleted
```
---
* Apply a Deployment Configuration
Assuming you have a `deployment.yaml` file with the following content:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: transformers-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: transformers
  template:
    metadata:
      labels:
        app: transformers
    spec:
      containers:
      - name: transformers
        image: huggingface/transformers:latest
        ports:
        - containerPort: 80
```
Apply the configuration:
```
kubectl apply -f deployment.yaml
```
* Output:
```
deployment.apps/transformers-deployment created
```
---
* Get Deployment Status
```
kubectl rollout status deployment/transformers-deployment
```
* Output:
```
deployment "transformers-deployment" successfully rolled out
```
---
* Roll Back a Deployment
```
kubectl rollout undo deployment/transformers-deployment
```
* Purpose: Reverts the Deployment to a previous revision. This is useful when a recent update has caused issues, and you need to return to a previously known good state.
* Output:
```
deployment.apps/transformers-deployment rolled back
```
---
* View Deployment History
```
kubectl rollout history deployment/transformers-deployment
```
* Output:
```
deployment.apps/transformers-deployment
REVISION  CHANGE-CAUSE
1         <none>
2         <none>
```
---
* Pause a Deployment
```
kubectl rollout pause deployment/transformers-deployment
```
* Purpose: any ongoing or future updates to the Deployment will be halted until the rollout is resumed.
* Output:
```
deployment.apps/transformers-deployment paused
```
---
* Resume a Deployment
```
kubectl rollout resume deployment/transformers-deployment
```
* Output:
```
deployment.apps/transformers-deployment resumed
```
