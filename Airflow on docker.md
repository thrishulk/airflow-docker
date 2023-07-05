Run Airflow on Docker
--

### Links:

- [Blog](https://towardsdatascience.com/getting-started-with-airflow-using-docker-cd8b44dbff98)
- [docker hub](https://hub.docker.com/r/puckel/docker-airflow)

### **Steps**
1. Pull docker image from docker hub. Here we did not provide any version so it takes latest by default. 
use tag of required version if needed.
    ```
   $ docker pull puckel/docker-airflow
    Using default tag: latest
    latest: Pulling from puckel/docker-airflow
    bc51dd8edc1b: Pull complete 
    dc4aa7361f66: Pull complete 
    5f346cb9ea74: Pull complete 
    a4f1efa8e0e8: Pull complete 
    7e4812fc693b: Pull complete 
    f46373e205f2: Pull complete 
    3c982a1645fa: Pull complete 
    c39994a04957: Pull complete 
    8eece23a38e7: Pull complete 
    Digest: sha256:e3012994e4e730dccf56878094ff5524bffbe347e5870832dd6f7636eb0292a4
    Status: Downloaded newer image for puckel/docker-airflow:latest
    docker.io/puckel/docker-airflow:latest
    ```
2. Check the image 
    ```
   $ docker images
    REPOSITORY                      TAG                 IMAGE ID            CREATED             SIZE
    puckel/docker-airflow           latest              ce92b0f4d1d5        2 months ago        797MB
   ```
3. Create a local directory to mount to container for sharing files (example dags)
    ```
    $ mkdir -p ~/docker-mount/airflow/dags
   ``` 
4. run a container using image and start a webserver
    ```
    $ docker run -d -p 8080:8080 -v ~/docker-mount/airflow/dags:/usr/local/airflow/dags  puckel/docker-airflow webserver
    77ac692a02c4ca2ab71a65970c0bc16adcb31b5bcf7572bc9d9a950e77a85750
   ``` 
5. check the container
    ```
    $ docker ps
    CONTAINER ID        IMAGE                   COMMAND                  CREATED             STATUS              PORTS                                        NAMES
    77ac692a02c4        puckel/docker-airflow   "/entrypoint.sh webs…"   29 seconds ago      Up 29 seconds       5555/tcp, 8793/tcp, 0.0.0.0:8080->8080/tcp   stupefied_goldstine
   ```
6. Check the airflow web server using mapped port (in this case 8080)
![](../docker/images/airflow_ui_start.png) 
7. copy sample dag file to dags folder in local machine
    ```
   $ cp ~/Desktop/hello_world_dag.py ~/docker-mount/airflow/dags/
    ```
8. Check the content of sample dag (if need, create a sample file copy using the displayed content)
    ```
   cat ~/docker-mount/airflow/dags/hello_world_dag.py 
    """ Hellow World Dag """
    from airflow import DAG
    from airflow.operators.bash_operator import BashOperator
    from airflow.operators.dummy_operator import DummyOperator
    from airflow.utils.dates import days_ago
    
    dag_options = {
        'dag_id': 'hellow_world',
        'default_args': {
            'owner': 'airflow',
            'start_date': days_ago(1),
            'provide_context': True,
            },
        'schedule_interval': None,
        'catchup': False
    }
    
    with DAG(**dag_options) as dag:
        start = DummyOperator(task_id='start')
        hello = BashOperator(task_id='hello_task', bash_command='echo \'Hello \'')
        end = DummyOperator(task_id='end')
    
        start >> hello >> end

   ```
9. Refresh Airflow UI web page. New dag showing in the web page
![](../docker/images/airflow_ui_hello.png) 
10. stop the container
    ```
    $ docker ps
    CONTAINER ID        IMAGE                   COMMAND                  CREATED             STATUS              PORTS                                        NAMES
    77ac692a02c4        puckel/docker-airflow   "/entrypoint.sh webs…"   45 minutes ago      Up 45 minutes       5555/tcp, 8793/tcp, 0.0.0.0:8080->8080/tcp   stupefied_goldstine
    
    $ docker stop 77ac692a02c4
    77ac692a02c4
    
    $ docker ps -a
    CONTAINER ID        IMAGE                   COMMAND                  CREATED             STATUS                          PORTS               NAMES
    77ac692a02c4        puckel/docker-airflow   "/entrypoint.sh webs…"   47 minutes ago      Exited (0) About a minute ago                       stupefied_goldstine

    ```
11. Start the stopped container
    ```
    $ docker start 77ac692a02c4
    77ac692a02c4
    
    $ docker ps
    CONTAINER ID        IMAGE                   COMMAND                  CREATED             STATUS              PORTS                                        NAMES
    77ac692a02c4        puckel/docker-airflow   "/entrypoint.sh webs…"   50 minutes ago      Up 2 minutes        5555/tcp, 8793/tcp, 0.0.0.0:8080->8080/tcp   stupefied_goldstine
    ``` 
   