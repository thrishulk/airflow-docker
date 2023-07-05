#### Reference
[run command - docker docs](https://docs.docker.com/engine/reference/commandline/run/)


```
docker run <image>:<tag>

if tag not provided , default used tag is latest
```

we can find the supported information on tags of a image docker hub
#### STDIN
```
-i  interactive
-t terminal
```

#### Port mapping
```
-p <docker host port>:<Application port>
application port wil be mapped to docker host port provided
``` 

#### Volume Mapping
``` 
-v <docker host dir path>:<path inside container>
```

#### docker inspect

provide more information on container

#### logs

```docker logs <container id>```
#### docker attach
docker attach 
``` docker attach <container id> ```