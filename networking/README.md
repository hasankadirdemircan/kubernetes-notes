<h1 align="center"> k8s Networking Nedir? </h1> <br>
<p align="center">
  <a href="https://user-images.githubusercontent.com/34090058/80845541-31bd2200-8c12-11ea-8738-2ff872ba3ffe.png">
    <img alt="Techs" title="Techs" src="https://user-images.githubusercontent.com/34090058/80845541-31bd2200-8c12-11ea-8738-2ff872ba3ffe.png"width="600">
  </a>
</p>

 - Uygulamalarımızın tamamını dış dünyaya açmak istemeyiz.
 - Örnek olarak fullstack bir uygulamada front-end dış dünyaya açılmalı backend ve veritabanı dış dünyadan erişilmez olmalır. 
 - Pod'ların oluşturulurken bir ip adresi atanır.
 - Pod'lar güncellendiğinde veya down olduğunda tekrar ayağa kalkarken yeni bir ip adresi atanmaktadır.
 - Front-end back-end ve database birbirlerini uzun süre ip ile erişmesi imkansızdır.
 - Burada işin içerisine namespaces ve kube-dns'ler girmektedir.
 - namespace k8s de objeleri ayırmamıza/gruplamamıza yarar.
 
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

#### List the current namespaces in a cluster 
```
kubectl get ns
```
#### kubectl get pod in default namespaces
```
kubectl get po
```
#### kubectl get pod list in different namespaces
```
kubectl get po -n kube-system
```
(kube-dns, etcd-minikube, storage-provisioner, kube-proxy etc.)

#### kubectl get all on the kube-system namespace
```
kubectl get all -n kube-system
```
(service/kube-dns, service/kubernetes-dashboard, deployment.apps/kube-dns, deployment.apps/kubernetes-dashboard etc.)
#### kubectl get all on the kube-public namespace
```
kubectl get all -n kube-public
```
#### kubectl describe list kube-dns service
```
kubectl describe svc kube-dns -n kube-system
```

### Running and Testing

#### kubectll apply yamls
```
kubectl apply -f pods-test.yaml
kubectl apply -f services-test.yaml
kubectl apply -f networking-test.yaml
```
#### kubectl list all services/replicasets/pods ..
```
kubectl get all
```
### Accessing MySQL from inside a Pod
#### Pod port forwarded
```
`deprecated`
kubectl exec -it  webapp-86bd4996fc-cscw6 sh
`new` kubectl exec <podName> -- <command>
kubectl exec  webapp-86bd4996fc-cscw6 -- ls
```
#### nameserver ip
```
kubectl exec  webapp-86bd4996fc-cscw6 -- cat /etc/resolv.conf
```
#### database service ip 
```
kubectl exec  webapp-86bd4996fc-cscw6 -- nslookup database
```
#### Access MySQL from inside a Pod
**NOT:** Because mysql aplhine not mysql client
```
kubectl exec  webapp-86bd4996fc-cscw6 -- apk update
kubectl exec  webapp-86bd4996fc-cscw6 -- apk add mysql-client
```
#### exec webapp pod
```
kubectl exec -it  webapp-86bd4996fc-cscw6 sh
mysql -h database -uroot -proot testdb
```
**NOT:** yest its work. webapp pod accessing database pod :)
#### Fully Qualified Domain Names(FQDN)
```
kubectl exec  webapp-86bd4996fc-cscw6 -- nslookup database
kubectl exec  webapp-86bd4996fc-cscw6 -- cat /etc/resolv.conf
```
