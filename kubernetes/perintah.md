### list node
```bash
kubectl get node
```

### melihat detail node
```bash
kubectl describe node namanode
```

### melihat semua pod
```bash
kubectl get pod

kubectl get pod -o wide
```

### melihat detail pod
```bash
kubectl describe pod namapod
```

### membuat Pod
```bash
kubectl create -f filepod.yaml
```

### mengakses Pod (ngetest doang)
```bash
kubectl port-forward namapod portAkses:portForward

kubectl port-forward namapod 8888:8080

```

### melihat semua pod dengan labels
```bash
kubectl get pod --show-labels
```

### menambah atau mengubah labels di Pod
```bash
kubectl label pod namapod key=value

kubectl label pod namapod key=value --overwrite
```

### mencari Pod dengan labels
```bash
kubectl get pods -l key

kubectl get pods -l key=value

kubectl get pods -l '!key'

kubectl get pods -l key!=value

kubectl get pods -l 'key in (value1, value2)'

kubectl get pods -l 'key notin (value1, value2)'

```

### mencari Pod dengan beberapa labels
```bash
kubectl get pods -l key, key=value

kubectl get pods -l key=value,key2=value

```

### melihat Annotation pada Pod
```bash
kubectl describe pods nginx-with-annotation

```


### menambah Annotation ke Pod
```bash
kubectl annotate pod namapod key=value

kubectl annotate pod namapod key=value --overwrite

```

### melihat Namespace
```bash
kubectl get namespaces

kubectl get namespace

kubectl get ns

```

### melihat Pod di Namespace
```bash
kubectl get pod --namespace namanamespace

kubectl get pod --n namanamespace

```

### membuat Pod di namespace
```bash
kubectl create -f namafile.yaml --namespace namanamespace

```

### menghapus  namespace
```bash
kubectl delete namespace namanamespace

```

### menghapus  Pod
```bash
kubectl delete pod namapod

kubectl delete pod namapod1 namapod2 namapod3

```

### menghapus Pod menggunakan label
```bash
kubectl delete pod -l key=value

```

### menghapus semua Pod di NameSpace
```bash
kubectl delete pod --all --namespace namanamespace

```

### melihat Detail Probe
```bash
kubectl describe pods podname
```
### Liveness, Readiness, Startup Probe
- Liveness probe untuk mengecek kapan perlu merestart probe. misal saat liveness probe pada Pod tidak merespons kubelet akan secara otomatis me-restart port
- Readiness probe utuk mengecek apakah pod siap menerima traffic.
- Startup probe untuk mengecek apakah pod sudah berjalan, jika belum berjalan, maka kubelet tidak akan melakukan pengecekan liveness dan readiness
- Startup Pod cocok untuk Pod yang membutuhkan proses startup lama, ini dapat digunakan untuk memastikan Pod tidak mati oleh kubelet sebelum selesai berjalan dengan sempurna 

### Konfigurasi Probe
- InitialDelaySeconds : waktu setelah container jalan dan dilakukan pengecekan, default nya 0
- periodSeconds : seberapa sering pengecekan dilakukan, defaulnya 10
- timeoutSeconds : waktu timeout ketika pengecekan gagal, default 1
- successThreshold : minimum dianggap sukses setelah berstatus failure, default 1
- failureThreshold : minimum dianggap gagal, default 3

### membuat Replication Controller
```bash
kubectl create -f nginc-rc.yaml
```

### melihat Replication Controller
```bash
kubectl get replicationcontrollers

kubectl get replicationcontroller

kubectl get rc
```

### Menghapus Replication Controller
```bash
kubectl delete rc namarc

kubectl delete rc namarc --cascade=false
```