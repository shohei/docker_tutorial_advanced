■6-02: STEP 0 Create an Apache container
docker run --name apa000ex19 -d -p 8089:80 httpd


■6-02: [Preparation] Create the index.html file
(Refer to the index.html in the chapter06 folder)


■6-02: STEP 2 Copy a file from the host to the container using the "cp" command
* Replace "username" with your PC's login username

- Windows
docker cp C:\Users\username\Documents\index.html apa000ex19:/usr/local/apache2/htdocs/

- Mac
docker cp /Users/username/Documents/index.html apa000ex19:/usr/local/apache2/htdocs/

- Linux
docker cp /home/username/index.html apa000ex19:/usr/local/apache2/htdocs/



■6-02: STEP 1 Copy a file from the container to the host using the "cp" command
- Windows
docker cp apa000ex19:/usr/local/apache2/htdocs/index.html C:\Users\username\Documents\

- Mac
docker cp apa000ex19:/usr/local/apache2/htdocs/index.html /Users/username/Documents/

- Linux
docker cp apa000ex19:/usr/local/apache2/htdocs/index.html /home/username/



■6-03: Mount a storage volume STEP 2 Start an Apache container using the "run" command
- Windows
docker run --name apa000ex20 -d -p 8090:80 -v C:\Users\username\Documents\apa_folder:/usr/local/apache2/htdocs httpd


- Mac
docker run --name apa000ex20 -d -p 8090:80 -v /Users/username/Documents/apa_folder:/usr/local/apache2/htdocs httpd

- Linux
docker run --name apa000ex20 -d -p 8090:80 -v /home/username/apa_folder:/usr/local/apache2/htdocs httpd



■6-03: [Steps] <Advanced> Try volume mounting STEP 1 Create a volume to mount
docker volume create apa000vol1



■6-03: STEP 2 Start an Apache container using the "run" command
docker run --name apa000ex21 -d -p 8091:80 -v apa000vol1:/usr/local/apache2/htdocs httpd



■6-03: STEP 3 Display volume details using the "volume inspect" command
- Volume
docker volume inspect apa000vol1

- Container
docker container inspect apa000ex21



■6-03: STEP 4 Clean up
docker volume rm apa000vol1



■6-03: COLUMN Volume backup
- Command based on the above configuration
docker run --rm -v apa000vol1:/source -v C:\Users\username\Documents:/dest busybox tar czvf /dest/backup_apa.tar.gz -C /source .


- Common usage example (restore)
docker run --rm -v apa000vol2:/source -v C:\Users\username\Documents:/dest busybox tar xzvf /dest/backup_apa.tar.gz -C /source



■6-04: STEP 0 Create an Apache container
docker run --name apa000ex22 -d -p 8092:80 httpd




■6-04: STEP 1 Export a container as an image
docker commit apa000ex22 ex22_original1



■6-04: STEP 2 Verify the image was created
docker image ls



■6-04: [Steps] <Advanced> Create an image from a container using a Dockerfile STEP 2 Create a Dockerfile
(Refer to the Dockerfile in the chapter06 folder)


■6-04: STEP 3 Build the image using the "build" command
- Windows
docker build -t ex22_original2 C:\Users\username\Documents\apa_folder\

- Mac
docker build -t ex22_original2 /Users/username/Documents/apa_folder/

- Linux
docker build -t ex22_original2 /home/username/apa_folder/


■6-04: STEP 4 Verify the image was created
docker image ls
