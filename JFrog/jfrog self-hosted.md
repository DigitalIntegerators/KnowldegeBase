## Installation Guide For jfrog self-hosted server on linux



### Download the artifactory 
```
https://jfrog.com/download-jfrog-platform
```
and choose linux
### Download from terminal 
```
wget https://releases.jfrog.io/artifactory/artifactory-pro/org/artifactory/pro/jfrog-artifactory-pro/[RELEASE]/jfrog-artifactory-pro-[RELEASE]-linux.tar.gz --no-certificate-check 
```

### After the download extract the package 
enter the extracted DIR 
using 
```
tar -xvzf <name of the file>
```
then go to the path (jfrog/artifactory/app/bin/)

### Open the terminal and enter the command 
```
./artifactoryctl start
```
![command1](https://github.com/DigitalIntegerators/KnowldegeBase/assets/132379090/c41b3fa6-3b33-4f18-8de1-239e6f76fa5d)

### After the starting run the following command
```
./artifactoryctl check
``` 
![command2](https://github.com/DigitalIntegerators/KnowldegeBase/assets/132379090/66fcf179-5235-4a53-adbc-3e6e831ad19c)


### then the command 
```
ip addr

```
![Command3](https://github.com/DigitalIntegerators/KnowldegeBase/assets/132379090/da3eac1a-7f4a-4397-b943-dac6b741ea5c)


#### Get the ip address <BROADCAST,MULTICAST,UP,LOWER_UP> get the ip and the port is 8081 for example (192.12.1.15:8081)

### In case the firewall is blocking the port run : ```sudo ufw status```
### Then : ```sudo apt install ufw```
### Then : ```sudo ufw allow 8081/tcp```
### Then : ```sudo ufw allow 8082/tcp```
### Last command : ```sudo ufw enable ```
### Then the ip should work and open the UI on the browser
![login](https://github.com/DigitalIntegerators/KnowldegeBase/assets/132379090/352bd8d6-3705-459e-aec7-5d13fec9de25)


```
 Initial username: admin 
         password:password
```
### Get the certificate from
```
https://jfrog.com/start-free 
``` 
then in the second page select self-hosted
#### insert the certificate that was sent via E-mail entered 
#### now the server is up and running 
#### create a repo and start push and pull from docker 



➕Important note ➕

The server will be not secured(http) abd docker push will be pushing on https and this will make an issue of (TLS unrecognized) so to fix this issue you need to include the server domain in the demon.json for the docker and in docker engine demon on docker desktop. Then restart the machine. 
(https://docs.docker.com/registry/insecure/ )

##the login will need to generate token from the jfrog platform from the set me up menu 

Docker commands for
```
docker login 192.168.1.17:8082
```
```
Username: username 
password: token generated OR PASSWORD
```

docker tag image then push it

```
docker tag <imageid> <Domain name>/<Repo name>/<image name>
  ```
```
docker tag <imageid> 192.168.1.17:8082/dockerlocal/hello-world:latest
```
```
docker push 192.168.1.17:8082/dockerlocal/hello-world
```
```
docker pull 192.168.1.17:8082/dockerlocal/hello-world
```


REFERENCE:
### How to upload from the JFrog GUI
``` 
https://jfrog.com/help/r/artifactory-how-to-upload-a-folder-with-its-content-to-artifactory/artifactory-how-to-upload-a-folder-with-its-content-to-artifactory
```
``` 
https://www.youtube.com/watch?v=ry20qKqJzys
```
``` 
https://www.youtube.com/watch?v=qdCVimkd9xQ 
```
