# Heading for Step 1

To start with the scenario, we need to create the docker compose file and its related configuration files first.
In this scenario, we have pre-created the docker compose file `docker-compose.yml`, the SQL initialzation file `setup.sql` under the path`./cfg`.
Now we can copy the following contents to the file respectively, and they will be auto-saved.


`docker-compose.yml`:
<pre class="file" data-target="clipboard">
version: '3.2' 
 
services: 
    mysql-server: 
        container_name: mysql 
        ports: 
            - "13306:3306"    
        volumes:  
            - ./cfg/setup.sql:/docker-entrypoint-initdb.d/setup.sql
        command: mysqld --general_log=1 --log_output='table'
        environment: 
            MYSQL_ROOT_PASSWORD: 12345 
            MYSQL_DATABASE: wordpress 
            MYSQL_USER: wordpress_user 
            MYSQL_PASSWORD: secret 
        image: mysql:5.7 
    
    wordpress: 
        image: wordpress:latest 
        container_name: wordpress 
        ports: 
            - "20080:80" 
        environment: 
            WORDPRESS_DB_HOST: mysql-server:3306 
            WORDPRESS_DB_USER: wordpress_user 
            WORDPRESS_DB_PASSWORD: secret 
        depends_on: 
            - mysql-server 
    grafana:
        image: grafana/grafana
        container_name: grafana
        ports:
          - '3000:3000'
        depends_on:
            - mysql-server 
        environment:
          GF_INSTALL_PLUGINS: percona-percona-app
</pre>

`/cfg/setup.sql`:
<pre class="file" data-target="clipboard">
CREATE USER 'grafana'@'%' IDENTIFIED BY 'grafana';
GRANT ALL PRIVILEGES ON *.* TO 'grafana'@'%' with GRANT OPTION;
GRANT PROXY ON ''@'' TO 'grafana'@'%' WITH GRANT OPTION;

CREATE USER 'insider'@'%' IDENTIFIED BY 'insider';
GRANT ALL PRIVILEGES ON *.* TO 'insider'@'%' with GRANT OPTION;
GRANT PROXY ON ''@'' TO 'insider'@'%' WITH GRANT OPTION;

FLUSH PRIVILEGES;
</pre>


In the docker compose file, there are 3 docker containers created.

1.	`mysql-server`: a mysql service used for storing the any data in the database.
	It maps the 3306 port in container to the host's 13306 port.
	Also, the mysql root password and the mysql account are initialized.
	The general_log is enabled, to keep tracking query logs and pass to grafana.
	A volume is set up to read the SQL initialzation file.

2.	`wordpress`: a wordpress used for hosting the web server.
	It maps the 80 port in container to the host's 20080 port. (We can access the wordpress service and website through port 20080)
	Also, the wordpress db account and connection are initialized.
	
3.	`grafana`: a grafana service used for monitoring the logs and access of mysql server.
	It maps the 3000 port in container to the host's 3000 port. (We can access the grafana service through port 3000)

In the SQL initialzation file, there are 2 accounts with priviledges equal to root account being created.

1.	grafana account: the account used for viewing the statistics in the grafana application.
2.	insider: the insider account which performs the internal attack in future steps.


After editing the above files, we can execute the following command to compose the docker file:
`docker-compose up`{{execute}}

