#kubectl get list namespaces
kubectl get ns

#kubectl get pod in default namespaces
kubectl get po

#kubectl get pod list in different namespaces
kubectl get po -n kube-system
(kube-dns, etcd-minikube, storage-provisioner, kube-proxy etc.)

#kubectl get all on the kube-system namespace
kubectl get all -n kube-system
(service/kube-dns, service/kubernetes-dashboard, deployment.apps/kube-dns, deployment.apps/kubernetes-dashboard etc.)

#kubectl get all on the kube-public namespace
kubectl get all -n kube-public

#What is the kube-public
Herkesin görebileceği bir yapılandırma haritası oluşturmak için yeni bir kube-public ad alanı sunuyoruz . Bu ad alanı, kural olarak, tüm kullanıcılar tarafından okunabilir (kimliği doğrulanmamış olanlar dahil)

İlk uygulamada kube-public ad alanı (ve küme bilgisi yapılandırma haritası) kubeadm tarafından oluşturulur. Bu, bunların kubeadm ile önyüklenmeyen kümeler için mevcut olmayacağı anlamına gelir. 
#kubectl describe list kube-dns service
kubectl describe svc kube-dns -n kube-system

## running
# kubectll apply yaml
 kubectl apply -f networking-test.yaml

# kubectl list all
kubectl get all

#Accessing MySQL from a Pod
--deprecated 
kubectl exec -it  webapp-86bd4996fc-cscw6 sh
nwew
kubectl exec  webapp-86bd4996fc-cscw6 -- ls

# nameserver ip
kubectl exec  webapp-86bd4996fc-cscw6 -- cat /etc/resolv.conf
# database service ip 
 kubectl exec  webapp-86bd4996fc-cscw6 -- nslookup database

# Because mysql aplhine not mysql client
kubectl exec  webapp-86bd4996fc-cscw6 -- apk update
 kubectl exec  webapp-86bd4996fc-cscw6 -- apk add mysql-client

# exec webapp pod
kubectl exec -it  webapp-86bd4996fc-cscw6 sh
 mysql -h database -uroot -proot testdb

yest its work. webapp pod accessing database pod :)

# Fully Qualified Domain Names(FQDN)
kubectl exec  webapp-86bd4996fc-cscw6 -- nslookup database

kubectl exec  webapp-86bd4996fc-cscw6 -- cat /etc/resolv.conf

FQDN: FQDN (Fully Qualified Domain Name), alan adı sisteminde bir alan adının tamamını nitelemek için kullanılır. Örneğin; ‘secure.hkdemircan.com’ tanımlarken “secure” alt alan adı, “hkdemircan.com” alan adıdır. “secure.hkdemircan.com” ise FQDN olarak belirtilir.






