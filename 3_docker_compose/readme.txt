■7-02: STEP 1 Install Docker Compose
- Linux
sudo apt install -y python3 python3-pip
sudo pip3 install docker-compose



■7-03: STEP 2 Run the definition file
* Replace "username" with your PC's login username
- Windows
docker-compose -f C:\Users\username\Documents\com_folder\docker-compose.yml up -d

- Mac
docker-compose -f /Users/username/Documents/com_folder/docker-compose.yml up -d

- Linux
docker-compose -f /home/username/com_folder/docker-compose.yml up -d



■7-03: STEP 4 Stop and remove containers and networks
- Windows
docker-compose -f C:\Users\username\Documents\com_folder\docker-compose.yml down

- Mac
docker-compose -f /Users/username/Documents/com_folder/docker-compose.yml down

- Linux
docker-compose -f /home/username/com_folder/docker-compose.yml down


