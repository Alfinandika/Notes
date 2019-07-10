#list image
```bash
docker image
```

#Pull Image
```bash
docker pull namakontainer
```

#Remove Image
```bash
docker rmi <IMAGE ID>
docker image rm mongo
```

#Cek daftar kontainer yang running di Host kita
```bash
docker container ls
```

#Cek daftar semua kontainer di Host kita (baik running maupun tidak running)
```bash
docker container ls --all
```

#Create Container
```bash
docker container create --name mongoserver1 mongo
docker container create --name mongoserver2 mongo
docker container create --name mongoserver3 mongo:4.1
```

#Menjalankan Container & Membuka port agar bisa diakses dari luar
27017 : Port internal container
8080 : port yang bisa diakses dari luar
```bash
docker container create --name mongoserver1 -p 8080:27017 mongo:4.1
```

#Remove Container
```bash
docker container rm f8a5f1cee011
```

#Menjalankan Container
```bash
docker container start mongoserver1
docker container start mongoserver2
docker container start mongoserver3
```

#Stop Container
```bash
docker container stop mongoserver1
docker container stop mongoserver1 mongoserver2
```
#Build Image
buat file namanya DockerFile

```bash
docker build --tag app-golang:1.0 .
```

#Push Image ke Docker Registry
kita buat nama image di local kita sama dengan nama image di registry kita

```bash
docker tag local-image:tagname reponame:tagname
docker push reponame:tagname
```
local-image:tagname adalah nama image di local kita
reponame:tagname adalah nama image di docker registry kita

example : 
```bash
docker tag app-golang:1.0 alfinandika/app-golang:1.0
docker push alfinandika/app-golang:1.0
```

sebelum kita push image ke Docker Registry pastikan kita sudah login dahulu, karena jika belum login maka push akan ditolak

```bash
docker login
```

note : Kita tidak akan push semua image yang ada dilocal, kita hanya push sedikit yaitu main.go saja. Image Golang akan memakai yang sudah ada di repository server nya

#Create Container dengan mengset Environment Variable
```bash
docker container create --name java-docker -p 8080:8080 -e NAME=Alfin java-docker:1.0
```
note : NAME adalah nama environment variable

Set Environment Variable lebih dari satu
```bash
docker container create --name java-docker -p 8080:8080 -e NAME=Alfin -e APP=Java -e PASSWORD=rahasia java-docker:1.0
```

#Membuat network pada docker
Saat container container dibuat, maka mereka tidak akan bisa berkomunikasi sat
u sama lain. agar mereka bisa berkomunikasi satu sama lain maka harus dibuat network dulu dan masukan container container ke dalam network tersebut

```bash
docker network create java_network
```

#Memasukan Container ke dalam network yang sudah dibuat

```bash
docker network connect java_network mongo
docker network connect java_network redis
docker network connect java_network java-docker
```

#Mengecek container sudah masuk ke dalam network atau belum

```bash
docker container inspect mongo
docker container inspect redis
docker container inspect java-docker
```

#Integrasi Container Dengan network
```bash
docker container create --name java-docker -p 8080:8080 -e NAME=Docker -e MONGO_HOST=mongo -e REDIS_HOST=redis java-docker:1.0
```
note : environment variable diisi dengan nama container yang lain

#Menjalankan file yml configuration dengan menggunakan docker compose (Create and Start)
```bash
docker-compose up -d 
```

#Menghentikan docker compose (Stop and Remove All Container)
```bash
docker-compose down -d 
```

#Membuat volume
```bash
docker volume create mongo_data
```

#Membuat container yang mana datanya disimpan di volume
```bash
docker container create --name mongo -p 27017:27017 -v mongo_data:/data/db mongo:4-xenial
```