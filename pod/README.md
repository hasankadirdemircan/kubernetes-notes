<h1 align="center"> K8s Pod Nedir? </h1> <br>

Konteyner ‘ların çalışma alanı denilebilir. Bir pod içerisinde birden fazla konteyner çalışabilir. Kubernetes tarafında çalışma şekli gereği yeni bir deploy isteği geldiğinde pod’un yeni versiyonu oluşturulur ve çalıştığı görüldüğünde diğer pod versiyonu kapatılır. Dolayısıyla pod içerisinde birden fazla konteyner olduğu durumda diğer uygulamala konteyner’ları etkileneceğinden bir pod içerisinde bir konteyner tavsiye edilir. Pod öldüğünde tekrar geri kalkmaz aynı imajdan onun yerine yeni bir pod ortaya çıkar.
#### Screnshoots
<table>
     <td><a href="#"><img src="https://user-images.githubusercontent.com/34090058/79017973-4b22ff00-7b7b-11ea-9abb-2958f4ad9bb6.png" width="400"></a></td>
    <td><a href="#"><img src="https://user-images.githubusercontent.com/34090058/79017974-4c542c00-7b7b-11ea-9e99-e1f664be82f5.png" width="400"></a></td>
</table>


#### Deploy Kubernetes
```
kubectl apply -f first-pod.yaml
```
#### Listing
```
kubectl get all
```
#### Pod Description
```
kubectl describe pod webapp
```
**NOT:** webapp -> first-pod.yaml  container name && metadata name.


#### to open shell in Pod
```
kubectl -it  exec webapp -- sh
```
#### Test & Ping 
**NOT:** Before to open shell in Pod
```
wget http://localhost:80
```
#### Open Source Code
```
cat index.html
```

