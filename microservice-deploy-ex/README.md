<h1 align="center"> K8s Microservice Deployment</h1> <br>
<p align="center">
  <a href="https://user-images.githubusercontent.com/34090058/80921510-8631e000-8d7f-11ea-8fe2-00adc999278c.png">
    <img alt="Techs" title="Techs" src="https://user-images.githubusercontent.com/34090058/80921510-8631e000-8d7f-11ea-8fe2-00adc999278c.png"width="600">
  </a>
</p>

 - Microservice olan araba takip sistemini K8s üzerinde deploy etmeyi amaçlamaktadır.
 
#### delete all services/deployments/replicasets/pods
```
kubectl delete -f .
```
####  test (empty services/deployments/replicasets/pods)
```
kubectl get all
```
####  deploy all pods
```
kubectl apply -f workloads.yaml
```
####  deploy all services
```
kubectl apply -f services.yaml
```
#### pod logs
kubectl logs `<podName>`
```
kubectl logs position-simulator-f48b877cb-xhwlz
```
## Screenshots

### Example kubectl get all
<p align="center">
<a href="#"><img src="https://user-images.githubusercontent.com/34090058/80921511-87630d00-8d7f-11ea-9261-7f5cf7453458.png" width="700"></a>
</p>

### Application Screenshot
<p align="center">
<a href="#"><img src="https://user-images.githubusercontent.com/34090058/80921513-87630d00-8d7f-11ea-9495-1c1222679a1f.png" width="700"></a>
</p>
