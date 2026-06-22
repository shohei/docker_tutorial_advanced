■5-02: STEP 1 Create a network using the "network create" command
docker network create wordpress000net1



■5-02: STEP 2 Create and start a MySQL container using the "run" command
docker run --name mysql000ex11 -dit --net=wordpress000net1 -e MYSQL_ROOT_PASSWORD=myrootpass -e MYSQL_DATABASE=wordpress000db -e MYSQL_USER=wordpress000kun -e MYSQL_PASSWORD=wkunpass mysql --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci



■5-02: STEP 3 Create and start a WordPress container using the "run" command
docker run --name wordpress000ex12 -dit --net=wordpress000net1 -p 8085:80 -e WORDPRESS_DB_HOST=mysql000ex11 -e WORDPRESS_DB_NAME=wordpress000db -e WORDPRESS_DB_USER=wordpress000kun -e WORDPRESS_DB_PASSWORD=wkunpass wordpress




■5-02: STEP 4 Verify that the containers are running using the "ps" command
docker ps



■5-02: STEP 6 Clean up
docker stop wordpress000ex12
docker stop mysql000ex11
docker rm wordpress000ex12
docker rm mysql000ex11
docker network rm wordpress000net1



■5-03: Answer 1
(Refer to "■5-02: STEP 3 Create and start a WordPress container using the 'run' command")



■5-03: Answer 2
(Refer to "■5-02: STEP 3 Create and start a WordPress container using the 'run' command")



■5-04: Create Redmine and MySQL containers
○ Options, targets, and arguments for the commands used
- Create a network
docker network create redmine000net2

- Create and start a MySQL container
docker run --name mysql000ex13 -dit --net=redmine000net2 -e MYSQL_ROOT_PASSWORD=myrootpass -e MYSQL_DATABASE=redmine000db -e MYSQL_USER=redmine000kun -e MYSQL_PASSWORD=rkunpass mysql --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci

- Create and start a Redmine container
docker run -dit --name redmine000ex14 --network redmine000net2 -p 8086:3000 -e REDMINE_DB_MYSQL=mysql000ex13 -e REDMINE_DB_DATABASE=redmine000db -e REDMINE_DB_USERNAME=redmine000kun -e REDMINE_DB_PASSWORD=rkunpass redmine



■5-04: Create Redmine and MariaDB containers
○ Options, targets, and arguments for the commands used
- Create a network
docker network create redmine000net3


- Create and start a MariaDB container
docker run --name mariadb000ex15 -dit --net=redmine000net3 -e MYSQL_ROOT_PASSWORD=mariarootpass -e MYSQL_DATABASE=redmine000db -e MYSQL_USER=redmine000kun -e MYSQL_PASSWORD=rkunpass mariadb --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci


- Create and start a Redmine container
docker run -dit --name redmine000ex16 --network redmine000net3 -p 8087:3000 -e REDMINE_DB_MYSQL=mariadb000ex15 -e REDMINE_DB_DATABASE=redmine000db -e REDMINE_DB_USERNAME=redmine000kun -e REDMINE_DB_PASSWORD=rkunpass redmine



■5-04: Try the WordPress and MariaDB combination as well
- Create a network
docker network create wordpress000net4

- Create and start a MariaDB container
docker run --name mariadb000ex17 -dit --net=wordpress000net4 -e MYSQL_ROOT_PASSWORD=mariarootpass -e MYSQL_DATABASE=wordpress000db -e MYSQL_USER=wordpress000kun -e MYSQL_PASSWORD=wkunpass mariadb --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci

- Create and start a WordPress container
docker run --name wordpress000ex18 -dit --net=wordpress000net4 -p 8088:80 -e WORDPRESS_DB_HOST=mariadb000ex17 -e WORDPRESS_DB_NAME=wordpress000db -e WORDPRESS_DB_USER=wordpress000kun -e WORDPRESS_DB_PASSWORD=wkunpass wordpress

