Running Manually
---
1. start db
    ```
   $ docker run -d --env POSTGRES_PASSWORD=mysecretpassword --name db postgres
   ```
2. start word press and link with db
    ```
   $ docker run -d -p 8085:80 --link db:db --name wordpress wordpress
   ```

Using Docker Compose yaml
---
1. create yaml file
    ```
   $ mkdir wordpress
   $ cd wordpress
   $ nano docker-compose.yml
   
   copy the content:
   version: "3"
   services:
      db: 
        image: postgres
        environment:
          - POSTGRES_PASSWORD=mysecretpassword
      wordpress:
        image: wordpress
        ports:
          - "8085:80"
        links:
          - "db"
   
   ```

2. run docker compose up command
    ```
    $ docker-compose up -d 
   ```
3. down the service us docker-compose down
    ```
    $ docker-compose down
    ```
