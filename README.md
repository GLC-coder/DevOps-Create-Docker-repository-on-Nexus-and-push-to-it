## DevOps-Create-Docker-repository-on-Nexus-and-push-to-it

### Technologies used:

Docker,Java, Nexus, DigitalOcean, Linux

### Project Description:

1- Create Docker hosted repository on Nexus.

2- Create Docker repository role on Nexus.

3- Configure Nexus, DigitalOcean Droplet and Docker to be able to push to Docker repository.

5- Build and Push Docker image to Docker repository on Nexus.

### Instruction

Step 1: Create droplet server on DigitalOcean

Step 2: Install Nexus, start nexus artifact manager and login to Nexus artifact manager by admin
![image](https://github.com/GLC-coder/DevOps-Artifact-Java-Gradle-Nexus-DigitalOcean/blob/master/image/Screenshot%202023-01-27%20at%208.46.21%20pm.png)

Step 3: Create a docker hosted repository on Nexus artifact manager

![Alt text](/image/Screenshot%202023-02-08%20at%209.47.05%20pm.png?raw=true)

Step 4: Create a non-root User and role with least privilege of views docker to interact with the Nexus artifact manager.
![Alt text](/image/Screenshot%202023-02-08%20at%209.50.50%20pm.png?raw=true)

![Alt text](/image/Screenshot%202023-02-08%20at%209.52.46%20pm.png?raw=true)

Step 5: Configure Nexus, DigitalOcean Droplet and Docker to be able to push to Docker repository.

######Configure a docker port for docker login
![Alt text](/image/Screenshot%202023-02-08%20at%209.55.37%20pm.png?raw=true)

![Alt text](/image/Screenshot%202023-02-08%20at%209.57.52%20pm.png?raw=true)

######Update droplet server firewall with docker port: 8083
![Alt text](/image/Screenshot%202023-02-08%20at%2010.00.53%20pm.png?raw=true)
######Add Docker Bearer Token Realm into Realms to authenticate docker interact with Nexus
![Alt text](/image/Screenshot%202023-02-08%20at%2010.03.16%20pm.png?raw=true)
######Configure docker decker engine with nexus ip and docker running port number to allow docker interact with unsecure http request
![Alt text](/image/Screenshot%202023-02-08%20at%2010.08.43%20pm.png?raw=true)
######Docker login

```
docker login 167.99.248.163:8083
```

![Alt text](/image/Screenshot%202023-02-08%20at%2010.13.30%20pm.png?raw=true)

Step 4: Build and Push Docker image to Docker repository on Nexus.
######Build image

```
docker build -t my-image:1.0 .
```

######Re-tag image with docker-hosted domain url and port

```
docker tag my-image:1.0 167.99.248.163:8083/my-image:1.0
```

######Push docker image to Docker-hosted of Nexus

```
docker push 167.99.248.163:8083/my-image:1.0
```

![Alt text](/image/Screenshot%202023-02-08%20at%2010.21.33%20pm.png?raw=true)
