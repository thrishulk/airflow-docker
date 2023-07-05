Sample application from docker
1. Clone the repository
   ``` 
    $ git clone https://github.com/dockersamples/example-voting-app.git
    Cloning into 'example-voting-app'...
    remote: Enumerating objects: 860, done.
    remote: Total 860 (delta 0), reused 0 (delta 0), pack-reused 860
    Receiving objects: 100% (860/860), 953.96 KiB | 126.00 KiB/s, done.
    Resolving deltas: 100% (311/311), done.
   ```
2. navigate into the directory
    ```
   cd example-voting-app
   ```
3. run docker-compose in deamon mode
    ```
   $ docker-compose up -d
    Starting redis                       ... done
    Starting db                          ... done
    Starting example-voting-app_result_1 ... done
    Starting example-voting-app_vote_1   ... done
    Starting example-voting-app_worker_1 ... done
   
   $ docker ps
    CONTAINER ID        IMAGE                       COMMAND                  CREATED             STATUS              PORTS                                          NAMES
    1dce286f2978        example-voting-app_worker   "/bin/sh -c 'dotnet …"   7 minutes ago       Up 3 seconds                                                       example-voting-app_worker_1
    39343e27ebf8        example-voting-app_vote     "python app.py"          7 minutes ago       Up 4 seconds        0.0.0.0:5000->80/tcp                           example-voting-app_vote_1
    295f43ebb7e4        example-voting-app_result   "docker-entrypoint.s…"   7 minutes ago       Up 4 seconds        0.0.0.0:5858->5858/tcp, 0.0.0.0:5001->80/tcp   example-voting-app_result_1
    7adf942a3417        postgres:9.4                "docker-entrypoint.s…"   7 minutes ago       Up 4 seconds        5432/tcp                                       db
    c8749c223d96        redis:alpine                "docker-entrypoint.s…"   7 minutes ago       Up 4 seconds        0.0.0.0:32770->6379/tcp                        redis
   ```
4. run command to down all services
    ```
   $ docker-compose down
    Stopping example-voting-app_worker_1 ... done
    Stopping example-voting-app_vote_1   ... done
    Stopping example-voting-app_result_1 ... done
    Stopping db                          ... done
    Stopping redis                       ... done
    Removing example-voting-app_worker_1 ... done
    Removing example-voting-app_vote_1   ... done
    Removing example-voting-app_result_1 ... done
    Removing db                          ... done
    Removing redis                       ... done
    
   
   ```