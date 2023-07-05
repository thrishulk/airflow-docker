1  while [ ! -f /tmp/wait-script.sh ]; do   sleep .2; done
2  chmod 755 /tmp/wait-script.sh; /tmp/wait-script.sh
3  docker images
4  docker images | wc -l
5  docker images | ubuntu
6  docker images | grep 'ubuntu'
7  docker images
8  ls webapp-color/
9  cat webapp-color/Docker
10  cat webapp-color/Dockerfile
11  ls
12  cd webapp-color/
13  docker build . -t webapp-color
14  docker images
15  docker run -d -it -p 8080:8282 webapp-color
16  docker run -d -it -p 8282:8080 webapp-color
17  docker inspect 3a73af5cc3ed4ae5784b01fd4f93b8ff56a6ea5c6c1bdab9bc00d743ab14d896
18  docker images
19  docker inspect python
20  docker inspect python:3.6
21  docker ps
22  docker exec 3a73af5cc3ed cat /etc/*release*
23  docker images
24  docker pull python:3.6-slim
25  docker images
26  docker pull python:3.6-slim-stretch
27  docker images
28  ls
29  nano Dockerfile
30  cat Dockerfile
31  docker run -d -it -p 8282:8080 webapp-color:lite
32  docker build . -t webapp-color:lite
33  docker images
34  nano Dockerfile
35  docker build . -t webapp-color:lite
36  docker images
37  docker rmi 99db6c93eea5
38  docker images
39  docker run -d -it -p 8383:8080 webapp-color:lite
40  ls
41  cat app.py
42  ls
43  cat Dockerfile
44  cat requirements.txt
45  cat templates/
46  cd templates/
47  ls
48  cat hello.html
49  history