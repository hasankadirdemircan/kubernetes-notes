<h1 align="center"> K8s Microservice Deployment</h1> <br>
<p align="center">
  <a href="https://user-images.githubusercontent.com/34090058/80921510-8631e000-8d7f-11ea-8fe2-00adc999278c.png">
    <img alt="Techs" title="Techs" src="https://user-images.githubusercontent.com/34090058/80921510-8631e000-8d7f-11ea-8fe2-00adc999278c.png"width="600">
  </a>
</p>

 - Microservice olan araba takip sistemini K8s üzerinde deploy etmeyi amaçlamaktadır.
 
 ### Namespaces
 
 <table>
     <td><a href="#"><img src="https://user-images.githubusercontent.com/34090058/80845550-37b30300-8c12-11ea-98b7-764ff8300edf.png" width="400"></a></td>
    <td><a href="#"><img src="https://user-images.githubusercontent.com/34090058/80845554-3a155d00-8c12-11ea-8ae9-07d26edd3d94.png" width="400"></a></td>
</table>


 - Kubernetes objelerini/resource ayırmamıza/gruplamamıza yarar.
 - Her kubernetes resource yalnızca bir namespace alanına ait olabilir.
 - Cluster kaynaklarını birden çok kullanıcı arasında bölmenin bir yoludur.
 - 3 tane namespace ile başlanılır.
	- `default` Başka bir namespace olmayan objeler için varsayılandır. İlk kurulumda default seçilidir.
	 -  `kube-system` Kubernetes sistemi tarafından oluşturulan objeler için namespace.
	   -  `kube-public` Herkesin görebileceği bir yapılandırma haritası oluşturmak için yeni bir kube-public ad alanı sunuyoruz . Otomatik oluşturulur ve tüm kullanıcılar tarafından okunabilir(kimliği doğrulanmamış olanlar dahil.) Bu namespace, çoğunlukla cluster kullanımı için ayrılmıştır. 
	        - İlk uygulamada kube-public ad alanı (ve küme bilgisi yapılandırma haritası) kubeadm tarafından oluşturulur. Bu, bunların kubeadm ile önyüklenmeyen kümeler için mevcut olmayacağı anlamına gelir.    

### Namespaces and DNS

<p align="center">
<a href="#"><img src="https://user-images.githubusercontent.com/34090058/80845560-3eda1100-8c12-11ea-99de-52786770dd04.png" width="700"></a>
</p>

- Bir service oluşturduğumuzda karşılık gelen bir entry DNS oluşturulur.
- Bi entry DNS `<sevice-name>.<namespace-name>.svc.cluster.local` formundadır.
- Yani yeni bir container yalnızca `<service-name>` kullanılıyorsa bir namespace'elocal olan hizmete çözümlenir.
- Bu aynı yapılandırmayı geliştirme, hazırlama ve development gibi birden çok namespace alanında kullanmak için kullanışlıdır.
- Namespace'lere ulaşmak için etki alanı adını (FQDN) kullanmanız gerekmektedir.
-  `FQDN (Fully Qualified Domain Name)`, alan adı sisteminde bir alan adının tamamını nitelemek için kullanılır. Örneğin; ‘secure.hkdemircan.com’ tanımlarken “secure” alt alan adı, “hkdemircan.com” alan adıdır. “secure.hkdemircan.com” ise FQDN olarak belirtilir.

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
## pod logs
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
