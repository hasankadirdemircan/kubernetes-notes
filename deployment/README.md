
<h1 align="center"> K8s Deployment Nedir? </h1> <br>
<p align="center">
  <a href="https://user-images.githubusercontent.com/34090058/80259608-b5b16000-868e-11ea-8e56-bd8f12b3beed.png">
    <img alt="Techs" title="Techs" src="https://user-images.githubusercontent.com/34090058/80259608-b5b16000-868e-11ea-8e56-bd8f12b3beed.png"width="400">
  </a>
</p>

 - Uygulamalarımızı bir cluster üzerinden dağıtabiliriz. Bunun için deployment yapılandırmasına ihtiyacımız vardır.
 - Deployment uygulamamızın instance'larını nasıl oluşturacağımızı ve güncelleyeceğimizi bildirmektedir.
 - Instance'ları Node'lara zamanlamaktadır.
 - Uygulamanın instance'ları oluşturulduktan sonra bir kubernetes **Deployment Controller** bu instance'ları sürekli olarak izler. Bir instance içeren Node down olursa, **Deployment Controller** down olan instance'ı değiştirir. Buna aynı zamanda **self-healing mechanism** denir.

**NOT:** Eğer 2 replicasets çalışıyorsa ve güncelleme yapacaksak, ilk önce 2 tane yeni versiyon pod olarak çalıştırır ve güncelleme başarılı ise eski versiyonlar ile yeri değiştirilerek. Zero time kaybı yaşanmaktadır. Böylelikle erişim hiç gitmemiş olur.
Eğer yeni versiyon container register'dan çekilirken hata çıkarsa(PullImageError..) eski versiyonlar çalışmaya devam edecektir.

#### Deployment Update Süreci

 <a href="#"><img src="https://user-images.githubusercontent.com/34090058/80259619-bb0eaa80-868e-11ea-823c-2fd611d12084.png" width="400"></a>
 
#### Deployment Update Yaml 
```
kubectl apply -f pods.yaml
```
#### Deployment Update Yaml
```
kubectl apply -f services.yaml
```
#### get all Listing (service, deployment, pod, replicaset)
```
kubectl get all
```
#### Delete Replicaset 
```
kubectl delete rs webapp
```
#### Deployment Update 
```
kubectl apply -f pod.yaml
```
#### Rollout Satus 
```
kubectl rollout status webapp
```

#### Rolluot 
```
kubectl rollout status deploy webapp
```
**NOT:** (deploy->deployment)
#### History Rollout
```
kubectl rollout history deploy webapp
```
#### Rollout 
```
kubectl rollout undo deploy webapp
```
