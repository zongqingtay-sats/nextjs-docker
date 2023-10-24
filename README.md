This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).  
Ready to be built and deployed with Docker.  

## Prerequisites
### Azure VM
Working configuration:  
- Operating system: Linux (ubuntu 20.04) (Ubuntu 20.04.6 LTS)  
- Size: Standard B2s (2 vcpus, 4 GiB memory)  

### Docker
Set up Docker's apt repository
```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
Install ```docker``` and ```docker-compose```
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo apt-get install docker-compose-plugin
```
Login to container image registry (required for pulling and pushing images)
```bash
sudo docker login dnadpscontainerregistry.azurecr.io
```
Links:
- https://docs.docker.com/engine/install/ubuntu/  
- https://docs.docker.com/compose/install/linux/  

## Build and run with ```docker-compose```
Clone this repository
```bash
git clone https://github.com/zongqingtay-sats/nextjs-docker.git
```
Run ```docker-compose```
```bash
sudo docker compose -f docker-compose-build.yml up
```
Check images are built
```bash
[+] Building 61.6s (20/20) FINISHED                              docker:default
```
Check containers are running
```bash
[+] Running 2/0
 ✔ Container nextjs-test-nginx-1   Cre...                                 0.0s
 ✔ Container nextjs-test-nextjs-1  Cr...                                  0.0s
```

## Pull and run with ```docker-compose```
Clone this repository (only ```docker-compose-pull.yml``` is needed)
```bash
git clone https://github.com/zongqingtay-sats/nextjs-docker.git
```
Run ```docker-compose```
```bash
sudo docker compose -f docker-compose-pull.yml up
```
Check images are pulled
```bash
 ✔ nginx 10 layers [⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿]      0B/0B      Pulled                    0.4s
 ✔ nextjs 14 layers [⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿]      0B/0B      Pulled               0.6s
```
Check containers are running
```bash
[+] Running 2/0
 ✔ Container nextjs-test-nginx-1   Cre...                                 0.0s
 ✔ Container nextjs-test-nextjs-1  Cr...                                  0.0s
```

## Commands
List all images
```bash
sudo docker image ls
```
Pull an image
```bash
sudo docker image pull IMAGE_NAME:TAG
```
Build an image
```bash
sudo docker build -t IMAGE_NAME .
```
Push an image
```bash
sudo docker push IMAGE_NAME:TAG
```
Remove an image
```bash
sudo docker rmi IMAGE_NAME_OR_ID
```
List all containers
```bash
sudo docker container ls
```
Run a new container
```bash
sudo docker run -p HOST_PORT:CONTAINER_PORT IMAGE_NAME
```
Stop a container
```bash
sudo docker stop CONTAINER_NAME
```
Kill a container
```bash
sudo docker kill CONTAINER_NAME
```