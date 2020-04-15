<h1 align="center"> K8s ReplicaSet Nedir? </h1> <br>
<p align="center">
  <a href="https://user-images.githubusercontent.com/34090058/79375383-3373be00-7f61-11ea-9f69-daf6a154f45f.png">
    <img alt="Techs" title="Techs" src="https://user-images.githubusercontent.com/34090058/79375383-3373be00-7f61-11ea-9f69-daf6a154f45f.png"width="400">
  </a>
</p>

 - Bir ReplicaSet, belirli bir zamanda belirli sayıda pod kopyasının çalışmasını sağlar. Ancak, `Deployment` ReplicaSet'i yöneten ve diğer birçok yararlı özellikle birlikte Pod'lara bildirici güncellemeler sağlayan daha üst düzey bir kavramdır. Bu nedenle, özel güncelleme düzenlemesine veya hiç güncelleme gerektirmedikçe doğrudan ReplicaSets kullanmak yerine `Deployment` kullanması önerilmektedir.
   - Bu aslında ReplicaSet nesnelerini asla manipüle etmeniz gerekmeyeceği anlamına gelir: bunun yerine bir `Deployment` kullanın ve uygulamanızı spec bölümünde tanımlayın.

- Kısacası pod'umuzdan kaç tane istediğimizi belirttiğimiz bir özelliktir. Eğer pod'umuz ölürse/crash olursa yedekte başka bir pod ayağa kaldırdıysak (ReplicaSet: 2), böylelikle uygulamamıza gelen istekler diğer canlı olan pod'a yöneleceği için erişim kısıtı olmayacaktır.
- Aynı zamanda scalling olarak geçen bu özellik ile uygulamamıza yoğun erişimler olduğunda yükü pod'lar arasına yayacağı için daha fazla erişim kaldırabilecektir.

#### Deploy Kubernetes of Pod
```
kubectl apply -f pod.yaml
```
#### Deploy Kubernetes of Service
```
kubectl apply -f service.yaml
```
#### List Service and Pods and ReplicaSets
```
kubectl get all
```
## Testing

#### Pod Delete
```
kubectl delete po webapp-release-0-5
```
#### Service Describe
```
kubectl describe svc fleetman-webapp
```
#### Delete all Pod 
```
kubectl delete po --all
```
#### ReplicaSet Describe 
```
kubectl describe rs webapp
```
**NOT:** We deleted it, but pod will form again. (2 pod, beacuse replicaset: 2)

#### and Browser Test
```
<minikubeIp>:30080
```
**NOT:** Zero timeout and %100 accessibility (when you kill one of the two pods)
