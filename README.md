# helloPython

### 加入 Python 學習的 trello
https://trello.com/invite/b/e0fqCm7o/fc9a7e6fa416ecc281559781dab2b00b/python-%E5%AD%B8%E7%BF%92%E8%AA%B2%E7%A8%8B


### 本機執行

```
$ git clone https://github.com/jackey525/helloPython
$ cd app
$ pip install -r requirements.txt
$ python main.py
```

### docker 部份

#### ====== Create a Dockerfile in your Python app project ls======

$ vi Dockerfile
```
  FROM python:3.8

  RUN mkdir /app
  WORKDIR /app
  ADD ./app /app/
  RUN pip install -r requirements.txt

  EXPOSE 5000
  CMD ["python", "/app/main.py"]
```
#### ====== 建立 docker image ======
$ docker build -f Dockerfile -t hello-python:latest .

#### ====== 執行 docker ======
$ docker run -p 5000:5000 hello-python

#### 打開瀏覽器
http://localhost:5000


### k8s 部份 （minikube ＋ 本機的 docker images)

$ kubectl apply -f deployment.yaml

$ kubectl get pods

$ minikube service hello-python-service  --url


### k8s 部份(自建 k8s ＋ docker hub)

#### 先上傳 docker image 到 docker hub

```
$ docker login
$ docker tag hello-python jackylin525/hello-python
$ docker push jackylin525/hello-python
```
#### 修改  deployment.yaml
```
  containers:
  - name: hello-python
     image: jackylin525/hello-python
     imagePullPolicy: Always
     ports:
     - containerPort: 5000
```
```
$ kubectl apply -f deployment.yaml

$ kubectl describe svc hello-python-service
```
```
 % kubectl describe svc hello-python-service               
Name:                     hello-python-service
Namespace:                default
Labels:                   <none>
Annotations:              Selector:  app=hello-python
Type:                     LoadBalancer
IP:                       10.43.73.155
Port:                     <unset>  6000/TCP
TargetPort:               5000/TCP
NodePort:                 <unset>  32062/TCP
Endpoints:                10.42.218.12:5000,10.42.35.91:5000,10.42.38.74:5000 + 1 more...
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
```
```
$ curl 192.168.9.180:32062
```
