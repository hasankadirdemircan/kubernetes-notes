<h1 align="center"> K8s Persistence Volumes Nedir? </h1> <br>
<p align="center">
  <a href="https://user-images.githubusercontent.com/34090058/81210705-eec8c900-8fda-11ea-855b-c18724fe6f6c.png">
    <img alt="Techs" title="Techs" src="https://user-images.githubusercontent.com/34090058/81210705-eec8c900-8fda-11ea-855b-c18724fe6f6c.png"width="400">
  </a>
</p>

- Uygulamamız veritabanı etkileşiminde kaydedilen güncellenen veriler fiziksel olarak saklanması gerekir ki bu verilere istediğimiz zaman erişebilelim.
- Tam burada persistence-volumes konusu devreye giriyor.
- Container çökerse(crash) her veri kaybolur.
- docker, dosya sistemi hiyerarşisinin kökenindedir. Birimler diğer birimlere bağlanamaz.
- awsEBS(aws block storage) kullanıldığında, pod öldüğünde veriler korunur.
#### Example Urls.
- [Volumes Docs](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)
- [Volume Example Yaml](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.18/#persistentvolumeclaim-v1-core)

## Overview
<a href="#"><img src="https://user-images.githubusercontent.com/34090058/81210703-ee303280-8fda-11ea-993d-6a59fa773cda.png" width="400"></a>

[ConfigMap](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/)  (Object)) 
- `ConfigMap` nesne bölmelerin tüketmesi için yapılandırma verilerini tutar.

#### EmptyDir
- Podun ömrünü paylaşan boş tmp dizini.
- `emptyDir.medium`  veya `Memory` (tmpfs - RAM destekli dosya sistemi) olabilir. (node restart olduğunda veriler kaybolur.)
- Pod çöktüğünde güvenli container çöküyor.
- Yazabilir. (can write)

#### hostpath
- Genellikle ana bilgisayarın sistem aracılarına veya diğer ayrıcalıklı şeylere veya Docker içlerine (/var/lkib/docker), cAdvisor(QJenny) çalıştıran  veya
- Pod'ların, pod başlatılmadan önce belirli bir `hostPath` olup olmadığını kontrol etmesine izin verir.
- `hostPath.type` - `""` (geriye dönük uyumlu = hiçbir denetim yapılmayacak). - `directorycreate` dizin, dosya oluşturma, dosya,soket,chardevice..)
- Ana `Node`'a yani `minikube ssh` dosyasına girdiğinizde bölmenizde oluşturduğunuz dosyaları göreceksiniz. (Bizim örneğimizde de bu kullanılmaktadır.)
- Pod'a birden fazla volume ekleyebilirsiniz. Başka bir mount içine bile ekleyebilirsiniz. (aynı volume.)
        -
 ## PVC (PersistentVolumeClaim)
 -  pv(persistentVolume) node gibidir. pvc pod gibidir.
 - pod kaynakları ister, pvc boyut/erişim modlarını ister.
 - fiziksel depolamada bir pv oluşturulur.
 - cluster otomatik olarak bir pv'ye bağlı bir pvc oluşturur. (Biz örnekte ikisinide kendimiz oluşturuyoruz.)
 - pvc kullanan bir pod oluşturulur.
 - [https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/)
 - UJenny Access Control [https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/#access-control](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/#access-control)
 - Tek düğümde test ve geliştirme için `hostPath`, production'da kalıcı disk kullanılır. (nfs share, amazon ebs etc..)
 - Bir pvc oluşturduktan sonra, kontrol düzlemi depolama sınıfa sahip, uygun şartlarda bir pv bulursa
 - depolama sınıfı boşsa, herhangi bir depolama sınıfına ait olmadığı anlamına gelir. (boş görünür.)
 - depolama sınıfından bahsedilmezse, standarda ait olacaktır.
 - ReadWriteOnce, birimin tek bir node tarafından okuma yazma olarak mount edilebileceği anlamına gelir.
 - Bir pvc tarafından kullanılan pv'yi silmeye çalışırsanız, bu pvc'yi silene kadar sonlandırma aşamasında olacaktır. ( https://kubernetes.io/docs/concepts/storage/persistent-volumes/#storage-object-in-use-protection )
 - storage class: standart(varsayılan) veya ("" bir tür storage class'tır.)
 - "" ve yeni bir storageclass arasında fark vardır. Boş bir durumda pvc kullanmak için sınıf oluşturmak zorunda değilsiniz.(ancak boş bir depolama sınıfı pv olmalıdır, çünkü boş bir dinamik pv sınıfı oluşturalamaz.)
 - Bir storage class dinamik pv oluşturmaktan sorumludur.
 - Eğer bir standarda bir pvc atamaya çalışırsanız ve bu talebi karşılayan hiçbir pv mevcut değilse, bu pvc standart storageclass'tan bir pv oluşturur.
 - pvc ve pv bire bir eşleme, bu yüzden pv 10 gb kullanıyorsa, pvc 3gb kullanıyor. pvc kapasitesi 10 gb'dır.)
 - Erişim modu pvc ve pv ile eşleşmelidir.(storageClassName)
 - Bir pvc(standart) oluşturursanız, pv yoksa otomatik olarak bir tane oluşturulur ve bu pvc silinirse, bu pv de otomatik olarak silinir. (çünkü varsayılan dinamik policy silinir.)
 - Gereksinimi karşılayabilecek bir pv olsa bile, kubectl tarafından bazı ara pv'nin oluşturulduğunu ve serbest bırakıldığını görebiliriz.
 - Pvc'ler otomatik olarak güncellenir, bu nedenle uygun bir pv oluştulursa bekleyen olanlar bağlanır. (pvc üzerinde bir kontrol döngüsü izler.)
  
## Running and Testing

#### delete all services/deployments/replicasets/pods
```
kubectl aplly -f .
```
#### logs pod
```
kubectl logs -f pod/mongodb-695ddf6d4c-mglps
```
kubectl logs -f `<podName>`

#### listing persistentVolume
```
kubectl get pv
```
#### listing persistentVolumeClaim
```
kubectl get pvc
```
#### and testing mongo pods inside  claimName, mounts path .. 
```
kubectl describe pod/mongodb-65784d9f9d-hh2ck
```
