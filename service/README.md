<h1 align="center"> K8s Service Nedir? </h1> <br>
<p align="center">
  <a href="https://user-images.githubusercontent.com/34090058/79047848-f6868f00-7c21-11ea-9c1c-727c16d6b06e.png">
    <img alt="Techs" title="Techs" src="https://user-images.githubusercontent.com/34090058/79047848-f6868f00-7c21-11ea-9c1c-727c16d6b06e.png"width="400">
  </a>
</p>

 - Pod'lar ölümlüdür. Yaşam döngüleri vardır. Bir node ölürse, o node'da çalışan pod'lar da kaybolur.
 - Replication Controller , bu durumda yeni pod'lar oluşturur (podu kullanılabilir node'larda yeniden zamanlayarak).
 - Pod'ların K8s kümesinde benzersiz IP'si vardır.
 - Front-end, back-end bir pod'un silinip yeniden yaratıldığını umursamayacaktır.(yeni backend sürümü çıkmak gibi.)
 - K8s service, mantıksal bir pod seti ve bunlara erişmek için bir ilke tanımlar. Service yaml kullanılarak tanımlanır.
 - Service tarafından hedeflenen pod'lar kümesi genellikle bir LabelSelector ile belirlenir.
 - Unique IP adsleri bir service ile dış cluster'a maruz kalmaz. ServiceSpec içerisinde bir tür belirtilerek hizmetler farklı şekillerde verilebilir.
Bu hizmlet türleri;
	 - `ClusterIP` (default) cluster'daki bir iç IP'de service sunar. Bu service'e cluster içinden erişilmesini sağlar.
	 - <a href="#"><img src="https://user-images.githubusercontent.com/34090058/79047881-161db780-7c22-11ea-9934-1c7bc87e184d.png" width="400"></a>
	 - `NodePort` NAT kullanılarak cluster'da seçilen her node'un aynı aynı bağlantı noktasında service sunar.  `<NodeIP>:<NodePort` kullanarak bir service cluster dışından erişilebilir hale getirilir. 
	 -<a href="#"><img src="https://user-images.githubusercontent.com/34090058/79047888-1e75f280-7c22-11ea-83d3-fde71cde6ed4.png" width="400"></a>
	 - `LoadBalancer` geçerli bir cloud'da harici bir yük dengeleyici oluşturur (destekleniyorsa). Service için harici bir IP atar. NodePort'un Superset'idir.
	 - `ExternalName` adı olan bir `CNAME` kaydı döndürerek rastgele bir ad  spesifikasyonda `externalName` tarafından belirtilir.)  kullanarak service'i sunar. Proxy kullanılmaz. Bu tür v1.7 veya daha yüksek `kube-dns` gerektirir.
 -  Selector olmadan oluşturulan bir hizmet, karşılık gelen Endpoints nesnesini de oluşturmaz. Bu kullanıcıların bir service'i belirli uç noktarala manuel olarak eşlemelerini sağlar. Selector'in bulunmamasının başka bir olasılığıda kesinlikle `type:ExternalName` kullanmanızdır. 
	 
 #### Services and Labels
 <a href="#"><img src="https://user-images.githubusercontent.com/34090058/79048245-67c74180-7c24-11ea-95fd-add5803afc8f.png" width="400"></a>
 - Service bir dizi pod için trafiği yönlendirir ve uygulamayı etkilemeden k8'lerde ölmesine ve çoğalmasına izin verir.(service'ler pod2ları ortak bir port üzerinden expose eder.) Böylece eğer bir node/port çalışmıyorsa bu alanları dahili olarak yeniden oluşturuyorsa uygulama zarar görmez.
 - Label'lar key-value çiftleridir. Oluşturma sırasında veya daha sonrada eklenebilir.
 - Minikube cluster'ı çalıştırdığımızda default olarak bir service oluşturulur.

#### Update Pod and Service Steps
<table>
     <td><a href="#"><img src="https://user-images.githubusercontent.com/34090058/79047901-2d5ca500-7c22-11ea-822d-2d6de9278523.png" width="400"></a></td>
    <td><a href="#"><img src="https://user-images.githubusercontent.com/34090058/79047907-38afd080-7c22-11ea-9d56-1f92ead47845.png" width="400"></a></td>
    <td><a href="#"><img src="https://user-images.githubusercontent.com/34090058/79047909-39e0fd80-7c22-11ea-9734-cdf45bb496ee.png" width="400"></a></td>
</table>


#### Deploy Kubernetes
```
kubectl apply -f webapp-service.yaml
```
#### List Service and Pods
```
kubectl get all
```
**NOT:** fist-pods.yaml added label..
#### Get Learn Your minikube IP
```
minikube ip
```
#### and Browser Test
```
<minikubeIp>:30080
```
#### image new tag pull dockerHub
Bkz:  pods/first-pods.yaml spec.container.image update

#### Describe Service
```
 kubectl describe service  fleetman-webapp
```
#### Pod and Label Show
```
kubectl get po --show-labels
```
#### Just Specific Release Show
```
 kubectl get po --show-labels -l release=0
```
