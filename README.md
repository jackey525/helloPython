# helloPython

# docker 部份
## ====== Create a Dockerfile in your Python app project ls======
$ vi Dockerfile
'''
FROM python:3.8

RUN mkdir /app
WORKDIR /app
ADD ./app /app/
RUN pip install -r requirements.txt

EXPOSE 5000
CMD ["python", "/app/main.py"]
'''
## ====== 建立 docker image ======
$ docker build -f Dockerfile -t hello-python:latest .

## ====== 執行 docker ======
$ docker run -p 5000:5000 hello-python

## 打開瀏覽器
http://localhost:5000


# k8s 部份

