# Task 1 — Deploy a Standalone Application Using the Default Bridge Network
The goal is to deploy an Nginx web server using Docker’s default bridge network and access it through the VM Public IP address.
1. Pull the required image from docker registry using:
   
```bash
docker pull nginx:alpine
```



2. Run the nginx on the default bridge network using the command
 ```bash
docker run -d \
  --name myweb \
  -p 80:80 \
  nginx:alpine
```
![](Image/dockerpull.png)

3. check the running containers using

```bash
docker ps
```
   
![](Image/alpineimage.png)

4. The container should be accessible via the VM public ip address/port
   
```bash
http://20.90.12.64:80
```
![](Image/nginx.png)
