# docker-nginx-containers-network

Containers Communication In A Network
-------------------------------------
Two containers can communicate with each other when they are in same network. Below are the steps to achieve the communication between containers in a network.

1. Create and View network.
2. Create nginx image.
3. Run the image created in step 2 as container mynginx1 with user defined network created in step 1.
   * Verify that container is running. 
4. Run the image created in step 2 as container mynginx2 with user defined network created in step 1.
    * Verify that container is running. 
5. Access each container using curl.
6. Go into the container mynginx1. Ping to the mynginx2. 
7. Go into the container mynginx2. Ping to the mynginx1.
8. Remove resources.
    * Stop the both of the containers.
    * Remove the images.
    * Remove the network.
    
Create and View network
-----------------------
* create: `sudo docker network create --driver bridge my_nw`
* view: `sudo docker network ls`

![image](https://user-images.githubusercontent.com/17001948/44581949-6df17b80-a7bd-11e8-84a1-d8b0ce469595.png)

Create Nginx Image
------------------
* Download this repository. Go to the repostiroy directory. Open the terminal.
* create image: `sudo docker build -t my-nginx-image .`
![image](https://user-images.githubusercontent.com/17001948/44582806-62538400-a7c0-11e8-899e-a253e9d2e246.png)
You will see below screen while running the above command.
![image](https://user-images.githubusercontent.com/17001948/44582827-7bf4cb80-a7c0-11e8-9d48-43f3f33c6cc8.png)
Imgae create successfully
![image](https://user-images.githubusercontent.com/17001948/44582856-99c23080-a7c0-11e8-9cc5-979fe96b9691.png)

* view: `sudo docker images`
![image](https://user-images.githubusercontent.com/17001948/44582903-bc544980-a7c0-11e8-92ec-6a4706e214a1.png)

Run Image As Container(mynginx1) By Attaching With The Network Name
---------------------------------------------------------
* run : `sudo docker run --rm --name mynginx1 -d -p 81:80 my-nginx-image`
* view: `sudo docker ps`
* mynginx1 is exposed to 81 port of the localhost.
Run Image As Container(mynginx2) By Attaching With The Network Name
---------------------------------------------------------
* run : `sudo docker run --rm --name mynginx2 -d -p 82:80 my-nginx-image`
* view: `sudo docker ps`
* mynginx1 is exposed to 82 port of the localhost.
![image](https://user-images.githubusercontent.com/17001948/44583415-d42ccd00-a7c2-11e8-8438-96264f60147b.png)

Access Each Container Using Curl
--------------------------------
* curl(mynginx1) : `curl http://localhost:81`
![image](https://user-images.githubusercontent.com/17001948/44583516-4a313400-a7c3-11e8-9463-4c34af79f201.png)

* curl(mynginx2) : `curl http://localhost:82`
![image](https://user-images.githubusercontent.com/17001948/44583530-5cab6d80-a7c3-11e8-8de5-1f98c03ee760.png)


